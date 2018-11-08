# PostgreSQL tips

### Fully explain any query
```SQL
EXPLAIN ANALYZE <query>;
```

### Import csv into table
```SQL
COPY table_name(field1, field2, field3, field4) 
FROM '/home/user/project/data/table_name.csv' DELIMITER ',' CSV HEADER;
```
