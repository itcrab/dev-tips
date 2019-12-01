# Python tips

### Find caller function
```Python
def func_a():
    ...
    import inspect
    print('caller: {}'.format(inspect.stack()[1].function))
    ...


def func_b():
    ...
    func_a()
    ...


func_b()
```

### Copy list with dict inside dict
```Python
>>> bad
>>> lst1 = [{'root': {'sub_root': 123}}]
>>> lst2 = list(lst1)
>>> lst2[0]['root']['sub_root'] = 321
>>> print(lst1)
[{'root': {'sub_root': 321}}]
>>> # good
>>> import copy
>>> lst1 = [{'root': {'sub_root': 123}}]
>>> lst2 = [copy.deepcopy(l) for l in lst1]
>>> lst2[0]['root']['sub_root'] = 321
>>> print(lst1)
[{'root': {'sub_root': 123}}]
```

### Works with money
```Python
>>> # bad
>>> price = 0.01
>>> for _ in range(15):
>>>     price += 0.01
>>>     print(price)
0.02
0.03
0.04
0.05
0.060000000000000005
0.07
0.08
0.09
0.09999999999999999
0.10999999999999999
0.11999999999999998
0.12999999999999998
0.13999999999999999
0.15
0.16
>>> # good
>>> from decimal import Decimal
>>> price = Decimal('0.01')
>>> for _ in range(15):
>>>     price += Decimal('0.01')
>>>     print(price)
0.02
0.03
0.04
0.05
0.06
0.07
0.08
0.09
0.10
0.11
0.12
0.13
0.14
0.15
0.16
```

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
