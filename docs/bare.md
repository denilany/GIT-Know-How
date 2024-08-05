# Bare repositories

## What is a bare repository and why is it needed?
- A bare repository is a special type of Git repository that doesn't contain a working directory.

### Why bare repositories are needed:

1. Central repository: Bare repositories are ideal for serving as a central repository that multiple developers push to and pull from. They're designed for sharing, not for direct development work.

2. Efficiency: Without a working directory, bare repositories are more efficient for storage and network transfers, especially important for large projects or servers handling many repositories.

3. Preventing conflicts: Since there's no working directory, there's no risk of conflicts between the repository state and a working copy, which could happen if someone tried to push to a non-bare repository with a working directory.

4. Server-side hooks: Bare repositories are often used on servers to implement pre-receive and post-receive hooks for things like continuous integration, deployment, or notifications.

5. Git hosting services: Services like GitHub, GitLab, and Bitbucket use bare repositories on their servers to store your projects.

6. Local remotes: When you want to use a local repository as a remote for another local repository (like in some of our earlier exercises), it's best practice to use a bare repository.

## Creating a bare repository
- Create a bare repository named `hello.git` from the existing `hello` repository.

    ```bash
    # switch to the parent directory of the hello repo
    cd work/

    # create a bare repo
    git clone --bare hello hello.git

    # output
    Cloning into bare repository 'hello.git'...
    done.
    ```
- Add the bare `hello.git` repository as a remote to the original repository `hello`.
    ```bash
    cd hello

    git remote add origin ../hello.git
    ```

