## What Are Special Variables?

In Shell scripting, special variables are predefined variables that hold specific information about the script's execution or arguments. They are automatic variables managed by the shell.

Some commonly used special variables:

| Variable          | Description                                     |
| ----------------- | ----------------------------------------------- |
| `$0`              | Name of the script                              |
| `$1, $2, ..., $9` | Positional parameters (arguments to the script) |
| `$#`              | Number of positional parameters                 |
| `$@`              | All the arguments as separate words             |
| `$*`              | All the arguments as a single word              |
| `$$`              | Process ID of the current shell                 |
| `$?`              | Exit status of the last executed command        |
| `$!`              | Process ID of the last background command       |


## Example Script 01: Special Variables in Action

    #!/bin/bash
    # This is a shell script to demonstrate special variables

    echo "Script name is: $0"
    # $0 gives the name of the script you are executing

    echo "First argument is: $1"
    # $1 is the first argument passed when you run the script

    echo "Second argument is: $2"
    # $2 is the second argument passed to the script

    echo "Total number of arguments: $#"
    # $# shows how many arguments were passed

    echo "All arguments (individually): $@"
    # $@ treats each argument separately (useful in loops)

    echo "All arguments (as a single string): $*"
    # $* treats all arguments as a single string

    echo "Current shell's process ID: $$"
    # $$ prints the process ID of the running script

    echo "Running 'ls' command..."
    ls > /dev/null
    echo "Exit status of 'ls' command: $?"
    # $? gives the exit status of the last command. 0 = success, non-zero = error

    sleep 2 &
    # run 'sleep' in the background for 2 seconds

    echo "PID of the last background command (sleep): $!"
    # $! gives the process ID of the most recent background command

## Output Example

    Script name is: ./special_vars.sh
    First argument is: apple
    Second argument is: banana
    Total number of arguments: 2
    All arguments (individually): apple banana
    All arguments (as a single string): apple banana
    Current shell's process ID: 13456
    Running 'ls' command...
    Exit status of 'ls' command: 0
    PID of the last background command (sleep): 13458
