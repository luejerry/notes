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

### Origin
`git pull`

### Upstream
`git pull upstream master`

## Commit to repository

### Origin
`git push origin master`

### Upstream
`git push upstream master`

## Commit all changes
~~~~
git add .
git commit -m "Commit message"
~~~~
