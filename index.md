

## git incoming

    $ git fetch && git log ..origin/master

## git outgoing

    $ git fetch && git log origin/master..

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

ref: https://github.com/magicmonty/bash-git-prompt


## Discard local changes

    $ git checkout -- .

## Replace local changes from remote

    $ git fetch origin
    $ git reset --hard origin/master

## Undoing the last commit

You can continue to edit the same commit by making amends.

    $ git commit --amend

To undo a commit

    $ git reflog
    $ git reset --hard #####   <- commit number
    
## Add your server as a Git remote called 'deploy'

List remotes

    $ git remote -v

git remote add deploy ssh://<your-name>@<your-ip>/srv/git/<your-project>.git/
    
    $ git remote add deploy ssh://project@prod.server.com/~/app/Project
    
## Push your code and deploy

    $ git push deploy master

## Providing username and password

WARNING: Adding your password to the clone URL will cause Git to store your plaintext password in .git/config. To securely store your password when using HTTP, use a credential helper. For example:

    $ git config --global credential.helper cache
    $ git config --global credential.https://github.com.username foo
    $ git clone https://github.com/foo/repository.git
    
The above will cause Git to ask for your password once every 15 minutes (by default). See git [help credentials](https://git-scm.com/docs/gitcredentials) for details.

## Git branch graphs

    $ git config --global alias.adog "log --all --decorate --oneline --graph"
    $ git adog
