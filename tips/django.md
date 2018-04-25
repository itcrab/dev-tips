# Django tips

### Get list relations (o2o, m2o, m2m) in model
```Python
from app_name.models import Order
[field for field in Order._meta.get_fields(include_hidden=True) if field.auto_created and not field.concrete]
```

### DRF disable authorization only in current view
```Python
class OrderCreateView(CreateAPIView):
    authentication_classes = []
    permission_classes = []
```

### SQL-queries count
```Python
from django.db import connection
start_count = len(connection.queries)
...
end_count = len(connection.queries)
print('sql-queries count is: {}'.format(end_count - start_count))
```

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

### Revert and re-run all migrations for application
```Bash
python manage.py migrate app_name zero
python manage.py migrate app_name
```

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

### Django-filter: BooleanFilter not working with annotated fields in Django-REST-Framework
```Python
class OrderFilter(django_filters.FilterSet):
    # if you have annotated field(s) - you must declare all BooleanFields in FilterSet
    # is_active is BooleanField in model and custom_field is BooleanField in annotated fields

    # is_active = django_filters.BooleanFilter(name='is_active')  # not working
    is_active = django_filters.rest_framework.BooleanFilter(name='is_active')  # normal behavior

    # custom_field = django_filters.BooleanFilter(method='filter_custom_field')  # not working
    custom_field = django_filters.rest_framework.BooleanFilter(method='filter_custom_field')  # for more power

    class Meta:
        model = Order
        fields = ['title', 'status', 'is_active', 'custom_field']

    def filter_custom_field(self, queryset, name, value):
        lookup = {name: value}
        return queryset.filter(**lookup)

class OrderListViewSet(ListAPIView):
    serializer_class = OrderSerializer
    filter_backends = (DjangoFilterBackend, OrderingFilter,)
    filter_class = OrderFilter
    ...
    
    def get_queryset(self):
        return Order.objects.annotate(custom_field=...).all()  # custom_field is BooleanField
```
