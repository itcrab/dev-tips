# RabbitMQ tips

### Flush all
```Bash
rabbitmqctl stop_app
rabbitmqctl reset
rabbitmqctl start_app
```

### Enable UI
```Bash
export ERLANG_HOME=/path/to/erlang
rabbitmq-plugins enable rabbitmq_management
# http://localhost:15672/
```

### Create administrator user
```Bash
rabbitmqctl add_user user password
rabbitmqctl set_user_tags user administrator
rabbitmqctl set_permissions -p / user ".*" ".*" ".*"
```
