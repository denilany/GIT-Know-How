# Check it out
1. **Restore First Snapshot:**
    - Revert the working tree to its initial state.
    1. *Find the initial commit* (initial commit hash)
        ```bash
        git rev-list --max-parents=0 HEAD
        ```
    - **Output**: 
        ```bash
        dfe8be684932dc07b52ed95a9b3b7e258ac82053
        ```
    2. *Reset the initial commit*
        ```bash
        git checkout dfe8be684932dc07b52ed95a9b3b7e258ac82053
        ```
    - **Output**:
        ```bash
        HEAD is now at dfe8be6 Initial commit, echo the contents 'Hello, World'
        ``` 
    3. Contents of hello.sh file:
        ```bash
        cat hello.sh
        echo "Hello, World"
        ```
    - ### **Alternative**:
        ```bash
        git log --reverse --oneline | head -1 | cut -d' ' -f1 | xargs git checkout
        cat hello.sh
        ```
    - **Explanation**:
        - `git log --reverse --oneline`: Lists commits in reverse order (oldest first)
        - `head -1`: Takes the first (oldest) commit
        - `cut -d' ' -f1`: Extracts the commit hash
        - `xargs git checkout`: Checks out that commit
        - 

2. **Restore Second Recent Snapshot:** 
    ```bash
    git checkout HEAD@{1}
    cat hello.sh
    ```
    - `git checkout HEAD@{1}`: Moves to the parent of the current commit


3. **Return to Latest Version:**
    - Ensure that the working directory reflects the latest version of the hello.sh file present in the main branch, without referring to specific commit hashes.
        ```bash
        git checkout master
        cat hello.sh
        ```
