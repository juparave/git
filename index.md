- [hooks](hooks.md)
- [branches](branches.md)
- [troubleshooting](troubleshooting.md)

## git incoming

    $ git fetch && git log ..origin/master

    $ git fetch && git log --pretty=oneline --abbrev-commit --graph ..@{u}

## git outgoing

    $ git fetch && git log origin/master..

    $ git log --pretty=oneline --abbrev-commit --graph @{u}.. --stat

Create alias in ~/.gitconfig

    [alias]
    out = log --pretty=oneline --abbrev-commit --graph @{u}.. --stat
    in = !git fetch && git log --pretty=oneline --abbrev-commit --graph ..@{u}

## git and meld

Add meld command

    $ git config --global alias.meld '!git difftool -t meld --dir-diff'

# Branching

## Create a new branch

Create a new branch

    $ git branch refactoring

Create a new branch and switch to it at the same time

    $ git checkout -b refactoring

## Switching Branches

    $ git checkout refactoring

## Merging

    $ git checkout master
    $ git merge refactoring

## Delete local branch

After the merge and if you no longer need that branch. You can delete it with the -d option to git branch

    $ git branch -d refactoring

## Delete remote branch

To delete a remote branch, you can’t use the git branch command. Instead, use the git push command with --delete flag, followed by the name of the branch you want to delete. You also need to specify the remote name (origin in this case) after git branch.

    $ git push --delete refactoring

## Push new branch

If you want to save the new branch in the repository

    $ git push -u origin refactoring

## git pull branches

    $ git remote update
    $ git pull --all

This assumes all branches are tracked.

If they aren't you can fire this in Bash:

    $ for remote in `git branch -r `; do git branch --track $remote; done

Then run the command.

## link remote branch

    $ git branch --set-upstream-to=origin/deploy deploy

# Plugins

## bash git-prompt

ref: [Bash Git Prompt](https://github.com/magicmonty/bash-git-prompt)

## Discard local changes

    $ git checkout -- .

## Replace local changes from remote

    $ git fetch origin
    $ git reset --hard origin/master

## Undoing the last commit

You can continue to edit the same commit by making amends.

    $ git commit --amend

To undo last commit

    $ git reset --soft HEAD~1

--soft flag: this makes sure that the changes in undone revisions are preserved. After running the command, you'll find the changes as uncommitted local modifications in your working copy.

To undo a commit removing changes

    $ git reflog
    $ git reset --hard #####   <- commit number

## Remove file from tracking

To stop tracking a file you need to remove it from the index. This can be achieved with this command.

    $ git rm --cached <file>

If you want to remove a whole folder, you need to remove all files in it recursively.

    $ git rm -r --cached <folder>

The removal of the file from the head revision will happen on the next commit.

WARNING: While this will not remove the physical file from your local, it will remove the files from other developers machines on next git pull.

## Add your server as a Git remote called 'deploy'

List remotes

    $ git remote -v

git remote add deploy ssh://<your-name>@<your-ip>/srv/git/<your-project>.git/

    $ git remote add deploy ssh://project@prod.server.com/~/app/Project

If nobody is working in that remote non-bare repo, then it should be possible to push to a checked out branch.
But to be more secure in that operation, you now can (with Git 2.3.0, February 2015), do in that remote repo:

    $ git config receive.denyCurrentBranch updateInstead

## Push your code and deploy

## Providing username and password

WARNING: Adding your password to the clone URL will cause Git to store your plaintext password in .git/config. To securely store your password when using HTTP, use a credential helper. For example:

    $ git config --global credential.helper cache
    $ git config --global credential.https://github.com.username foo
    $ git clone https://github.com/foo/repository.git

The above will cause Git to ask for your password once every 15 minutes (by default). See git [help credentials](https://git-scm.com/docs/gitcredentials) for details.

To store credentials in a file

    $ git config --global credential.helper 'store --file ~/.my-credentials'

Also run

    $ git config --global user.email "you@example.com"
    $ git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

## Git branch graphs

    $ git config --global alias.adog "log --all --decorate --oneline --graph"
    $ git adog

## Tagging

Annotated tag

    $ git tag -a v1.0.3 -m "Releasing version v1.0.3"

Publishing tags

    $ git push --tags
