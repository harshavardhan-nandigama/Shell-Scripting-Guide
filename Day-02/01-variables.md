
## What is a Variable in Shell?

A variable is a named storage that holds a value which can be reused later in your script.
Syntax:

    VAR_NAME=value

🚫 No spaces between VAR_NAME, =, and value

To access the value, prefix it with a dollar sign **$VAR_NAME.**

## Shell Scripting: Understanding Variables

In shell scripting, variables are used to store data that can be reused throughout the script. Think of variables as containers that hold information like names, numbers, paths, or results of commands.

There are two types of variables:

User-defined variables (like NAME=John)

System-defined variables (like $HOME, $USER)

## 📝 Example 01: Hardcoded Variables

    #!/bin/bash
    # This line tells the system to use bash shell to interpret the script

    PERSON1=Modi   # Declares a variable PERSON1 and assigns it the value "Modi"
    PERSON2=Musk   # Declares another variable PERSON2 with value "Musk"

    # Using the variables inside echo to simulate a conversation

    echo "$PERSON1:: Hey $PERSON2, How are you?"
    echo "$PERSON2:: Hello $PERSON1, I am fine. How are you doing?"
    echo "$PERSON1:: I am fine too. What's up?"
    echo "$PERSON2:: Nothing, just going to Mars now, will you come?"
    echo "$PERSON1:: Sorry, you carry on! I will come once you come back."


**📌 Key Takeaway:**

Variable assignment must not have spaces around =.

$VARIABLE_NAME is how we refer to a variable.

## 📝 Example Script 02: Positional Parameters (Dynamic Variables) 

    #!/bin/bash
    # The script now accepts user input from command-line arguments

    PERSON1=$1  # Assigns the first argument passed to the script to PERSON1
    PERSON2=$2  # Assigns the second argument to PERSON2

    # Using the inputs dynamically

    echo "$PERSON1:: Hey $PERSON2, How are you?"
    echo "$PERSON2:: Hello $PERSON1, I am fine. How are you doing?"
    echo "$PERSON1:: I am fine too. What's up?"
    echo "$PERSON2:: Nothing, just going to Mars now, will you come?"
    echo "$PERSON1:: Sorry, you carry on! I will come once you come back."

**Usage Example:**

    bash script.sh Raju Rani

**📌 Key Takeaway:**

**$1, $2, etc.**, are positional parameters that take values passed during execution.

## 📝 Example 03: Using read and -s for Sensitive Input

    #!/bin/bash

    echo "Enter your pin number::"

    read -s PIN  # -s means silent; it hides input (like passwords). The input is stored in variable PIN.

    echo "Your number is: $PIN"

**📌 Key Takeaway:**

**read** command is used to take user input.

**-s** option hides the input (ideal for passwords or PINs).

## Example 04: Simple Math Using Variables

    #!/bin/bash

    NUM1=10        # Assigning number 10 to variable NUM1
    NUM2=5         # Assigning number 5 to variable NUM2

    SUM=$((NUM1 + NUM2))  # Performing addition using arithmetic expansion

    echo "Sum of $NUM1 and $NUM2 is: $SUM"

**📌 Key Takeaway:**

Use $((expression)) to perform arithmetic in shell.

You can do +, -, *, /, and % inside this.

