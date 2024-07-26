# PostgreSQL tips

### Chancge user password in `psql`
```BASH
# psql
postgres=# ALTER USER user_name WITH PASSWORD 'new_password';
ALTER ROLE
```

### Fully explain any query
```SQL
EXPLAIN ANALYZE <query>;
```

### Import csv into table
```SQL
COPY table_name(field1, field2, field3, field4) 
FROM '/home/user/project/data/table_name.csv' DELIMITER ',' CSV HEADER;
```
