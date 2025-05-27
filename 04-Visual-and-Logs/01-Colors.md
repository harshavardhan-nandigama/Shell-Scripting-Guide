# 🎨 Shell Scripting: Using Colors in Terminal Output

colors in shell scripts to make output more readable and attractive. Colors are often used in real-world scripts to highlight success, errors, warnings, and guide users more effectively. It's very useful in DevOps, Linux administration, and automation tasks.

## 🌈 How to Use Colors in Shell Scripting?

We can print colored text in the terminal using ANSI escape sequences like:

    echo -e "\e[31m This is red text \e[0m"

**Format Breakdown:**

- **-e**: Enables interpretation of escape characters.

- **\e[**: Begins the escape sequence.

- **31m**: Color code (red in this case).

- **\e[0m**: Resets the color to normal.

 ## 🌈 Common Color Codes:

| Color   | Code | Example  |
| ------- | ---- | -------- |
| Red     | 31   | `\e[31m` |
| Green   | 32   | `\e[32m` |
| Yellow  | 33   | `\e[33m` |
| Blue    | 34   | `\e[34m` |
| Magenta | 35   | `\e[35m` |
| Cyan    | 36   | `\e[36m` |
| Reset   | 0    | `\e[0m`  |


## xample 1: Basic Color Usage

    #!/bin/bash

    # Prints red-colored text
    echo -e "\e[31m Hello Colors \e[0m"

    # Prints text without any color
    echo "Hello No Colors"

**Explanation:**

**\e[31m:** Sets text to red.

**\e[0m:** Resets color to normal.

This is useful for warnings or error messages.

## Example 2: Using Colors in Real-Time Validations

    #!/bin/bash

    # Get current user's ID (0 = root)
    USERID=$(id -u)

    # Define color codes
    R="\e[31m"  # Red for errors/failures
    G="\e[32m"  # Green for success
    Y="\e[33m"  # Yellow for warnings/info
    N="\e[0m"   # Reset color to normal

    
**🔐 Root User Check**

    if [ $USERID -ne 0 ]
    then
        echo -e "$R ERROR:: Please run this script with root access $N"
        exit 1
    else
        echo "You are running with root access"
    fi


id -u: Returns user ID.

If not root (ID != 0), script exits with error in red.

**Validation Function**

    VALIDATE(){
        if [ $1 -eq 0 ]
        then
            echo -e "Installing $2 is ... $G SUCCESS $N"
        else
            echo -e "Installing $2 is ... $R FAILURE $N"
            exit 1
        fi
    }

$1: Exit status of previous command.

$2: Package name.

Green = success, Red = failure, then exits if failed.

## Package Installation Check and Install (MySQL, Python3, Nginx)

    dnf list installed mysql
    if [ $? -ne 0 ]
    then
        echo "MySQL is not installed... going to install it"
        dnf install mysql -y
        VALIDATE $? "MySQL"
    else
        echo -e "Nothing to do MySQL... $Y already installed $N"
    fi

- **dnf list installed <pkg>**: Checks if package is installed.

- **$?**: Checks if previous command failed (not found).

- **If not found**, installs and validates.

- **Yellow** = info, package already installed

## Example 3: Colorful Success and Error Menu

    #!/bin/bash

    GREEN="\e[32m"
    RED="\e[31m"
    NORMAL="\e[0m"

    read -p "Enter your name: " NAME

    if [ -z "$NAME" ]; then
        echo -e "${RED}Error: Name cannot be empty!${NORMAL}"
    else
        echo -e "${GREEN}Welcome, $NAME! Script executed successfully.${NORMAL}"
    fi

**What's Happening:**

**read**: Takes user input.

**-z "$NAME"**: Checks if input is empty.

Red for error, green for success.

