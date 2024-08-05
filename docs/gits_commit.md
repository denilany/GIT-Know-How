# Git commits to commit

- Create a directory named hello and create a file named 'hello.sh'. Add these to the hello.sh file 'echo "Hello, World" 
    ```bash
    mkdir hello && cd hello
    touch hello.sh
    ```

- Initialize a git repository inside the hello directory.
    ```bash
    git init
    ```

- Check the status, stage the changes, and commit the changes.
    ```bash
    git status
    git add hello.sh
    git commit -m "Echo contents inside the hello.sh file"
    ```

- Change the contents of the file hello.sh, stage the changes and commit the changes made.
    ```bash
    git add hello.sh
    git commit -m "Update the hello.sh file"
    ```

- Modify the hello.sh file to include comments and stage it interactively.
    ```bash
    # stage the parts of the file in patches
    git add -p hello.sh
    ```
    - **Output:**
        ```bash
        @@ -1,4 +1,6 @@
        #!/bin/bash
        
        -echo "Hello, $1"
        +# Default is "World"
        +name=${1:-"World"}
        +echo "Hello, $name"
    
        (2/2) Stage this hunk [y,n,q,a,d,K,g,/,e,?]? e
        ```
    Commit after editing the file manually editing the current hunk
    ```bash
    git commit -m "Add comment"
    ```
    ```bash
    # stage the remaining part of the file
    git add hello.sh
    git commit -m "Add line 4 and 5 to include a variable to be echoed out"
    ```
