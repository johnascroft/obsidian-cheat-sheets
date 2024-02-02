# Supervisor

## Installation

```bash
sudo apt-get install supervisor
```

## Configuration

The main Supervisor configuration file is `supervisord.conf` and is usually found at `/etc/supervisor/supervisord.conf`.

## Subprocesses

Subprocesses are stored in `/etc/supervisor/conf.d`.

```bash
[program:laravel-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /home/forge/app.com/artisan queue:work sqs --sleep=3 --tries=3 --max-time=3600
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
user=forge
numprocs=8
redirect_stderr=true
stdout_logfile=/home/forge/app.com/worker.log
stopwaitsecs=3600
```
## Running supervisorctl

Full list of [Supervisor actions](http://supervisord.org/running.html#supervisorctl-actions). The ones listed below are the most commonly used:

Reload the daemon’s configuration files. This **does not** add/remove anything and **does not** restart jobs.

```bash
sudo supervisorctl reread
```

Reload config and add/remove as necessary, and will restart affected programs:

```bash
sudo supervisorctl update
```

Start a process:

```bash
sudo supervisorctl start laravel-worker:*
```