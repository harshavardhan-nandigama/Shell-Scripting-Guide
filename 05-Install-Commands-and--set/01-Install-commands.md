# Install Commands with Validation

This script demonstrates how to install a package (e.g., MySQL) using dnf in a shell script with proper validation, logging, and permission checks. It's written to help beginners and non-IT learners understand every line step-by-step.

## Script: Install MySQL with Validation

         #!/bin/bash

This is called a shebang. It tells the system that this script should be run using the Bash shell.

            USERID=$(id -u)

- id -u returns the numeric user ID of the current user.

- We store it in a variable called USERID to check if the user is root or not.

- Root users always have a user ID of 0.   



        if [ $USERID -ne 0 ]
        then
            echo "ERROR:: Please run this script with root access"
            exit 1
        else
            echo "You are running with root access"
        fi



- -ne means "not equal". If user is not root, we:

- Print an error message.

- Exit the script with status 1 (which signals failure).

- If the user is root, we proceed.


        dnf list installed mysql


- Checks if **MySQL** is already installed on the system using dnf.

- dnf is the default package manager in RHEL/CentOS 8+.

- If the package is installed, it returns exit status 0.


            if [ $? -ne 0 ]
            then
                echo "MySQL is not installed... going to install it"

 
 - $? contains the exit status of the last command.

- If MySQL was not found, we move ahead to install it



             dnf install mysql -y


- Checks if MySQL is already installed on the system using dnf.

- dnf is the default package manager in RHEL/CentOS 8+.

- If the package is installed, it returns exit status 0.



        if [ $? -eq 0 ]
        then
            echo "Installing MySQL is ... SUCCESS"
        else
            echo "Installing MySQL is ... FAILURE"
            exit 1
        fi

- Again, we check the exit status:

- 0 means successful installation.

- Any other number means it failed. So we exit with code 1.


        else
            echo "MySQL is already installed...Nothing to do"
        fi


If MySQL was already installed (dnf list installed mysql was successful), we skip the installation.

## Basic Script: Install Multiple Packages

        #!/bin/bash

        PACKAGES=("mysql" "git" "wget")

        for pkg in "${PACKAGES[@]}"
        do
            if ! dnf list installed "$pkg" &>/dev/null
            then
                echo "$pkg is not installed. Installing..."
                dnf install -y "$pkg"
            else
                echo "$pkg is already installed."
            fi
        done

- Uses an array to loop through multiple package names.

- Cleaner and reusable format.

- Redirects output to /dev/null for quiet checks.

 ## Key Concepts Learned

|        Concept          |                      Description                            |
| ----------------------- | ----------------------------------------------------------- |
| Shebang (`#!/bin/bash`) | Tells the system to use Bash shell to run the script        |
| `id -u`                 | Gets the current user’s UID to check if root                |
| `$?`                    | Captures exit status of last executed command               |
| `dnf list installed`    | Checks if a package is already installed                    |
| `dnf install -y`        | Installs a package without user interaction                 |
| `exit` codes            | Used to exit the script gracefully based on success/failure |
