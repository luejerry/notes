# Notes on Git

## Setup

### Set identity

~~~~
git config [--global] user.email "user@email.com"
git config [--global] user.name "Name"
~~~~

### Download repository
`git clone https://repository.git`

### View remote repositories
`git remote -v`

### Add upstream repository
`git remote add upstream https://repository.git`

## Updating
### Without review
* origin: `git pull`
* upstream: `git pull upstream master`

### With review
~~~~
git fetch origin master
git log ..origin/master
git merge origin/master
~~~~

## Committing

### Commit all changes to local
~~~~
git add .
git commit -m "Commit message"
~~~~

### Commit to remote repository
* origin: `git push origin master`
* upstream: `git push upstream master`


## Branch operations

### View available branches
* local: `git branch`
* remote: `git branch -r`
* upstream: `git remote show upstream`

### Delete branches
* local: `git branch -d branch-name`
* remote: `git branch -r -d branch-name`

### Create new branch
`git checkout -b branch-name`


## Reverting
### Discard uncommitted changes
`git reset --hard`
or
`git checkout -p`

### Revert to previous commit
`git reset --hard <commit>`

`<commit>` can be part of a commit hash, or `HEAD~1` for previous commit.

## Untrack repository files
~~~
git rm -r --cached <filename>
git add -u
~~~
Commit, pull, then push to remote.
