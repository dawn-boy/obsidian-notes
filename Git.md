# ==Starting==:
## version Check
```git
git --version
```
## config
```git
git config --global user.name "Depredox"
git config --global user.email "deprecatorp@gmail.com"
```
## initialize the repo
```git
git init 
```
## to change repo name
```git
git branch -m "repo_name"
```

# ==Staging==:
## add local files to repo
```git
git add file_name
```
## add all files to repo
```git
git add --all
```
## check status
```git
git status
```
## short status
```git
git status --short
```

# ==Committing==:
## commit with message
```git
git commit -m "message"
```
## commiting a file Directly without add
```git
git commit file_name -m message
```
## view commit history
```git
git log
```
## add remote repo
```git
git remote add repo_name repo_url
```
## pushing to remote repo (will create branch if it doesn't exist.)
```git
git push -u repo_name branch_name (first time)
git push (other times)
```
# ==Branch==
##  creating new branch
```git
git branch branch_name
```
## change branch 
```git
git checkout branch_name
```
## create a new branch and change to it
```git
git checkout -b new_branch_name
```