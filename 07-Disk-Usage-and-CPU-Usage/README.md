# 📅 Day 07 -  Disk Usage and CPU Usage

**📘 Learnings Covered - Day 7: Disk Usage and CPU Usage**

| # | Topic      | Description                                                   |
| - | ---------- | ------------------------------------------------------------- |
| 1 | Disk Usage | Monitor disk usage using `df`, `du`, and alerts for low space |
| 2 | CPU Usage  | Check CPU load with `top`, `uptime`, and log high usage       |



## 📁 Files Included

- `disk-usage-monitor.sh` — Monitors disk space usage and sends alert if threshold is breached.
- `cpu-usage-monitor.sh` — Continuously prints real-time CPU usage to the terminal.

---

##  Disk Usage Monitor


        #!/bin/bash

        DISK_USAGE=$(df -hT | grep -vE '^Filesystem|tmpfs|udev')
        DISK_THRESHOLD=75
        MSG=""
        IP=$(curl -s http://169.254.169.254/latest/meta-data/local-ipv4)

        while IFS= read -r line; do
            USAGE=$(echo "$line" | awk '{print $(NF-2)}' | tr -d '%')
            PARTITION=$(echo "$line" | awk '{print $NF}')
            if [ "$USAGE" -ge "$DISK_THRESHOLD" ]; then
                MSG+="High Disk Usage on $PARTITION: $USAGE%<br>"
            fi
        done <<< "$DISK_USAGE"

        if [ -n "$MSG" ]; then
            sh mail.sh "DevOps Team" "High Disk Usage" "$IP" "$MSG" "info@joindevops.com" "ALERT-High Disk Usage"
        fi

## Disk Usage Monitor — Explanation (Line-by-Line)


        1. `#!/bin/bash`  
        - Tells the system to run this script with the Bash shell.

        2. `DISK_USAGE=$(df -hT | grep -vE '^Filesystem|tmpfs|udev')`  
        - Runs the `df` command to get disk usage with human-readable sizes and filesystem type, then excludes header and temporary filesystems.

        3. `DISK_THRESHOLD=75`  
        - Sets a threshold percentage (75%) for disk usage alerts.

        4. `MSG=""`  
        - Initializes an empty message string to collect alert details.

        5. `IP=$(curl -s http://169.254.169.254/latest/meta-data/local-ipv4)`  
        - Retrieves the local IP address of the machine from metadata (usually in cloud environments).

        6. `while IFS= read -r line; do`  
        - Starts reading the disk info line by line for processing.

        7. `USAGE=$(echo "$line" | awk '{print $(NF-2)}' | tr -d '%')`  
        - Extracts the disk usage percent (without the % sign) from the current line.

        8. `PARTITION=$(echo "$line" | awk '{print $NF}')`  
        - Extracts the partition name (like `/dev/sda1`).

        9. `if [ "$USAGE" -ge "$DISK_THRESHOLD" ]; then`  
        - Checks if the disk usage exceeds the threshold.

        10. `MSG+="High Disk Usage on $PARTITION: $USAGE%<br>"`  
            - Adds a message about this partition to the alert string.

        11. `done <<< "$DISK_USAGE"`  
            - Ends the loop after processing all partitions.

        12. `if [ -n "$MSG" ]; then`  
            - Checks if there are any alerts to send (message is not empty).

        13. `sh mail.sh "DevOps Team" "High Disk Usage" "$IP" "$MSG" "info@joindevops.com" "ALERT-High Disk Usage"`  
            - Calls another script to send an email alert with the details.


   ## CPU Usage Monitor          


        #!/bin/bash

        while true; do
        cpu_usage=$(top -b -n2 -p 1 | fgrep "Cpu(s)" | tail -1 | awk -F'id,' -v prefix="$prefix" '{
            split($1, vs, ",");
            v=vs[length(vs)];
            sub("%", "", v);
            printf "%s%.1f%%\n", prefix, 100 - v
        }')
        echo "CPU Usage: ${cpu_usage}"
        sleep 1
        done



## CPU Usage Monitor — Explanation (Line-by-Line)


        1. `#!/bin/bash`  
        - Specifies Bash shell to run the script.

        2. `while true; do`  
        - Starts an infinite loop to check CPU usage continuously.

        3. `cpu_usage=$(top -b -n2 -p 1 | fgrep "Cpu(s)" | tail -1 | awk -F'id,' -v prefix="$prefix" '{ split($1, vs, ","); v=vs[length(vs)]; sub("%", "", v); printf "%s%.1f%%\n", prefix, 100 - v }')`  
        - Runs the `top` command twice in batch mode to get accurate CPU stats for process ID 1, then extracts the idle CPU percentage, calculates CPU usage as `100 - idle`, and formats the output.

        4. `echo "CPU Usage: ${cpu_usage}"`  
        - Prints the CPU usage on the terminal.

        5. `sleep 1`  
        - Waits for 1 second before the next check to avoid flooding output.

        6. `done`  
        - Ends the loop block, but loops back because it’s infinite.


