# Python tips

### Set logging level
```Python
import logging
logging.basicConfig(level=logging.INFO)
```

### pip install from GitHub
```Bash
pip install -e git://github.com/{user}/{repo}.git@{tag}#egg={package}
```

### Create python package on PyPI
```Bash
pip install twine
python setup.py sdist
twine upload dist/*
```

### Run tests
```Bash
# Run py.test tests
py.test

# if your tests in "tests" directory (fix imports)
python -m pytest tests/
```

### Unittest show full text in asserts
```Python
import unittest
unittest.util._MAX_LENGTH=4096
```

### Recurson depth
```Python
# RecursionError: maximum recursion depth exceeded in comparison
import sys
sys.setrecursionlimit(2000)
```

### HTTP server (Python 3)
```Bash
python -m http.server --cgi 8000
```

### SMTP server (Python 3)
```Bash
python -m smtpd -n -c DebuggingServer localhost:25
```
