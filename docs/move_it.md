# Move it

- Moving hello.sh:
    - Create the lib directory and move hello.sh file inside it:
        ```bash
        mkdir -p lib
        git mv hello.sh lib/

        # Commit the move
        git commit -m "Move the hello.sh file into the lib/ directory"

        # Output
        9c99220 (HEAD -> master) Move the hello.sh file into the lib/ directory
        ```
    - Create a `Makefile` in the root directory of the repository:
        ```bash
        touch Makefile

        # Write into the file
        echo 'TARGET="lib/hello.sh"\n\nrun:\n\tbash ${TARGET}' > Makefile

        # Commit the changes
        git commit -m "Add a Makefile"

        # Output
        442d459 (HEAD -> master) Add a Makefile
        ```

