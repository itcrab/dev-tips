# Python tips


### Install `pip` in new venv created by `uv venv` (clear and blank venv):
```Bash
# tested on Python 3.11
python -m ensurepip --upgrade
```

### Convert `\uXXXX` strings to plain text (example for Arabic):
```Python
>>> s = "\\u062d\\u0642\\u0644 \\u0627\\u0644\\u0645\\u0646\\u062a\\u062c\\u0627\\u062a \\u0645\\u0637\\u0644\\u0648\\u0628."
>>> result = s.encode('latin-1').decode('unicode-escape')
>>> result
'حقل المنتجات مطلوب.'
```


### Find all combinations
```Python
>>> import itertools
>>> for var in itertools.product([0, 1], repeat=4):
>>>     print(var)
(0, 0, 0, 0)
(0, 0, 0, 1)
(0, 0, 1, 0)
(0, 0, 1, 1)
(0, 1, 0, 0)
(0, 1, 0, 1)
(0, 1, 1, 0)
(0, 1, 1, 1)
(1, 0, 0, 0)
(1, 0, 0, 1)
(1, 0, 1, 0)
(1, 0, 1, 1)
(1, 1, 0, 0)
(1, 1, 0, 1)
(1, 1, 1, 0)
(1, 1, 1, 1)
```


### Fix cross-imports problem in type-hinting Python feature
```Python
from typing import TYPE_CHECKING
if TYPE_CHECKING:
    from order.models import PackageOrder  # cross-import problem
...

class PackagesLogic:
    def __init__(self, packages: list[Package], order: 'PackageOrder', ...):
        ...
```

### Access from decorator to self-class attributes
```Python
def decorator(f):
    @wraps(f)
    def wrapper(*args, **kwargs):
        user = args[0].user
        ...
        return f(*args, **kwargs)
    return wrapper
```

### Dict to Object
```Python
>>> from collections import namedtuple
>>> d = dict(name='Test', age=123)
>>> o = namedtuple('DictObject', d.keys())(*d.values())
>>> print(d)
{'name': 'Test', 'age': 123}
>>> print(o)
DictObject(name='Test', age=123)
>>> print(o.name)
Test
>>> print(o.age)
123
```

### Paste code in Python interpreter with some blank lines and tabulations
```Python
>>> %cpaste
def test_func(opt, grep):
    if opt in grep:
        return 'Super!'

    return 'Oops...'

--

```

### Logging execution result function
```Python
def log_exec(func):
    def wrapper(*args, **kwargs):
        resp = func(*args, **kwargs)
        print(f'{func}: {resp}')
        return resp
    return wrapper
...
@log_exec
def calc_discount(order, user):
    ...
    return discount
```

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
