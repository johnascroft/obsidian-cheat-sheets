# Indexing

## Access Types

How it's going to access the data

### const / eq_ref

Performs a B-Tree traversal to find a single value in the index tree, basically you are doing binary search. Const and eq_ref can only get used if uniqueness is guaranteed (limit 1 does not guarantee uniqueness).

Super fast - if it's using either of these… stop optimising! It's not going to get any faster

### ref / range

Index range scan. Performs a B-Tree traversal to find the starting point, then scans values from that point on. It limits the total number of rows that the query has to inspect.

### index

This is also known as a full index scan. Starts at the first leaf node, traverses through the entire index. It goes through the entire index, but you are still using the index.

### ALL

Also known as a full table scan - avoid at all costs! Does not use an index at all, loads every column of every row from the table

### Examples

Get all orders that were made in 2013. Typically you would do this, but once you add a function to a where, you lose any indexing that you have.

```mysql
SELECT 
    SUM(total) 
FROM 
    orders 
WHERE 
    YEAR(created_at) = 2013;
```

`possible_key` = ones that could potentially be used for this query

`key` = keys that have actually been used

The best way of writing this is to do the following:

```mysql
CREATE INDEX orders_created_at_idx ON orders(created_at, total);

SELECT
    SUM(total)  
FROM
    orders
WHERE
    created_at BETWEEN '2013-01-01 00:00:00' AND '2013-12-31 23:59:59';
```

The extra column - “Using index” means “Using index ONLY” If you see this, it means it is doing an index only search. It’s super super fast, but is very specific.

## Multi-column indexes

If you have an index on 3 columns, created_at, total and user_id… you have to query them in the right order.

## Inequality Operators

If you have an inequality operator on a column, it can only use the index up to that point.