# ==Starting==:
## version Check
```shell
git --version
```
## config
```sh
git config --global user.name "Depredox"
git config --global user.email "deprecatorp@gmail.com"
```
## initialize the repo
```sh
git init 
```
## to change repo name
```sh
git branch -m "repo_name"
```

# ==Staging==:
## add local files to repo
```sh
git add file_name
```
## add all files to repo
```sh
git add --all
```
## check status
```sh
git status
```
## short status
```sh
git status --short
```

# ==Committing==:
## commit with message
```sh
git commit -m "message"
```
## commiting a file Directly without add
```sh
git commit file_name -m message
```
## view commit history
```sh
git log
```
## add remote repo
```sh
git remote add repo_name repo_url
# lists the remotes locally
git remote -v
# change remote url
git remote set-url origin NewURL
```
## setting up sSH
```sh
git@github.com:username/repo.git
```
## pushing to remote repo (will create branch if it doesn't exist.)
```sh
git push -u repo_name branch_name (first time)
git push (other times)
```
# ==Branch==
##  creating new branch
```sh
git branch branch_name
```
## change branch 
```sh
git checkout branch_name
```
## create a new branch and change to it
```sh
git checkout -b new_branch_name
```
# ==Pull==
## pull a remote branch to update your local repo
```sh
git pull repo_name branch_name
```
## rebase your local repo
```sh
git pull repo_name branch_name --rebase
```
## to show git tags
```sh
git show tag_name
```

```shell
EDITOR=nvim git rebase -i HEAD~N
git show HEAD~N
```