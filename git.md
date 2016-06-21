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
* origin: `git pull`
* upstream: `git pull upstream master`

## Commit to repository
* origin: `git push origin master`
* upstream: `git push upstream master`

## Commit all changes
~~~~
git add .
git commit -m "Commit message"
~~~~
