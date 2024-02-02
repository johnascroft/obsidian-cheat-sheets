# Apache

## Ubuntu

Shows the service status of Apache:

```bash
sudo service apache2 status
```

Starts the Apache service:

```bash
sudo service apache2 start
```

Terminates the Apache service:

```bash
sudo service apache2 stop
```

Stops and then starts the Apache service:

```bash
sudo service apache2 restart
```

Gracefully restarts the Apache service. On reload, the main Apache process shuts down the child processes, loads the new configuration, and starts new child processes:

```bash
sudo service apache2 reload
```

## CentOS 6 or earlier

For CentOS 6 or earlier, you need to replace `apache2` with `httpd`, like this:

```bash
sudo service httpd status
```

## RHEL/CentOS 7 and 8

For RHEL/CentOS 7 and 8 the process is also `httpd`. You will need to use `systemctl` instead of `service`, and switch the commands around a little, e.g.

```bash
sudo systemctl start httpd
```
