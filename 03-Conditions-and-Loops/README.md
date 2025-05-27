
# 📅 Day 03 - Conditions and Loops

**📘 Learnings Covered - Day 3: Conditions and Loops**

| # |     Topic       |                   Description                           |
| - | --------------- | ------------------------------------------------------- |
| 1 | Conditions      | Using `if`, `else`, `elif`, and test commands           |
| 2 | While Loop      | Executing a block of code repeatedly using `while` loop |
| 3 | For Loop        | Looping through lists and sequences with `for` loops    |
| 4 | Case Statements | Pattern matching using `case` statements (if included)  |

This document covers Day 3 of my Shell Scripting learning journey: focusing on conditions and loops with real-world examples. Scripts are explained line-by-line, so even beginners and non-IT learners can understand.

## Conditions

Conditions help us make decisions in scripts based on input values or system states.

🔹 **Common Conditional Operators:**

| Operator |       Meaning       |
| -------- | ------------------- |
| `-eq`    | Equal to            |
| `-ne`    | Not equal to        |
| `-gt`    | Greater than        |
| `-lt`    | Less than           |
| `-ge`    | Greater or equal to |
| `-le`    | Less or equal to    |

## Example 1: Check if a number is less than 10

#!/bin/bash

NUMBER=$1  # Accept input from user as the first argument

# Compare the number using condition

    if [ $NUMBER -lt 10 ]
    then
    echo "Given number $NUMBER is less than 10"
    else
    echo "Given number $NUMBER is not less than 10"
    fi

    
**Explanation:**

- $1 takes the input number from the user.

- if [ $NUMBER -lt 10 ]: Checks if the number is less than 10.

- then: Executes the code block if condition is true.

- else: Runs if the condition is false.


# 🔁 Loops

Loops are used to run a set of commands multiple times.

##Example 2: Using for loop to install multiple packages


    #!/bin/bash

    PACKAGES=("nginx" "mysql" "python")

    for pkg in "${PACKAGES[@]}"
    do
    echo "Checking $pkg..."
    dnf list installed $pkg &>/dev/null

    if [ $? -ne 0 ]; then
        echo "$pkg not found, installing..."
        dnf install $pkg -y
    else
        echo "$pkg is already installed."
    fi
    done


**Explanation:**

- PACKAGES=(...): List of package names.

- for pkg in ...: Loops through each item.

- dnf list installed: Checks if the package is installed.

- $? -ne 0: Means the package is not found.


## Example 3: Simple while loop countdown

    #!/bin/bash

    i=5
    while [ $i -gt 0 ]
    do
    echo "Countdown: $i"
    ((i--))  # Decrement the counter
    done


**Explanation:**

- Starts from 5 and decreases until it reaches 0.

- ((i--)) decreases the value of i by 1 in each loop.


## Example 4: Combined Script (Validation, Logging, Loop, Condition)
    #!/bin/bash

    USERID=$(id -u)
    R="\e[31m"  # Red
    G="\e[32m"  # Green
    Y="\e[33m"  # Yellow
    N="\e[0m"   # Normal
    LOGS_FOLDER="/var/log/shellscript-logs"
    SCRIPT_NAME=$(basename "$0")
    LOG_FILE="$LOGS_FOLDER/${SCRIPT_NAME%.sh}.log"
    mkdir -p $LOGS_FOLDER

    echo "Script started at: $(date)" | tee -a $LOG_FILE

    if [ $USERID -ne 0 ]; then
    echo -e "$R ERROR: Please run as root! $N" | tee -a $LOG_FILE
    exit 1
    else
    echo "Running with root access" | tee -a $LOG_FILE
    fi

    VALIDATE(){
    if [ $1 -eq 0 ]; then
        echo -e "$2 is ... $G SUCCESS $N" | tee -a $LOG_FILE
    else
        echo -e "$2 is ... $R FAILED $N" | tee -a $LOG_FILE
        exit 1
    fi
    }

    for pkg in "$@"
    do
    dnf list installed $pkg &>> $LOG_FILE
    if [ $? -ne 0 ]; then
        echo "$pkg not found. Installing..." | tee -a $LOG_FILE
        dnf install $pkg -y &>> $LOG_FILE
        VALIDATE $? "$pkg"
    else
        echo -e "$Y $pkg is already installed. Skipping... $N" | tee -a $LOG_FILE
    fi
    done



**📁 Scripts Summary**

|        Script Name         |                Description                  |
| -------------------------- | ------------------------------------------- |
| `check-number.sh`          | Basic if-else condition with input number   |
| `package-installer-for.sh` | Install packages using `for` loop           |
| `countdown-while.sh`       | Countdown from 5 using `while` loop         |
| `validate-install.sh`      | Real-time logging, loop, root check, colors |









