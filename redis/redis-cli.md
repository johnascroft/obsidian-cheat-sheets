# Redis CLI

Full list of commands can be found in the [Redis Commands](https://redis.io/commands)

To start up the Redis CLI in [[linux]]:

```bash
redis-cli
```

To monitor what is going on in Redis, you can use:

```bash
redis-cli monitor
```

- [[keys]]
- [[set]]
- get
- del
- exists
- dbsize
- flushdb

## GET

Get the value of `key`. If the key does not exist the special value `(nil)` is returned.

```bash
GET name
GET age
GET gender
```

You can also use `MGET` to get multiple values:

```bash
MGET name age gender
```

## DEL

Removes the specified keys. A key is ignored if it does not exist.

```bash
DEL mykey
DEL name age gender
```

## EXISTS

Check to see if a key or keys exist in the current database.
This will return either `(integer) 1` or `(integer) 0`.

```bash
EXISTS age
EXISTS name age gender
```

## DBSIZE

Return the number of keys in the currently-selected database.

```bash
127.0.0.1:6379> DBSIZE
(integer) 4
```

## FLUSHDB

Delete all the keys of the currently selected DB.

```bash
127.0.0.1:6379> FLUSHDB
OK
```

