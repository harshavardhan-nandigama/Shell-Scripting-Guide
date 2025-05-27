# 📅 Day 5 - Install Commands and Set commands

**📘 Learnings Covered - Day 5: Install Commands and Set Command**

| # |       Topic      |                            Description                           |
| - | ---------------- | ---------------------------------------------------------------- |
| 1 | Install Commands | Check and install packages using `dnf` or `apt`                  |
| 2 | Set Command      | Using `set -e`, `set -x` for debugging and strict error handling |

## 01 - Install Commands in Shell Script

    #!/bin/bash

    USERID=$(id -u)

    if [ $USERID -ne 0 ]
    then
        echo "ERROR:: Please run this script with root access"
        exit 1
    else
        echo "You are running with root access"
    fi

    dnf list installed mysql

    if [ $? -ne 0 ]
    then
        echo "MySQL is not installed... going to install it"
        dnf install mysql -y
        if [ $? -eq 0 ]
        then
            echo "Installing MySQL is ... SUCCESS"
        else
            echo "Installing MySQL is ... FAILURE"
            exit 1
        fi
    else
        echo "MySQL is already installed...Nothing to do"
    fi


**Line-by-Line Explanation:**

        USERID=$(id -u)

➤ Get the current user's ID. Root user always has ID 0.

        if [ $USERID -ne 0 ]

➤ Check if the script is NOT being run as root. Exit if true.

        dnf list installed mysql

➤ Check if MySQL is already installed using dnf.

        if [ $? -ne 0 ]

➤ $? is the exit status of the last command. If not 0, MySQL is not installed.

        dnf install mysql -y

➤ If MySQL is missing, install it with -y to auto-confirm.


**Why This Is Useful:**

- Automates installation of required packages

- Prevents double installations

- Ensures script is run by the right user (root)

- Adds basic error handling


 ## 02 - set Command in Shell Script

        #!/bin/bash

        set -e

        echo "Hi, Good Morning"
        echoooooo "Hello, this will be error"
        echo "Hello, Morning"

**Line-by-Line Explanation:**

        set -e

➤ If any command fails, stop the script immediately. This prevents further execution after an error.

        echo "Hi, Good Morning"

➤ A simple greeting.

        echoooooo (intentional typo)

➤ This line will throw an error and stop the script. The next line won't be executed.

        echo "Hello, Morning"

➤ This will not run due to the error above — because of set -e.


**Why This Is Useful:**

- Prevents half-completed operations (great for DevOps and automation)

- Makes debugging easier by stopping exactly where something fails

- Industry standard in CI/CD pipelines and deployment scripts