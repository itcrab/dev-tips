# PowerShell tips

### First install PowerShell Installer script (like `pyenv-win`)
```PowerShell
> Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"
    + CategoryInfo          : SecurityError: (:) [], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess
...
> # fix - set execution policy
> Get-ExecutionPolicy
    Restricted
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
    [y]
> Get-ExecutionPolicy
    RemoteSigned
> # now we can install `pyenv-win` :)
```


### Count time running application (like `time` in NIX)
```PowerShell
Measure-Command { python script.py }
```
