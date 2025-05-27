# Backup and Clean Old Logs

This script backs up .log files older than a given number of days (default: 14), zips them into a timestamped file, and deletes the original log files after successful backup. It also logs the activity to a custom log file.

A simple, reliable, and reusable script to automate backup and cleanup of old log files in Linux environments.


## Features

✅ Root access validation

🧠 Defaults to 14-day retention if not provided

🔍 Finds .log files older than N days using find -mtime +N

📦 Zips old logs with timestamp

🧹 Deletes original files only if backup is successful

🪵 Detailed logging to /var/log/shellscript-logs/backup.log

✨ Color-coded output for better readability


**Example Usage**

    sudo bash backup-logs.sh /var/log/nginx /backup/logs 30

- /var/log/nginx: Source directory

- /backup/logs: Destination directory

- 30: (Optional) Retention period in days (default is 14)

**Output**

- Zipped logs: /backup/logs/app-logs-YYYY-MM-DD-HH-MM-SS.zip

- Log file: /var/log/shellscript-logs/backup.log


# Script Explained (Line by Line)

    #!/bin/bash

Declares the script to be interpreted using Bash shell.

    USERID=$(id -u)
    SOURCE_DIR="$1"
    DEST_DIR="$2"
    DAYS="${3:-14}"

- Captures current user ID.

- Takes input parameters: source dir, destination dir, and number of days.

- Defaults to 14 days if $3 isn’t provided.


    LOGS_FOLDER="/var/log/shellscript-logs"
    SCRIPT_NAME=$(basename "$0" .sh)
    LOG_FILE="$LOGS_FOLDER/backup.log"

Sets up paths for script name and log storage.


    R="\e[31m"; G="\e[32m"; Y="\e[33m"; N="\e[0m"


Sets up color codes for red (errors), green (success), yellow (warnings), and reset.

**Function: VALIDATE()**

    VALIDATE(){
    if [ $1 -eq 0 ]; then
        echo -e "$2 is ... $G SUCCESS $N" | tee -a "$LOG_FILE"
    else
        echo -e "$2 is ... $R FAILURE $N" | tee -a "$LOG_FILE"
        exit 1
    fi
    }


- Takes exit status ($1) and command description ($2)

- Prints result and exits on failure.


 **Function: check_root()**

    check_root(){
    if [ "$USERID" -ne 0 ]; then
        echo -e "$R ERROR:: Please run this script with root access $N"
        exit 1
    else
        echo "You are running with root access"
    fi
    }
    check_root


- Ensures script is executed as root (UID 0).

- Aborts if not.

**Prepare Log Directory**

    mkdir -p "$LOGS_FOLDER"

Creates log folder if it doesn't exist.

❗ **Usage Validation**

    USAGE(){
    echo -e "$R USAGE:: $N sh $SCRIPT_NAME.sh <source-dir> <destination-dir> <days(optional)>"
    exit 1
    }

Prints correct usage and exits if arguments are insufficient.

**Argument & Directory Validation**

    if [ $# -lt 2 ]; then USAGE; fi
    if [ ! -d "$SOURCE_DIR" ]; then echo -e "$R Source directory not found $N"; exit 1; fi
    if [ ! -d "$DEST_DIR" ]; then echo -e "$R Destination directory not found $N"; exit 1; fi


Validates source and destination directories exist.


**Find .log Files Older Than N Days**

    FILES=$(find "$SOURCE_DIR" -name "*.log" -mtime +"$DAYS")

Uses find to get logs older than $DAYS.

**Backup & Clean**

    if [ -n "$FILES" ]; then
    TIMESTAMP=$(date +%F-%H-%M-%S)
    ZIP_FILE="$DEST_DIR/app-logs-$TIMESTAMP.zip"

    echo "$FILES" | zip -@ "$ZIP_FILE"
    VALIDATE $? "Zipping log files"

Creates zip with timestamp and archives files using zip -@.


  if [ -f "$ZIP_FILE" ]; then
    while IFS= read -r filepath; do
      echo "Deleting: $filepath" | tee -a "$LOG_FILE"
      rm -f "$filepath"
      VALIDATE $? "Deleting $filepath"
    done <<< "$FILES"
  fi


Deletes each original log file only if zip is created successfully.

**Nothing to Backup**


    else
    echo -e "No log files older than $DAYS days ... $Y SKIPPING $N" | tee -a "$LOG_FILE"
    fi


Displays message if there’s nothing to archive.


## Want to Automate It?

Use cron to schedule automatic backups.

    crontab -e

Example:

    0 2 * * * /usr/bin/bash /scripts/backup-logs.sh /var/log/myapp /mnt/backups 7 

Runs daily at 2 AM.


**📘 Learning Outcomes**

- Learn bash scripting

- Master find, zip, rm, and tee

- Understand user validation & logging

- Build real-time production-friendly utilities




















