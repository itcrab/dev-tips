# Zed tips

### Run Django tests in Zed tasks
```JSON
  {
    "label": "Run Django Tests in selected dir/file",
    "command": "uv run --env-file=.env manage.py test ($env:ZED_RELATIVE_FILE -replace '\\\\','.' -replace '\\.py$','')",
    //"hide": "on_success", // Keep terminal open on test failures
    "allow_concurrent_runs": true,
    "use_new_terminal": true,
    "shell": {
      "program": "powershell",
    },
  },
  {
    "label": "Run Django Tests in selected test class/method",
    "command": "uv run --env-file=.env manage.py test ($env:ZED_RELATIVE_FILE -replace '\\\\','.' -replace '\\.py$','.$ZED_SYMBOL')",
    //"hide": "on_success", // Keep terminal open on test failures
    "allow_concurrent_runs": true,
    "use_new_terminal": true,
    "shell": {
      "program": "powershell",
    },
  },
```


### Fix activating Python virtual environment on Windows 10/11 PowerShell
```CMD
> zed --version
Zed 1.13.2 5cdb7ab9d9546db683132cfa78e68acec3064cac
```
```JSON
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
