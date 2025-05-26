# Conditions

**Conditions (if, else, comparisons)**
Conditions are one of the core parts of scripting — they help the script make decisions. In shell scripting, we use if, else, elif blocks to check conditions.

Common Operators in Conditions

| Operator |       Meaning         |
| -------- | --------------------- |
| `-eq`    | Equal to              |
| `-ne`    | Not equal to          |
| `-lt`    | Less than             |
| `-le`    | Less than or equal to |
| `-gt`    | Greater than          |
| `-ge`    | Greater than or equal |


## Example 1: Check if a number is less than 10


    #!/bin/bash  # This tells the system to use bash shell to run this script


    NUMBER=$1     # The first command-line argument is stored in the variable NUMBER


    # Below we are using an 'if' condition to compare NUMBER

    if [ $NUMBER -lt 10 ]  # -lt means 'less than'
    then
        echo "Given number $NUMBER is less than 10"  # This line will run if the condition is true
    else
        echo "Given number $NUMBER is not less than 10"  # This line will run if the condition is false
    fi  # This marks the end of the if-else block


## Example 2: Check if a number is even or odd

    #!/bin/bash

    NUMBER=$1  # Accept the first argument from the command line


    # Use modulus operator % to find remainder
    

    if [ $((NUMBER % 2)) -eq 0 ]  # If remainder is 0, it's even
    then
        echo "Number $NUMBER is Even"
    else
        echo "Number $NUMBER is Odd"
    fi


## Example 3: Check if a file exists

    #!/bin/bash

    FILENAME=$1  # Take filename from the user as the first argument

    # Use -f to check if it's a regular file
    if [ -f "$FILENAME" ]
    then
        echo "File '$FILENAME' exists."
    else
        echo "File '$FILENAME' does not exist."
    fi


# Note

$1 – This is a special variable that gets the first argument passed to the script.

[ condition ] – This is how we write conditions in bash. There must be a space after [ and before ].

Always test your script with different inputs to understand how conditions behave.

