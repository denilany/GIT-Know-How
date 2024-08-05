# TAG me

- **Tag the Current Version** of the repo as v1:
    ```bash
    git tag v1
    ```
    - **Output**:
        ```bash
        777ce84 (HEAD -> master, tag: v1) HEAD@{0}: reset: moving to 777ce842bcb82c8d5c07361f9adb5f7caf759fab
        ```

- **Tag the Previous Version** as v1-beta, without relying on commit hashes to navigate through the history.
    ```bash
    git reflog
    git tag v1-beta HEAD@{1}
    git reflog
    ```
    - **Output**:
        ```bash    
        2026a4d (tag: v1-beta) HEAD@{1}: reset: moving to master
        ```

- **Navigating Tagged Versions**: Move back and forth between the two tagged versions, v1 and v1-beta
    1. Move to v1
        ```bash
        git checkout v1
        ```
    - **Output**:
        ```
        HEAD is now at 777ce84 Add a variable that contains a default value to be echoed
        ```

    2. Move to v1-beta
        ```bash
        git checkout v1-beta
        ```
    - **Output**:
        ```
        Previous HEAD position was 777ce84 Add a variable that contains a default value to be echoed
        HEAD is now at 2026a4d Add comments to line 3
        ```

- **Listing Tags**: Display a list of all tags present in the repository.
    ```bash
    git tag
    ```
    - **Output**:
        ```bash
        v1
        v1-beta
        ```

