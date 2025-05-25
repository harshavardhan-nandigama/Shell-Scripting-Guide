## What is Shell Scripting ?

Shell Scripting is like handing your computer a checklist. You write a bunch of commands in a text file stuff you’d normally type into the terminal and then run that file like a program. It’s a simple yet powerful way to tell your computer what to do, step by step.

 
**What Does a Shell Script Look Like ?**

     #!/bin/bash

     echo "Hello, this is my first shell script!"

- **#!/bin/bash** tells the system to use the Bash shell. and
- **echo** prints a message to the screen.


## Why Shell Scripts ?

- 1. **Restarting servers automatically.**
- 2. **Creating daily backups.**
- 3. **Installing software with one command.**
- 4. **Analyzing logs and saving the results for later.**
- 5. **These practical applications are what excite me most—I can’t wait to build scripts that solve real problems!**



 ## What is Shebang (#!) in Shell Script ?

 **Shebang** is the first line in a shell script that tells the operating system which interpreter to use to run the script.

      #!/path/to/interpreter '''


Common example for Bash:

     #!/bin/bash


The **#!** is called the shebang.

The **/bin/bash** part tells the OS to run this script using the Bash shell.


## Why Shebang Is Important ?

**Reason**	                                   **Explanation**

- **Interpreter Clarity**          Tells the system which shell (e.g., Bash, Python) to use
- **Script Portability**	          Ensures consistent behavior across systems
- **Avoids Errors**	               Prevents unexpected behavior or command errors

**Example shell script**

     \#!/bin/bash
     echo "Hello, $USER"
