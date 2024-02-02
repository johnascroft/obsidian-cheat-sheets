# set

```
## SET

Set `key` to hold the string `value`. If `key` already holds a value, it is overwritten, regardless of its type.

```bash
SET name "John"
SET mykey "this will expire in 5 seconds" EX 5
```

You can also use `MSET` to set multiple values:

```bash
MSET name "John" age 37 gender "Male"
```