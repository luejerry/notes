# Notes on Git

## Set identity

~~~~
git config [--global] user.email "user@email.com"
git config [--global] user.name "Name"
~~~~

## Download repository
`git clone https://repository.git`

## View remote repositories
`git remote -v`

## Add upstream repository
`git remote add upstream https://repository.git`

## Update from repository
### Without review
* origin: `git pull`
* upstream: `git pull upstream master`

### With review
~~~~
git fetch origin master
git log ..origin/master
git merge origin/master
~~~~

## Commit to repository
* origin: `git push origin master`
* upstream: `git push upstream master`

## Commit all changes
~~~~
git add .
git commit -m "Commit message"
~~~~

## View available branches
* local: `git branch`
* remote: `git branch -r`

## Delete branches
* local: `git branch -d branch-name`
* remote: `git branch -r -d branch-name`

## Create new brach
`git checkout -b branch-name`

