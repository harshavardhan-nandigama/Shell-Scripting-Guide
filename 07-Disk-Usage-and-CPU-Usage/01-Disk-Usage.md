# 🚨 Disk Usage Monitor 

A production-ready shell script to monitor disk usage on Linux servers and trigger email alerts when usage crosses a defined threshold. Ideal for system administrators, DevOps engineers, or students learning shell scripting

**Objective**

- Automatically detect disk partitions with usage above a set threshold.
- Send email alerts with server IP and usage details.
- Easy to customize, readable for non-IT students, and cron-job friendly.


 ## Script: disk-usage-monitor.sh

        #!/bin/bash

        # Get disk usage details, exclude 'tmpfs' and 'udev' file systems
        DISK_USAGE=$(df -hT | grep -vE '^Filesystem|tmpfs|udev')

        # Set threshold for disk usage percentage
        DISK_THRESHOLD=75

        # Initialize message variable for alert content
        MSG=""

        # Get local IP address (useful for identifying the server)
        IP=$(curl -s http://169.254.169.254/latest/meta-data/local-ipv4)

        # Read each line of disk usage info
        while IFS= read -r line; do
            # Extract the usage percentage and remove the '%' symbol
            USAGE=$(echo "$line" | awk '{print $(NF-2)}' | tr -d '%')
            
            # Get the name of the disk partition (e.g., /, /var)
            PARTITION=$(echo "$line" | awk '{print $NF}')
            
            # Check if usage is above the threshold
            if [ "$USAGE" -ge "$DISK_THRESHOLD" ]; then
                # Append warning message
                MSG+="High Disk Usage on $PARTITION: $USAGE%<br>"
            fi
        done <<< "$DISK_USAGE"

        # If any warning message exists, send an email
        if [ -n "$MSG" ]; then
            sh mail.sh "DevOps Team" "High Disk Usage Alert" "$IP" "$MSG" "info@joindevops.com" "ALERT - High Disk Usage"
        fi

                

### Explanation (Line-by-Line)

`#!/bin/bash`
Declares the interpreter to execute this script.

`DISK_USAGE=$(df -hT | grep -vE '^Filesystem|tmpfs|udev')`
Fetches disk usage (df -hT), removing unwanted file systems.

`DISK_THRESHOLD=75`
Sets the alert threshold to 75%. You can change it.

`MSG=""`
Creates an empty message string to hold alerts.

`IP=$(curl -s http://169.254.169.254/latest/meta-data/local-ipv4)`
Gets the server’s private IP (used for AWS EC2).

`while IFS= read -r line; do`
Starts reading each line of the disk usage report.

`USAGE=$(...)`
Extracts the second-to-last column (disk usage %), removes %.

`PARTITION=$(...)`
Extracts the last column (partition name like /, /var).

`if [ "$USAGE" -ge "$DISK_THRESHOLD" ]; then`
Checks if usage is greater than or equal to the threshold.

`MSG+="..."`
Adds a new warning line in the alert message.

`done <<< "$DISK_USAGE"`
Feeds the disk usage list into the while loop.

`if [ -n "$MSG" ]; then`
If the message is not empty, it means we found issues.

`sh mail.sh ...`
Calls an external script to send an HTML-formatted email.