# Conflicts, merging and rebasing

- **Merge master into Greet Branch**:
    1. Merge the changes from the `master` branch into `greet` branch

    - Switch to the `greet` branch, and merge `master` into `greet`:
        ```bash
        greet checkout greet

        git merge master
        ```
    2. Switch to `master` branch and make the changes to the `hello.sh` file:
        ```bash
        git checkout master

        git add lib/hello.sh
        git commit -m "Update hello.sh file"
        ```

- **Merging Master into Greet Branch (Conflict):** 
    1. Switch to `greet` branch and merge, then commit the changes:
        ```bash
        git checkout greet
        git merge master

        # Output
        Auto-merging lib/hello.sh
        CONFLICT (content): Merge conflict in lib/hello.sh
        Automatic merge failed; fix conflicts and then commit the result.

        # commit the changes
        git commit -m "merge master into greet branch"
        ```

- **Rebasing Greet Branch**:
    - Rebasing is a git tool that is used to move or combine a sequence of commits to a new base commit.
    1. Find the point before the initial merge between master and greet:
        ```bash
        git checkout master

        git log --graph --oneline

        # Copy the commit hash and reset to it

        git reset --hard e3e5149e3ba09c111652144636302f7e9067041f
        ```
    2. Rebase the greet branch on top of the latest changes in the master branch.
        ```bash
        git checkout greet

        git rebase master  #  Replays the commits from the greet branch on top of the latest main branch

        # Output 
        Successfully rebased and updated refs/heads/greet.
        ```

- **Merging Greet into Master**:
    ```bash
    git checkout master

    git merge greet
    ```

- **Understanding Fast-Forwarding and Differences**:
    - Explain fast-forwarding and the difference between merging and rebasing.

    1. **Fast-Forward Merging**:
    - Fast-forwarding occurs when the branch you are trying to merge into has not diverged from the branch you are merging. Is simmilar to updating the target branch to point to the same commit as the source branch without creating any new commits. 

    - No merge commit is created in this case.

    2. **Standard Merging**:
    - Merging combines the changes from two branches and and creates a new commit that has both braches as parents.
    - This is done when both branches have diverged.

    3. **Rebasing**:
    - Rebasing involves moving or combining a sequence of commits to a new base commit.
    - Instead of creating a merge commit, rebasing replays the changes from one branch into another.

    - **Differences Between Merging and Rebasing**
    1. Commit History:

        - Merging preserves the original commit history and adds a merge commit, making it clear where the branches diverged and converged.
        - Rebasing creates a linear commit history by replaying the changes of one branch onto another, which can make the history cleaner and easier to read but loses the context of when branches diverged and merged.

    2. **Commit IDs**:
        - Merging does not change existing commits.
        - Rebasing rewrites the commits on the branch being rebased, creating new commit IDs.

    3. **Conflict Resolution**:
        - Merging might require resolving conflicts at the time of the merge commit.
        - Rebasing requires resolving conflicts as each commit is replayed onto the new base.

    4. Use Cases:

        - Merging is useful for preserving the context of branch creation and integration, especially in a collaborative environment where history transparency is important.
        - Rebasing is useful for cleaning up a feature branch before integrating it into the main branch, making for a linear, cleaner history.
