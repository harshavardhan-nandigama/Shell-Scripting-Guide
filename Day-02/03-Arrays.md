## Arrays 

Arrays in Bash allow you to store multiple values (like a list). This is useful when dealing with multiple inputs like filenames, movie names, user data, etc.

## Example Script: 01-array-example.sh

`#!/bin/bash`

🔹 Shebang line: This tells the system to run the script using the bash shell.

`MOVIES=("Court" "HIT3" "PUSHPA2" "Thandel")`

Array declaration:
We are creating an array named MOVIES that contains four movie names.

Indexing starts from 0.

MOVIES[0] = "Court", MOVIES[1] = "HIT3", and so on.

`echo "First Movie: ${MOVIES[0]}"`

Accesses and prints the first movie in the array → Court


`echo "Fourth Movie: ${MOVIES[3]}"`

Accesses and prints the fourth movie (index 3) → Thandel


`echo "Invalid Index: ${MOVIES[4]}"`

⚠️ This tries to access index 4 which does not exist, so this will return an empty string.


`echo "All Movies: ${MOVIES[@]}"`

${MOVIES[@]} expands to all elements in the array → Court HIT3 PUSHPA2 Thandel

