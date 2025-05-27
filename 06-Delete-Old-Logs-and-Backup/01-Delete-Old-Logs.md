# Delete Old Log Files (14+ Days)

A production-friendly shell script that safely deletes .log files older than 14 days from a specified directory, with logging, error handling, and status color-coding.

**Script Features**

✅ Root access verification
✅ Deletes only .log files older than 14 days
✅ Color-coded and timestamped logging
✅ Reusable validation function
✅ Handles spaces and special characters in filenames

## Full Script with Inline Explanation

    #!/bin/bash

🔹 Tells the system to use bash to execute the script.

    USERID=$(id -u)
    R="\e[31m"  # Red
    G="\e[32m"  # Green
    Y="\e[33m"  # Yellow
    N="\e[0m"   # No Color

🔹 Fetches the current user's ID and sets up color codes for pretty output.

    LOGS_FOLDER="/var/log/shellscript-logs"
    SCRIPT_NAME=$(basename "$0" | cut -d "." -f1)
    LOG_FILE="$LOGS_FOLDER/$SCRIPT_NAME.log"
    SOURCE_DIR="/home/ec2-user/app-logs"

**🔹 Defines:**

- where logs will be stored,

- dynamic naming for the script log file, and

- the folder where old logs are searched


    mkdir -p "$LOGS_FOLDER"

🔹 Ensures the log folder exists.


**🔒 Root Permission Check**

    if [ $USERID -ne 0 ]; then
        echo -e "$R ERROR:: Please run this script with root access $N" | tee -a "$LOG_FILE"
        exit 1
    else
        echo "You are running with root access" | tee -a "$LOG_FILE"
    fi


🔹 If not run as root, it exits with a clear error message.

# ✅ Validation Function

    VALIDATE(){
        if [ $1 -eq 0 ]; then
            echo -e "$2 is ... $G SUCCESS $N" | tee -a "$LOG_FILE"
        else
            echo -e "$2 is ... $R FAILURE $N" | tee -a "$LOG_FILE"
            exit 1
        fi
    }

🔹 Simplifies status checking and prints clean success or error messages.

**Execution Log Start**

    echo "Script started executing at $(date)" | tee -a "$LOG_FILE"


**Delete Old Logs (14+ days)**

    find "$SOURCE_DIR" -name "*.log" -mtime +14 -print0 | while IFS= read -r -d '' filepath
    do
        echo "Deleting file: $filepath" | tee -a "$LOG_FILE"
        rm -rf "$filepath"
        VALIDATE $? "Deleting $filepath"
    done

🔹 This:

- Finds .log files older than 14 days

- Deletes each file and validates the action

- Handles filenames with spaces using -print0 and read -d ''

**Execution Log End**

    echo "Script finished executing at $(date)" | tee -a "$LOG_FILE"

🔹 Marks end time of the script.
















