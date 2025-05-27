# 📅 Day 4 - Colors and Logs

📘 **Learnings Covered**

| # |   Topic    |                           Description                                       |
| - | ---------- | --------------------------------------------------------------------------- |
| 1 | Colors     | Make script output visually readable using ANSI color codes                 |
| 2 | Logs       | Add logging mechanisms to track events, tasks, and errors                   |
| 3 | Validation | Validate user access (root/non-root), command outputs, and package installs |
| 4 | Daily Logs | Create date-based log files for automation and cron jobs                    |



# 🎨 Colors in Shell Script
Using colors makes script output visually intuitive, especially for:

✅ Status messages (Success, Error, Warnings)

✅ Differentiating between normal and alert outputs

✅ Improving readability in CLI tools

## Learning 1: Colors in Shell Script

    #!/bin/bash

    echo -e "\e[31m Hello Colors \e[0m"
    echo "Hello No Colors"

    Explanation:

\e[31m → Red text

\e[0m → Resets color to default

-e in echo enables escape sequence interpretation

**Script:2**

    #!/bin/bash

    USERID=$(id -u)
    R="\e[31m"
    G="\e[32m"
    Y="\e[33m"
    N="\e[0m"

    if [ $USERID -ne 0 ]; then
        echo -e "$R ERROR:: Please run this script with root access $N"
        exit 1
    else
        echo -e "$G You are running with root access $N"
    fi

    VALIDATE() {
        if [ $1 -eq 0 ]; then
            echo -e "Installing $2 ... $G SUCCESS $N"
        else
            echo -e "Installing $2 ... $R FAILURE $N"
            exit 1
        fi
    }

    dnf list installed mysql &> /dev/null
    if [ $? -ne 0 ]; then
        echo "MySQL is not installed. Installing..."
        dnf install mysql -y &> /dev/null
        VALIDATE $? "MySQL"
    else
        echo -e "MySQL is $Y already installed $N"
    fi

# Learning 2: Logging Basics

    #!/bin/bash

    LOGFILE="/tmp/basic_script.log"
    echo "[$(date)] Script started" >> $LOGFILE
    echo "[$(date)] Doing a task..." >> $LOGFILE
    sleep 2
    echo "[$(date)] Task completed successfully" >> $LOGFILE


**Explanation:**

Logs are written with timestamps

>> appends logs to file

Useful for debugging and audits

✅ Use Case: Background jobs, long-running tasks, cron jobs


## Learning 3: Validation + Logging

    #!/bin/bash

    LOGFILE="/tmp/install.log"
    RED="\e[31m"
    GREEN="\e[32m"
    YELLOW="\e[33m"
    RESET="\e[0m"

    if [ "$(id -u)" -ne 0 ]; then
        echo -e "${RED}ERROR: Run this script as root!${RESET}" | tee -a $LOGFILE
        exit 1
    fi

    VALIDATE() {
        if [ $1 -eq 0 ]; then
            echo -e "$2 ... ${GREEN}SUCCESS${RESET}" | tee -a $LOGFILE
        else
            echo -e "$2 ... ${RED}FAILED${RESET}" | tee -a $LOGFILE
            exit 1
        fi
    }

    for pkg in mysql python3 nginx; do
        dnf list installed $pkg &> /dev/null
        if [ $? -ne 0 ]; then
            echo "Installing $pkg..."
            dnf install $pkg -y &> /dev/null
            VALIDATE $? "$pkg installation"
        else
            echo -e "${YELLOW}$pkg already installed${RESET}" | tee -a $LOGFILE
        fi
    done

**Explanation:**

- Combines tee to log and show output

- Validates install status

- Prevents repeated installation

✅ Use Case: Robust deployment and installation scripts


## Learning 4: Daily Logs with Timestamp

    #!/bin/bash

    TODAY=$(date +%F)
    LOGFILE="/tmp/log-$TODAY.log"

    echo "[$(date)] Daily job started" >> $LOGFILE
    sleep 1
    echo "[$(date)] Daily job finished" >> $LOGFILE
