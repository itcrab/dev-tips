# MySQL tips

### Fix unstable work on 5$ droplet in [DO](https://www.digitalocean.com/)
```
[mysqld]
performance_schema = off
```

### Copy data from old to new table
```SQL
INSERT INTO new_table SELECT * FROM old_table;
```
