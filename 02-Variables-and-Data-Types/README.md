## Shell Scripting – Day 2: Core Concepts

Learn the basics of Shell Scripting with real examples.  
Day 2 covers:

✅ Variables  
✅ Special Variables  
✅ Arrays  
✅ Data Types


## 1️⃣ Variables

**Used to store values.**

    name="Alice"
    echo "Hello, $name"

No spaces around =, use $ to access.

## 2️⃣ Special Variables

**Built-in variables for script handling.**

    Variable	Description
    $0	Script name
    $1	First argument
    $@	All arguments
    $#	Number of arguments
    $$	Script PID
    $?	Last command status

    echo "Script: $0, Arg1: $1, Total Args: $#"

## 3️⃣ Arrays

**Store multiple values.**

    fruits=("apple" "banana" "cherry")
    echo "First: ${fruits[0]}"
    echo "All: ${fruits[@]}"

**Loop:**

    for fruit in "${fruits[@]}"; do
    echo "$fruit"
    done

## 4️⃣ Data Types

**Shell treats all values as strings by default.**

    name="Linux"
    age=25
    sum=$((age + 5))
    echo "New age: $sum"

Use (( )) for arithmetic.
