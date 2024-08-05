# Branching

- **Create and Switch to New Branch**:
    ```bash
    git checkout -b greet

    touch greeter.sh

    git add greeter.sh
    git commit -m "Add a file greeter.sh"
    ```

- **Update the `lib/hello.sh` file, stage and commit the changes.**
    ```bash
    git add hello.sh
    git commit -m "Update hello.sh file to call greeter.sh"
    ```

- **Update the Makefile and commit the changes.**
    ```bash
    git add Makefile
    git commit -m "Add a comment"
    ```

- Switch back to the `master` branch, compare and show the differences between the `master` and `greet` branches for `Makefile`, `hello.sh`, and `greeter.sh` files.
    ```bash
    git checkout master

    # Makefile comparison
    git diff master greet -- Makefile
    ```
    Output
    ```bash
    diff --git a/Makefile b/Makefile
    index 5adf547..58bb416 100644
    --- a/Makefile
    +++ b/Makefile
    @@ -1,3 +1,4 @@
    +# Ensure it runs the updated lib/hello.sh file
    TARGET="lib/hello.sh"
    
    run:
    ```

    hello.sh comparison
    ```bash
    git diff master greet -- lib/hello.sh
    ```

    Output
    ```bash
    diff --git a/lib/hello.sh b/lib/hello.sh
    index 9bd6cc8..459fa8f 100755
    --- a/lib/hello.sh
    +++ b/lib/hello.sh
    @@ -1,8 +1,11 @@
    #!/bin/bash
    
    -# Default is World
    -# Author: Denil Any 
    -name=${1:-"World"}
    +source lib/greeter.sh
    
    :...skipping...
    diff --git a/lib/hello.sh b/lib/hello.sh
    index 9bd6cc8..459fa8f 100755
    --- a/lib/hello.sh
    +++ b/lib/hello.sh
    @@ -1,8 +1,11 @@
    #!/bin/bash
    
    -# Default is World
    -# Author: Denil Any 
    -name=${1:-"World"}
    +source lib/greeter.sh
    
    -echo "Hello, $name"
    +name="$1"
    +if [ -z "$name" ]; then
    +    name="World"
    +fi
    +
    +Greeter "$name"
    ```

    - Cannot compare greeter.sh file as it does not exist in the master branch

- Generate a `README.md` file for the project with the provided content. Commit this file.
    ```bash
    echo "This is the Hello World example from the git project." > README.md
    ```

- Draw a commit tree diagram illustrating the diverging changes between all branches to demonstrate the branch history.
    ```bash
    git log --graph --oneline --all
    ```
    Output
    ```bash
    * e3e5149 (HEAD -> master) Add README.md file
    | * 7c1624e (greet) Add a comment
    | * ead1af7 Update hello.sh file to call greeter.sh
    | * 934b6a8 Add a file greeter.sh
    |/  
    * 442d459 Add a Makefile
    * 9c99220 Move the hello.sh file into the lib/ directory
    * ce5aa93 Add author information in comments
    | * 3f18dd8 (tag: oops) Revert "Add unwanted comment to hello.sh"
    | | * f6f8645 (refs/stash) WIP on master: 2a46375 Add unwanted comment to hello.sh
    | |/| 
    | | * d020dd9 index on master: 2a46375 Add unwanted comment to hello.sh
    | |/  
    | * 2a46375 Add unwanted comment to hello.sh
    |/  
    * 777ce84 (tag: v1) Add a variable that contains a default value to be echoed
    * 2026a4d (tag: v1-beta) Add comments to line 3
    * bda72af Update the file hello.sh to include shabang
    * dfe8be6 Initial commit, echo the contents 'Hello, World'
    ```    
