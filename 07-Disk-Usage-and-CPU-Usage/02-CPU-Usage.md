
 # CPU-usage-monitor

 ### cpu-usage-monitor.sh

        #!/bin/bash  # Use Bash shell interpreter

        # Infinite loop to monitor CPU usage continuously
        while true; do

        # Fetch CPU usage using 'top' command:
        # -b: batch mode (for scripting)
        # -n2: take 2 samples (first is often inaccurate)
        # -p 1: focus on process with PID 1 (usually systemd/init)
        # 'fgrep "Cpu(s)"' filters CPU lines
        # 'tail -1' picks the second sample
        cpu_usage=$(top -b -n2 -p 1 | fgrep "Cpu(s)" | tail -1 | \
            awk -F'id,' -v prefix="$prefix" '{
            # Split the first part of the line by comma
            split($1, vs, ",");

            # Get the last value (idle %)
            v=vs[length(vs)];

            # Remove '%' if present
            sub("%", "", v);

            # Subtract idle from 100 to get used CPU percentage
            printf "%s%.1f%%\n", prefix, 100 - v
            }'
        )

        # Print the final CPU usage to the terminal
        echo "CPU Usage: ${cpu_usage}"

        # Wait for 1 second before next iteration
        sleep 1
        done


