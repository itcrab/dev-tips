# RabbitMQ tips

### Flush all
```Bash
rabbitmqctl stop_app
rabbitmqctl reset
rabbitmqctl start_app
```

### Create administrator user
```Bash
rabbitmqctl add_user user password
rabbitmqctl set_user_tags user administrator
rabbitmqctl set_permissions -p / user ".*" ".*" ".*"
```
