# Python tips

### Mock "name" attribute in MagicMock object
```Python
>>> from unittest.mock import MagicMock
>>> mock_obj = MagicMock(id='123', name='test')
>>> mock_obj.id
'123'
>>> mock_obj.name  # WTF???
<MagicMock name='test.name' id='1517971199760'>
>>> # fix
>>> mock_obj.name = 'test'
>>> mock_obj.id
'123'
>>> mock_obj.name
'test'
```

### Parse ISO 8601 string to datetime object without any third-party libs
```Python
from datetime import datetime

date_string = '2018-06-24T16:20:03+05:00'
date_string = '{}{}'.format(date_string[:-3], date_string[-2:])  # delete ":" in timezone
date_object = datetime.strptime(date_string, '%Y-%m-%dT%H:%M:%S%z')
print('{}: {}'.format(type(date_object), date_object))
print('Year: {}, month: {}, day: {}, hour: {}, minutes: {}, seconds: {}, tzinfo: {}'.format(
    date_object.year, date_object.month, date_object.day,
    date_object.hour, date_object.minute, date_object.second,
    date_object.tzinfo
))
```

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
