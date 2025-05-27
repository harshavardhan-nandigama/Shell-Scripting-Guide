# 📅 Day 02 - Variables and Data Types

**📘 Learnings Covered - Day 2: Variables and Data Types**

| # |      Topic        |                        Description                               |
| - | ----------------- | ---------------------------------------------------------------- |
| 1 | Variables         | Defining and using variables in scripts                          |
| 2 | Data Types        | Using integers, strings, and understanding how Bash handles them |
| 3 | Arrays            | Working with indexed arrays in Bash                              |
| 4 | Special Variables | Using `$0`, `$1`, `$#`, `$?`, `$@`, and `$*` effectively         |


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
