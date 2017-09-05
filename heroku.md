# Heroku tips

### Connect to `container-production`
```Bash
heroku run bash -a container-production
```

### Connect to Django shell on `container-production`
```Bash
heroku run python manage.py shell -a container-production
```
