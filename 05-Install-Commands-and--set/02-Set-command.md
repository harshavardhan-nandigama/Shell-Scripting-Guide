# Set Command

## What does set -e do? 

- It tells the script to immediately stop execution if any command fails (returns a non-zero exit status).

- This helps you avoid executing any dependent commands after a failure, which is especially useful in automation, deployment scripts, or CI/CD pipelines.

## Example Script: set -e in Action

    #!/bin/bash

This line is called a shebang. It tells the system to use the Bash shell to run this script.

    set -e

It tells the script to immediately stop execution if any command fails (returns a non-zero exit status).

    echo "Hi, Good Morning"

Prints a simple message to the terminal: "Hi, Good Morning"

    echoooooo "Hello, this will be error"

- ⚠️ This is an intentional error. There’s no command called echoooooo.

- Because we used set -e above, the script will immediately stop here.

- The next line will not be executed.

    echo "Hello, Morning"

✅ This line will not run, because the script already stopped due to the previous error (because of set -e).


**Output Preview**

    Hi, Good Morning
    ./script.sh: line 6: echoooooo: command not found

Notice: The script exits immediately after the error. It doesn’t continue to "Hello, Morning".

**Why Use set -e?**

|     Use Case         |                    Benefit                                      |
| -------------------- | --------------------------------------------------------------- |
| Automation           | Prevents broken deployments or configuration if something fails |
| CI/CD Pipelines      | Fails early and clearly on errors                               |
| System Setup Scripts | Stops midway to prevent partial setup                           |
| Secure Scripts       | Avoids running unnecessary commands after an error              |


## Other Useful set Options

|     Flag      |                      Description                           |
| ------------- | ---------------------------------------------------------- |
| `-e`          | Exit immediately if any command fails                      |
| `-x`          | Print each command before running it (used for debugging)  |
| `-u`          | Treat unset variables as an error and exit                 |
| `-o pipefail` | Makes a pipeline fail if any command in the pipeline fails |
