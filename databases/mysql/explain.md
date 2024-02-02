# Explain

It will show you how many rows MySQL is actually checking:

```mysql
EXPLAIN SELECT * FROM table;
```

|Column|JSON Name|Meaning|
|---|---|---|
|id|select_id|The SELECT identifier|
|select_type|None|The SELECT type|
|table|table_name|The table for the output row|
|partitions|partitions|The matching partitions|
|type|access_type|The join type|
|possible_keys|possible_keys|The possible indexes to choose|
|key|key|The index actually chosen|
|key_len|key_length|The length of the chosen key|
|ref|ref|The columns compared to the index|
|rows|rows|Estimate of rows to be examined|
|filtered|filtered|Percentage of rows filtered by table condition|
|Extra|None|Additional information|

[Explain Output](https://dev.mysql.com/doc/refman/5.7/en/explain-output.html)

Consider using multiple queries over 1 big query. It might not be the case that the 1 big query is better.

For example, a query with 3 joins might not be quicker than running the 3 joins separately. Unless there is a huge difference between the costs, go for the single query as you have to consider network traffic and other considerations. Use the following command directly after a query to get the query cost. 

```mysql
SELECT * FROM feedback;  
SHOW STATUS LIKE 'Last_Query_Cost'; 
```

```mysql
EXPLAIN EXTENDED SELECT *  
FROM film f  
INNER JOIN film_actor fa ON f.film_id fa.film_id;
```

Optimising aggregate functions such as MIN and MAX

There are 2 methods of getting the MIN film_id from this table:

```mysql
EXPLAIN SELECT MIN(film_id)  
FROM film  
WHERE length < 100;
```

In this demo, this scans 1000 rows to get the result.

and 

```mysql
EXPLAIN SELECT film_id  
FROM film  
WHERE length < 100  
ORDER BY film_id  
LIMIT 1; 
```

In this demo, it scans 1 row to get the result.  

Tip: Use indexing on columns that you are using aggregation on.

## Tips:

- You can use `EXPLAIN` keywords to check the execution plan of a query
- Avoid using `<>` operator in query as it ignores index created on table
- Use `UNION ALL` instead of `UNION` if you do not care about duplicate data
- Always test your query with real data on your dev server before deploying to production

## Best Practices

- Use `EXPLAIN`
    - Check the index usage    
    - Check rows scanned
- Use `LIMIT 1` clause when retrieving unique row (Laravel will do this internally)
    - Helps aggregate fnuctions like `MIN` or `MAX`
- Try to convert `<>` to `=` operator    
- Avoid using `SELECT *`
    - Forces a full table scan
    - Wastes network bandwidth
-   MySQL query cache is case sentitive
    - `select * from users` is different from `SELECT * FROM users` in cache.
- Index columns on the `WHERE` clause
- Table order does not matter when `INNER JOIN` clause is used
- If column used in `ORDER BY` clause are indexed, it helps with performance  

```mysql
SELECT CURRENT_USER(), CONNECTION_ID();
SHOW FULL PROCESSLIST;
```











**