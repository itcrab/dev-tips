# Windows 10 Tips

### Set new $PATH value permanently (not only current cmd session)
```CMD
# set user side $PATH
setx path "%path%;C:\path\to\portable\git"

# set system side $PATH
setx /M path "%path%;C:\path\to\portable\git"
```
