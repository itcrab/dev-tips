# Heroku tips

### Generate list config vars from app
```JavaScript
let config_items = document.querySelectorAll('.config-var-item')
let config_text = ''
config_items.forEach((item, index) => {
  let config_key = item.querySelector('.config-var-key').value
  let config_value = item.querySelector('.config-var-value').value
  config_text += config_key + ' = ' + config_value + '\n'
})
console.log(config_text)
```

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
