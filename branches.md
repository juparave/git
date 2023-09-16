# git branches

## Rename local branch

```bash
    $ git checkout refactoring
    Switched to branch 'refactoring'
    Your branch is up to date with 'origin/refactoring'.
```

### Set the new name, this will work with local repos

```bash
    $ git branch –m shippers
    fatal: Not a valid object name: 'shippers'.
```

You can't rename a remote git branch like you do with local repositories, this one is connected to a remote `'origin/refactoring'` repo

## Rename a remote branch

There is no way to rename a remote branch, so the steps to do it is by deleting the old repo and create a new one.

### List all branches

```bash
  $ git branch -a
    deploy
    master
  * refactoring
    remotes/origin/HEAD -> origin/master
    remotes/origin/deploy
    remotes/origin/master
    remotes/origin/origin/HEAD
    remotes/origin/origin/deploy
    remotes/origin/origin/master
    remotes/origin/refactoring
```

### Create new branch

    $ git checkout -b shippers

### Push the new branch with the correct name, and reset the upstream branch

    $ git push origin –u shippers

### List all branches

```bash
  $ git branch -a
    deploy
    master
    refactoring
  * shippers
    remotes/origin/HEAD -> origin/master
    remotes/origin/deploy
    remotes/origin/master
    remotes/origin/origin/HEAD
    remotes/origin/origin/deploy
    remotes/origin/origin/master
    remotes/origin/refactoring
    remotes/origin/shippers
```

### Update local repo and set upstream

```bash
    $ git pull --rebase
    $ git branch --set-upstream-to=origin/shippers shippers
```

### Delete local branch

```bash
    $ git branch -d refactoring
    Deleted branch refactoring (was 93acd6fd).
```

### Delete remote branch

    $ git push origin ––delete refactoring

Your local repo may still retain a remote reference that points to the remote
branch you just deleted. This is known as Git’s remote tracking branch.

    $ git branch --delete --remotes origin/refactoring

However, if the branch has already been deleted from the GitHub or BitBucket
server, a simpler approach is to call the git fetch command with the prune
option. The prune option removes any remote tracking branch in your local
repository that points to a remote branch that has been deleted on the server.

    $ git fetch origin --prune

