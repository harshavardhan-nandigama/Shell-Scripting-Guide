# 📅 Day 01 - Introduction to Shell Scripting

**📘 Learnings Covered - Day 1: Introduction**

| # |   Topic       |                  Description                        |
| - | ------------- | --------------------------------------------------- |
| 1 | What is Shell | Introduction to shell scripting and its importance  |
| 2 | Metadata      | Understanding `#!/bin/bash` and its role in scripts |
| 3 | Hello World   | Writing your first shell script with basic output   |
| 4 | Conversations | Reading input from users using `read` command       |

#  Key Concepts

##  What is Shebang?

Shebang (`#!`) is the first line in a shell script that tells the OS which interpreter to use to run the script. For example:


    #!/bin/bash


This means: “Use the **Bash shell** to execute this script.”

### What is Metadata in Shell Script?

Metadata is information *about* the script, like:

* Author name
* Creation date
* Description
* Version
* License

It helps others understand the purpose and origin of the script.

##  Script in this Folder

### `01-hello-script.sh`

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


## Output Example


    Welcome to my metadata example shell script
    Hostname of this system: myhost.local
    You are logged in as: harshavardhan
    Today is: Sat May 25 19:15:00 IST 2025


## Takeaways

* Always start a script with the correct **shebang**.
* Add **metadata comments** for clarity and professionalism.
* Use `echo` and shell commands like `hostname`, `date`, and `$USER` to create informative output.


📁 Ready for Day 02 ➡️ Variables, Inputs, and More!
