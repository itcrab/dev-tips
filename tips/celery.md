# Celery tips

### Celery task is not starting
```Python
>>> task_name.delay()
PreconditionFailed: Queue.declare: (406) PRECONDITION_FAILED - inequivalent arg 'x-max-priority' for queue 'queue_name' in vhost 'vhost_name': received the value '7' of type 'signedint' but current is none
# fix is simple - you must delete 'queue_name' queue (for recreating with new settings)
```

### Celery run
```Bash
celery -A app_name worker --loglevel=info
```
