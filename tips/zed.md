# Zed tips

### Fix activating Python virtual environment on Windows 10/11 PowerShell
```CMD
> zed --version
Zed 0.227.1 9f9b707d39d62468d4cdaed2d8eb95a847da4cf9

# in ~\AppData\Roaming\Zed\settings.json
  "terminal": {
    "shell": {
      "program": "powershell.exe -ExecutionPolicy Bypass",
    },
    "detect_venv": {
      "on": {
        // Default directories to search for virtual environments, relative
        // to the current working directory. We recommend overriding this
        // in your project's settings, rather than globally.
        "directories": [".env", "env", ".venv", "venv"],
        // Can also be `csh`, `fish`, and `nushell`
        "activate_script": "default",
      },
    },
  },
```
