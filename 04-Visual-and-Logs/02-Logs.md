# Logs
**Why Logging Is Important in Shell Scripts?**

- Debugging issues when something fails

- Tracking actions performed by the script

- Understanding who ran the script, when, and what happened

- Auditing installation, deployment, or any automated task

**Basic Logging Concepts**

There are typically two types of logs:

Standard Output **(stdout)** – normal information

Standard Error **(stderr)** – error messages


**In shell, we use:**

- **1>** for stdout

- **2>** for stderr

- **>>** to append to the log file

- **&>** to redirect both stdout and stderr

 ## Example 1: Basic Logging with Timestamps

    #!/bin/bash

    LOGFILE="/tmp/basic_script.log"   # Path to store logs

    echo "[$(date)] Script started" >> $LOGFILE

    echo "[$(date)] Doing a simulated task..." >> $LOGFILE
    sleep 2  # Simulating a task

    echo "[$(date)] Task completed successfully" >> $LOGFILE

**Explanation:**

LOGFILE="/tmp/basic_script.log": All logs go to this file.

$(date): Inserts the current timestamp.

>>: Appends to the file without overwriting.

sleep 2: Mimics a real-time delay/task.



## Example 2: Logging with Colors + Validation + Error Handling

    #!/bin/bash

    LOGFILE="/tmp/install.log"

    # Define color codes
    RED="\e[31m"
    GREEN="\e[32m"
    YELLOW="\e[33m"
    RESET="\e[0m"

    # Check for root access
    if [ "$(id -u)" -ne 0 ]; then
        echo -e "${RED}ERROR: Run this script as root.${RESET}" | tee -a $LOGFILE
        exit 1
    fi

    # Validation Function
    validate() {
        if [ $1 -eq 0 ]; then
            echo -e "$2 ... ${GREEN}SUCCESS${RESET}" | tee -a $LOGFILE
        else
            echo -e "$2 ... ${RED}FAILED${RESET}" | tee -a $LOGFILE
            exit 1
        fi
    }

    echo "[$(date)] Script execution started" >> $LOGFILE

    # Install MySQL
    dnf list installed mysql &>> $LOGFILE
    if [ $? -ne 0 ]; then
        echo "Installing MySQL..." | tee -a $LOGFILE
        dnf install mysql -y &>> $LOGFILE
        validate $? "MySQL Installation"
    else
        echo -e "${YELLOW}MySQL already installed${RESET}" | tee -a $LOGFILE
    fi

    # Install Python3
    dnf list installed python3 &>> $LOGFILE
    if [ $? -ne 0 ]; then
        echo "Installing Python3..." | tee -a $LOGFILE
        dnf install python3 -y &>> $LOGFILE
        validate $? "Python3 Installation"
    else
        echo -e "${YELLOW}Python3 already installed${RESET}" | tee -a $LOGFILE
    fi

    # Install Nginx
    dnf list installed nginx &>> $LOGFILE
    if [ $? -ne 0 ]; then
        echo "Installing Nginx..." | tee -a $LOGFILE
        dnf install nginx -y &>> $LOGFILE
        validate $? "Nginx Installation"
    else
        echo -e "${YELLOW}Nginx already installed${RESET}" | tee -a $LOGFILE
    fi

    echo "[$(date)] Script execution completed" >> $LOGFILE


Explanation

|         Code              |                         Purpose                               |
| ------------------------- | ------------------------------------------------------------- |
| `tee -a $LOGFILE`         | Appends output to both terminal and log file                  |
| `&>> $LOGFILE`            | Redirects both standard output and standard error to log file |
| `validate $? "Task Name"` | Checks if the previous command succeeded or failed            |
| `echo -e`                 | Enables interpretation of escape characters (for colors)      |


## Example: Daily Log File Generator

    #!/bin/bash

    TODAY=$(date +%F)     # 2025-05-26 format
    LOGFILE="/tmp/log-$TODAY.log"

    echo "[$(date)] Daily job started" >> $LOGFILE
    # Simulate work
    sleep 1
    echo "[$(date)] Job completed" >> $LOGFILE

This script creates a new log file every day with the date in its name — great for daily cron jobs or automated backups.

## 🔥 Pro Tips

|      Tip       |                   Description                    |
| -------------- | ------------------------------------------------ |
| Use `set -x`   | Debug mode: logs every command before executing  |
| Use timestamps | Always log with `$(date)` for traceability       |
| Log errors     | Redirect errors using `2>>` or `&>>`             |
| Archive logs   | Use `logrotate` to compress & rotate old logs    |
| Add log levels | Use tags like `INFO`, `ERROR`, `WARNING`, etc.   |
| Use functions  | Modular logging improves clarity and reusability |


