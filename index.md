

## git incoming

    $ git fetch && git log ..origin/master

## git outgoing

    $ git fetch && git log origin/master..

# Plugins

## bash git-prompt

ref: https://github.com/magicmonty/bash-git-prompt


## Discard local changes

    $ git checkout -- .

## Replace local changes from remote

    $ git fetch origin
    $ git reset --hard origin/master

