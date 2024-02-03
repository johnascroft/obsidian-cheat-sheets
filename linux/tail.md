# tail

The `--lines` option (abbreviated to `-n`) changes the total lines that are tailed. The default is 10.

```bash
tail -n 50 /var/log/apache2/error.log
```

The `--follow` option causes **tail** to loop forever, checking for new data at the end of the file(s). When new data appears, it will be printed.

```bash
tail -f /var/log/apache2/error.log
```