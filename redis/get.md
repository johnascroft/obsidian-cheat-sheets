## get

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