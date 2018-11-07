# Heroku tips

### Rebuild container `myapp`
```Bash
heroku plugins:install heroku-repo
heroku plugins:install heroku-releases-retry
heroku releases:retry --app myapp
```

### Connect to `container-production`
```Bash
heroku run bash -a container-production
```

### Connect to Django shell on `container-production`
```Bash
heroku run python manage.py shell -a container-production
```
