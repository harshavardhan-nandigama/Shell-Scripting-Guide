 # 📅 Day 6 -  Delete Old Logs and Backup Scripts 

 **📘 Learnings Covered - Day 6: Delete Old Logs and Backup Scripts**

| # |       Topic      |                       Description                         |
| - | --------------- | --------------------------------------------------------- |
| 1 | Delete Old Logs | Delete logs older than specific days using `find` command |
| 2 | Backup Scripts  | Create simple backup using `tar` and `rsync` commands     |

# Log Management Scripts – Clean, Backup & Automate Like a Pro

Two production-ready Bash scripts for efficient `.log` file **cleanup** and **backup**, built with best practices in mind: **safe deletion, automation, color-coded logging, error handling, and root access validation**.


## Common Features

- 🛡️ **Root access** check with exit on failure  
- 🎨 **Color-coded output** (Success, Error, Warning)  
- 🧠 **Reusable functions** for validation and status display  
- 📜 **Execution logs** stored at `/var/log/shellscript-logs/`  
- 📦 Designed for **cron automation** and real-world scenarios  

---

## 1. `delete-old-logs.sh`

> Automatically delete `.log` files older than 14 days from a defined directory.

### Configuration
- Set `SOURCE_DIR` inside the script (default: `/home/ec2-user/app-logs`)

### What It Does
- Finds all `.log` files older than 14 days  
- Deletes them safely  
- Logs each deletion to a file  
- Outputs **status** in color (green for success, red for failure)

### Sample Output

        Script started executing at 2025-05-27 12:00:00
        Deleting file: /home/ec2-user/app-logs/error log 1.log
        Deleting /home/ec2-user/app-logs/error log 1.log is ...  SUCCESS
        Script finished executing at 2025-05-27 12:00:01



# 2. backup-logs.sh

Backup and clean .log files older than N days with zip and validation

**Usage**

        sudo bash backup-logs.sh <source-dir> <destination-dir> [days]


- <source-dir> – Directory with .log files

- <destination-dir> – Backup output directory

- [days] – (Optional) Files older than N days (default: 14)

**Example**

        sudo bash backup-logs.sh /var/log/nginx /mnt/backups 30



- Finds .log files older than 30 days

- Creates a timestamped .zip file (e.g., app-logs-2025-05-27-12-30-00.zip)

- Deletes originals only if backup succeeds

- Logs all actions to /var/log/shellscript-logs/backup.log


## 🔁 Automation with Cron

Automate cleanup and backup using cron jobs:

        crontab -e


Example: Run backup every day at 2 AM:


        0 2 * * * /bin/bash /home/user/scripts/backup-logs.sh /var/log/myapp /mnt/backups 7


## Use Cases

- CI/CD log rotation

- Nginx/Apache log cleanup

- Application log backups

- Reduce disk usage on production servers


## 📚 Learning Objectives

This project helps you understand:

-  find, rm, zip, tee, read, basename

-  Bash scripting best practices (modular functions, root checks)

-  Logging and observability

-  Real-world Linux scripting automation




