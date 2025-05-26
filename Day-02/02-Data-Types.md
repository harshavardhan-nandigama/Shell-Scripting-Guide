## Basics

**String** = Text (default in Bash) → "hello", "123"

**Integer** = Numbers (used in math) → 5, 100

**Array** = List of values → ("one" "two" "three")

**Associative Array** = Key-value pairs (like a dictionary) → name="John", age="25"

**Boolean** = Simulated using numbers (0=true, 1=false)

## Data Types in Shell Scripting

Data types in shell scripting mean the kind of data a variable can hold — like text, numbers, or a list of items.

But in Bash (shell scripting):

🔸 **All variables are treated as text (strings) by default.**

You don’t need to say, "This is a number" or "This is a string."
Instead, how you use the variable decides its behavior.

## Explanation of Each Data Type

**1. String (Default)**

Used for storing any text or characters.

    NAME="John"
    echo "Hello, $NAME"

**2. Integer**

Used in arithmetic operations. Must be used with $(( )) or let.

    A=5
    B=10
    echo "Sum: $((A + B))"

**3. Array**
Used to store multiple values in a single variable. Index starts at 0.

    FRUITS=("Apple" "Banana" "Cherry")
    echo "Second fruit: ${FRUITS[1]}"

**4. Associative Array**

Used to store key-value pairs (available in Bash 4+).

    declare -A student
    student[name]="Ali"
    student[age]=21
    echo "Name: ${student[name]}"

**5. Boolean (Simulated)**
Bash doesn’t have a real boolean type. Use 0 as true and any non-zero number as false.

    STATUS=0
    if [ $STATUS -eq 0 ]; then
    echo "Success"
    fi

💡 **Final Note**
No need to declare a data type in Bash. Just assign a value to a variable.

Use the right syntax **($(( )), ${#VAR}, declare, etc.)** to treat the variable as the type you need.


## 🧾 Example to Understand:

    NAME="John"       # Treated as a string
    AGE=25            # Still a string, but can be used as a number
    FRUITS=("Apple" "Banana")  # Treated as an array

Even though AGE=25, it’s stored as text. But if you use it in math like $((AGE + 5)), Bash treats it as a number

## Script: Strings and Integers

**File name suggestion: 01_strings_and_integers.sh**

    '#!/bin/bash'  # Tells the system to use Bash to run this script

    # -------- String Variables --------

    ' NAME="John" '       # Assigning a string value to variable NAME
    CITY="Mumbai"     # Another string assigned to CITY

    # -------- Integer Variables --------

    'NUM1=100'         # Storing number 100 in NUM1
    NUM2=200          # Storing number 200 in NUM2

    # -------- Command Substitution --------

    TIMESTAMP=$(date)  # Storing current date & time output from 'date' command in TIMESTAMP
    echo "Script executed at: $TIMESTAMP"  # Printing the timestamp

    # -------- Arithmetic Operation --------

    SUM=$((NUM1 + NUM2))  # Performing integer addition using arithmetic expansion
    echo "Sum of $NUM1 and $NUM2 is: $SUM"  # Printing the result

    # -------- Using String Variables --------

    echo "User Name: $NAME"  # Displaying string variable
    echo "User City: $CITY"  # Displaying string variable

|     Data Type         |  Bash Support?  |           Example Usage             |
| --------------------- | -------------   | ----------------------------------- |
| **String** (default)  | ✅ Yes         | `name="Alice"`                      |
| **Integer**           | ✅ Yes         | `sum=$((10 + 5))`                   |
| **Indexed Array**     | ✅ Yes         | `arr=(one two)`                     |
| **Associative Array** | ✅ Bash 4+     | `declare -A map; map[key]="value"`  |
| **Boolean**           | 🚫 No direct   | Simulated using `0=true`, `1=false` |


**Notes:**

You don’t need to declare types. Bash interprets it based on how you use it.

Arithmetic operations must be done using $(( )).

Arrays and associative arrays are powerful tools to group values.

You can simulate booleans with exit codes (0 success, non-zero = failure).




