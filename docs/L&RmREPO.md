# Local and remote repositories

1. In the `work/` directory, make a clone of the repository `hello` as `cloned_hello`. (Do not use copy command)

    ```bash
    # Move into work dir/
    cd work/

    # clone the hello repo
    git clone hello cloned_hello
    ```

2. Show the logs for the cloned repository.
    ```bash
    cd cloned_hello

    git log --oneline
    ```

3. Display the name of the remote repository and provide more information about it.
    ```bash
    # Display the name of the remote repository
    git remote

    # output
    origin

    # More information about the repo.
    git remote -v

    # output
    origin  /home/danyonyi/work/hello (fetch)
    origin  /home/danyonyi/work/hello (push)

    # Alternatively
    git remote show origin

    # output
    * remote origin
    Fetch URL: /home/danyonyi/work/hello
    Push  URL: /home/danyonyi/work/hello
    HEAD branch: master
    Remote branches:
        greet  tracked
        master tracked
    Local branch configured for 'git pull':
        master merges with remote master
    Local ref configured for 'git push':
        master pushes to master (up to date)
    ```
    - This information helps in understanding how the local repository is connected to remote repository and how they're configured to ineract with each other.

4. List all remote and local branches in the `cloned_hello` repository.
    ```bash
    # list remote branches only
    git branch
     
    # output
    * master

    # list remote branches only 
    git branch -r

    # output
    origin/HEAD -> origin/master
    origin/greet
    origin/master
    
    # List all branches
    git branch -a

    # output
    * master
    remotes/origin/HEAD -> origin/master
    remotes/origin/greet
    remotes/origin/master
    ```

5. Make changes to the original repository, update the README.md file with the provided content, and commit the changes.
    ```bash
    cd hello/

    # Change README.md

    git add README.md 
    git commit -m "Update README.md file"
    ```

6. Inside the cloned repository `(cloned_hello)`, fetch the changes from the remote repository and display the logs. Ensure that commits from the `hello` repository are included in the logs.
    ```bash
    cd cloned_hello/

    git fetch origin

    # show logs
    git log --all --oneline --graph

    # output
    * b083def (origin/master, origin/HEAD) Update README.md file
    * 18a814e (HEAD -> master, origin/greet) Update hello.sh file
    * e3e5149 Add README.md file
        .
        .
        .
    ```

7. Merge the changes from the remote `master` branch into the local `master` branch.
    ```bash
    # ensure to be in the local master branch
    git checkout master

    # Merge the changes
    git merge origin/master
    ```

8. Add a local branch named `greet` tracking the remote `origin/greet` branch.
    ```bash
    git branch greet
    ```
9. Add a `remote` to your Git repository and push the `master` and `greet` branches to the `remote`.
    ```bash
    git remote add remote /home/danyonyi/work/hello

    # show all remote repositories
    git remote

    # output
    origin
    remote

    # push master and greet branches
    git push -u remote master
    git push -u remote greet
    ```
