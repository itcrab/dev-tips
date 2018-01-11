# RabbitMQ tips

### Create administrator user
```Bash
rabbitmqctl add_user user password
rabbitmqctl set_user_tags user administrator
rabbitmqctl set_permissions -p / user ".*" ".*" ".*"
```
