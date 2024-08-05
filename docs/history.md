# History In GIT

- Display the history in the working directory.
    ```bash
    git log
    ```
- **Output**:
    ```bash
    commit 777ce842bcb82c8d5c07361f9adb5f7caf759fab (HEAD -> master)
    Author: danyonyi <denilanyonyi1@gmailc.om>
    Date:   Tue Jul 16 13:02:36 2024 +0300

        Add a variable that contains a default value to be echoed
    ```

- Display One-Line History for a condensed view showing only commit hashes and messages.
    ```bash
    git log --oneline
    ```
- **Output**:
    ```bash
    777ce84 (HEAD -> master) Add a variable that contains a default value to be echoed
    2026a4d Add comments to line 3
    bda72af Update the file hello.sh to include shabang
    dfe8be6 Initial commit, echo the contents 'Hello, World'
    ```

## Controlled Entries

- Display a customized git log, by specifying the number of entries or a time range.
    ```bash
    git log -n 2 --since="5 minutes ago"

## Personalized Format

- Display logs in a personalized format, eg.: ```* e4e3645 2023-06-10 | Added a comment (HEAD -> main) [John Doe]```
    ```bash
    git log --pretty=format:"* %h %as | %s %d [%an]"
    ```
- Output:
    ```bash
    * 777ce84 2024-07-16 | Add a variable that contains a default value to be echoed  (HEAD -> master) [danyonyi]
    ```

