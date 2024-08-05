# blobs, trees and commits

- **Exploring** `.git/` **Directory**: 
    - *HEAD* : Is a symbolic reference to the `refs/heads/` namespace that indicates the present active branch.
        ```bash
        cat .git/HEAD

        ref: refs/heads/master
        ```
    - *refs/* : This directory contains the references to commits in branches and tags. It includes subdirectories such as `heads/` and `tags`.
        ```bash
        ls .git/refs/
        
        heads  tags
        ```
        The refs/heads/ directory contains the branches in the git repository.

    - *config* : This file contains configuration settings for the repository including user information, remote repository URL, and other settings. It contains the following contents and more can be included:
        ```bash
        cat .git/config

        [core]
                repositoryformatversion = 0
                filemode = true
                bare = false
                logallrefupdates = true
        ```
    
    - *objects/* : This directory contains all the objects (blobs, tree, commits) that make up the content of the repository. Objects are stored in subdirectories named after the first two characters of their hash.
        ```bash
        ls .git/objects/

        28  44  51  5a  9b  9c  c0  ce  fc  info  pack
        ```

- **Latest Object Hash**: Finding the latest object hash within the `.git/objects/` directory using Git commands.
    - To find the latest object hash, use the `git rev-parse` command to get the hash of the latest commit:
        ```bash
        # Inside the hello/ repository 
        LATEST_COMMIT_HASH=$(git rev-parse HEAD)
        echo "Latest commit hash: $LATEST_COMMIT_HASH"

        # Output
        Latest commit hash: 442d459714ed2ad697a03092ed34452935717900
        ```
    
    - Printing the Type and Content of the Latest Object
        ```bash
        cd ..  # Move out of the .git repository
        git cat-file -t $LATEST_COMMIT_HASH  # Print the type of the latest commit object

        # Output
        commit

        git cat-file -p $LATEST_COMMIT_HASH  # Print the content of the latest commit object

        # Output
        tree c0fa51938fdc4c42759b65a2e1faac89981d6e48
        parent 9c99220752d1078620baa253f173478c1c7a9ad2
        author danyonyi <denilanyonyi1@gmail.com> 1721461026 +0300
        committer danyonyi <denilanyonyi1@gmail.com> 1721461026 +0300

        Add a Makefile
        ```
    
- **Dumping Directory Tree**:
    1. To dump the directory tree referenced by the commit, find the tree hash from the commit object:
        ```bash
        TREE_HASH=$(git cat-file -p $LATEST_COMMIT_HASH | grep 'tree' | cut -d' ' -f2)
        echo "Tree hash: $TREE_HASH"

        # Output
        Tree hash: c0fa51938fdc4c42759b65a2e1faac89981d6e48
        ```
    - Dump the directory tree using the tree hash:
        ```bash
        git cat-file -p $TREE_HASH

        # Output
        100644 blob 5adf5479045f8787fa746687c43b311773fad503    Makefile
        040000 tree 2835e139e8e79677faf4f5c833f0185cf69a9a3a    lib
        ```

    2. To dump the contents of the `lib/` directory and `hello.sh` file:
    - Find the tree hash for the `lib/` directory:
        ```bash
        LIB_TREE_HASH=$(git cat-file -p $TREE_HASH | grep 'lib' | cut -d' ' -f3)
        echo "lib/ directory tree hash: $LIB_TREE_HASH"

        # Output
        lib/ directory tree hash: 2835e139e8e79677faf4f5c833f0185cf69a9a3a      lib

        git cat-file -p $LIB_TREE_HASH
        ```
    - Find the blob hash for the `hello.sh` file:
        ```bash
        HELLO_BLOB_HASH=$(git cat-file -p $LIB_TREE_HASH | grep 'hello.sh' | cut -d' ' -f3)
        echo "hello.sh file blob hash: $HELLO_BLOB_HASH"

        git cat-file -p $HELLO_BLOB_HASH
        ```

