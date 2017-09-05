# GIT tips

### Delete last commit and changes
```Bash
git reset --hard HEAD~1
git push --force
```

### Edit commits
```Bash
git rebase -i HEAD~3
git push --force
```

### GitHub fork update
```Bash
git remote add upstream https://github.com/user/repo.git
git remote -v
git fetch upstream
git checkout master
git rebase upstream
git push
```

### GitHub fork rebase
```Bash
git checkout master
git rebase branch_name
git push --force
```

### Commit to branch
```Bash
git cherry-pick 18db55bb31d8dffffd94af2f553eb4e982cd9785

# if conflicts
git add -A .
git commit -c 18db55bb31d8dffffd94af2f553eb4e982cd9785
```

### Delete remote tag
```Bash
git push --delete origin tagname
```

### Delete branch
```Bash
# local
git branch -d branch_name

# remote
git push origin --delete branch_name
```

### Switch to tag
```Bash
git tag
git checkout -b version2 v2.0.0
```
