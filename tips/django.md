# Django tips

### Move models from `app` to `newapp`
- move models from `app` to `newapp` (in `models.py`)
- fix all imports everywhere (find and fix imports in `*.py`)
- run `python manage.py makemigrations`
- in `app` find new migration and fix it to some example:
```Python
# 0005_auto_20170906_0029
class Migration(migrations.Migration):

    dependencies = []

    database_operations = [
        migrations.AlterModelTable('OrderModel', 'newapp_ordermodel')
    ]

    state_operations = [
        migrations.DeleteModel('OrderModel')
    ]

    operations = [
        migrations.SeparateDatabaseAndState(
            database_operations=database_operations,
            state_operations=state_operations)
    ]
```
- in `newapp` find new migration and fix it to some example:
```Python
class Migration(migrations.Migration):

    dependencies = [
        ('app', '0005_auto_20170906_0029'),
        ...
    ]

    state_operations = [  # just replace `operations`
        migrations.CreateModel(
            name='OrderModel',
            fields=[
                ...
            ],
            ...
        ),
    ]

    operations = [
        migrations.SeparateDatabaseAndState(state_operations=state_operations)
    ]
```
- final step - run `python manage.py migrate`
- enjoy!

### Fake single migration (migration is `0003_auto_20170905_1236`)
```Bash
python manage.py migrate --fake app_name 0003
```

### Run raw SQL
```Python
from django.db import connection

with connection.cursor() as cursor:
    cursor.execute("DROP TABLE table_name")
```

### Dump and load data
```Bash
python manage.py dumpdata -e contenttypes --indent=4 >data.json
python manage.py loaddata data.json
```

### Run tests and use exists database
```Bash
python manage.py test application --keepdb
```

### Clear cache (run in Django shell)
```Python
from django.core.cache import cache; cache.clear()
```
