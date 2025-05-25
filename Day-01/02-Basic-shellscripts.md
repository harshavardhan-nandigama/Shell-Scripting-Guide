


## Each Script Should Have....
For every .sh file, create a .md (markdown) file with:

🔹 Title

🔹 Purpose

🔹 Metadata

🔹 Script

🔹 Line-by-line Explanation

🔹 Output (Optional)


##  What is Metadata in a Shell Script?

Metadata is data about the script. It doesn’t affect how the script runs, but it helps developers and system administrators understand what the script is, who wrote it, and why.

 **Metadata in Shell Scripts - Example**

    #!/bin/bash
    # Author: Harshavardhan Nandigama
    # Date: 2025-05-25
    # Description: This script shows the use of metadata and prints system info
    # Version: 1.0
    # License: MIT


## Example Shell Sricpt

    #!/bin/bash
    # Author: Harshavardhan Nandigama
    # Date: 2025-05-25
    # Description: This script shows the use of metadata and prints system info
    # Version: 1.0
    # License: MIT

    # Print a welcome message
    echo "Welcome to my metadata example shell script"

    # Print hostname
    echo "Hostname of this system: $(hostname)"

    # Print current user
    echo "You are logged in as: $USER"

    # Print current date
    echo "Today is: $(date)"

**Output for example shellscript**

    Welcome to my metadata example shell script
    Hostname of this system: myhost.local
    You are logged in as: harshavardhan
    Today is: Sat May 25 19:15:00 IST 2025
