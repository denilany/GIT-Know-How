# Changed your mind?

- **Reverting Changes**: Revert to the previous version before statging it.
    ```bash
    git restore hello.sh
    ```

- **Staging and Cleaning**: Introduce unwanted changes to the file, stage them, then clean the staging area to discard the changes.

    ```bash
    git add hello.sh
    git status

    # Output
    On branch master
    Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
            modified:   hello.sh

    git restore --staged hello.sh
    git restore hello.sh
    ```  

- **Committing and Reverting**: Add the following unwanted changes again, stage the file, commit the changes, then revert them back to their original state.
    ```bash
    git add hello.sh
    git commit -m "Add unwanted changes"
    git revert HEAD
    ```
    
- **Tagging and Removing Commits**: Tag the latest commit with oops, then remove commits made after the v1 version. Ensure that the HEAD points to v1.
    ```bash
    git tag oops
    git reset --hard v1
    git log --oneline
    ```
    - **Output**:
        ```bash
        777ce84 (HEAD -> master, tag: v1) Add a variable that contains a default value to be echoed
        2026a4d (tag: v1-beta) Add comments to line 3
        bda72af Update the file hello.sh to include shabang
        dfe8be6 Initial commit, echo the contents 'Hello, World'    
        ```

- **Displaying Logs with Deleted Commits**: Show the logs with the deleted commits displayed, particularly focusing on the commit tagged oops.
    ```bash
    git reflog

    # output
    3f18dd8 (tag: oops) HEAD@{1}: revert: Revert "Add unwanted comment to hello.sh"
    ```
    
    ```bash
    git show oops
    
     # output
     commit 3f18dd83a77fd2875f45395b73994fac99458b4c (tag: oops)
     Author: danyonyi <denilanyonyi1@gmail.qcom>
     Date:   Wed Jul 17 09:28:46 2024 +0300
     ```

- **Cleaning Unreferenced Commits**:  Ensure that unreferenced commits are deleted from the history, meaning there should be no logs for these deleted commits.

    **Perform Garbage Collection** to force Git to delete unreachable objects immediately.
    ```bash
    # Git garbage collection
    git gc --prune=now

    # expire all reflog entries immediately
    git reflog expire --expire=now --all
    ```

- **Author Information**: Add an author comment to the file and commit the changes.
    - Include the comment with the author name, stage and commit it.
        ```bash
        git add hello.sh
        git commit -m "Add author information in comments"

        # Output
        51b9180 (HEAD -> master) Add author information in comments
        ```

- Ammend changes made later to the previous commit message:

    Update the file to include the email without making a new commit, but include the change in the last commit.
    - First include the email into the fil and stage the changes:
        ```bash
        git add hello.sh
        ```
    - Amend the last commit to include the changes without creating a new commit:
        ```bash
        git commit --amend --no-edit

        # Output
        ce5aa93 (HEAD -> master) Add author information in comments

        # "--no-edit" option preserves the original commit message
        ```
