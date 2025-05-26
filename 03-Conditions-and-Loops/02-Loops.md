# 🔁 Loops

Loops in shell scripting are powerful constructs that allow you to repeat a set of commands multiple times. They are commonly used in automation, monitoring, installation, and repetitive tasks.


## What Are Loops
| Type    | Description                                | Syntax Example                      |
| ------- | ------------------------------------------ | ----------------------------------- |
| `for`   | Repeats for each item in a list            | `for item in list; do ...; done`    |
| `while` | Repeats **while** a condition is true      | `while [ condition ]; do ...; done` |
| `until` | Repeats **until** a condition becomes true | `until [ condition ]; do ...; done` |


## Example 1: Basic for Loop – Print Numbers 1 to 5

    #!/bin/bash

    # Loop from 1 to 5
    for i in {1..5}
    do
        echo "Number: $i"
    done

**Outpu**

    Number: 1
    Number: 2
    Number: 3
    Number: 4
    Number: 5

**Explanation:**

    {1..5} is a range.

    The loop runs 5 times and prints each number.

Explanation:

{1..5} is a range.

The loop runs 5 times and prints each number.

## Example 2: while Loop – Countdown Timer

    #!/bin/bash

    count=5
    while [ $count -gt 0 ]
    do
        echo "Countdown: $count"
        sleep 1  # Wait for 1 second
        count=$((count - 1))  # Decrease the count
    done

    echo "🚀 Time's up!"

**Output:**
    Countdown: 5
    Countdown: 4
    ...
    🚀 Time's up!

## Example 3: Install Multiple Packages Using for Loop

    #!/bin/bash

    USERID=$(id -u)  # Get the user ID (0 = root)

    # Color codes for output styling
    R="\e[31m"  # Red for errors
    G="\e[32m"  # Green for success
    Y="\e[33m"  # Yellow for warning/info
    N="\e[0m"   # Reset color

    # Log file setup
    LOGS_FOLDER="/var/log/shellscript-logs"
    SCRIPT_NAME=$(basename "$0" | cut -d "." -f1)
    LOG_FILE="$LOGS_FOLDER/$SCRIPT_NAME.log"

    # Default packages list (can also be passed as arguments)
    PACKAGES=("mysql" "python" "nginx" "httpd")

    # Create log folder if it doesn't exist
    mkdir -p $LOGS_FOLDER

    # Start logging
    echo "Script started at: $(date)" | tee -a $LOG_FILE

    # Check if script is run as root
    if [ $USERID -ne 0 ]; then
        echo -e "$R ERROR: Please run this script as root $N" | tee -a $LOG_FILE
        exit 1
    else
        echo "Running with root access." | tee -a $LOG_FILE
    fi

    # Function to validate installation
    VALIDATE() {
        if [ $1 -eq 0 ]; then
            echo -e "Installing $2 ... $G SUCCESS $N" | tee -a $LOG_FILE
        else
            echo -e "Installing $2 ... $R FAILED $N" | tee -a $LOG_FILE
            exit 1
        fi
    }

    # Loop through each package passed as argument
    for package in "$@"
    do
        dnf list installed $package &>>$LOG_FILE
        if [ $? -ne 0 ]; then
            echo "$package is not installed. Installing..." | tee -a $LOG_FILE
            dnf install $package -y &>>$LOG_FILE
            VALIDATE $? "$package"
        else
            echo -e "$Y $package is already installed. Skipping. $N" | tee -a $LOG_FILE
        fi
    done

**Key Concepts Used**

    |       Concept        |         Explanation              |
    | -------------------- | -------------------------------- |
    | `$(id -u)`           | Gets current user's ID           |
    | `$@`                 | Represents all script arguments  |
    | `dnf list installed` | Checks if a package is installed |
    | `tee -a`             | Prints and appends to a log file |
    | `exit 1`             | Exits the script with error      |
