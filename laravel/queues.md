# Queues

## Supervisor ([[supervisor]])

In production, you need a way to keep your `queue:work` processes running. A `queue:work` process may stop running for a variety of reasons, such as an exceeded worker timeout or the execution of the `queue:restart` command.

For this reason, you might reach for [[supervisor]].
## Failed jobs

If you want to start tracking failed jobs, you can use the following artisan command:

```bash
php artisan queue:failed-table

php artisan migrate
```

Show your failed jobs:

```bash
php artisan queue:failed
```

To retry a failed job:

```bash
php artisan queue:retry ce7bb17c-cdd8-41f0-a8ec-7b4fef4e5ece
```

To retry all failed jobs on a particular queue:

```bash
php artisan queue:retry --queue=name
```

To retry **all** failed jobs:

```bash
php artisan queue:retry all
```

To delete a failed job:

```bash
php artisan queue:forget 91401d2c-0784-4f43-824c-34f94a33c24d
```

To delete **all** failed jobs:

```bash
php artisan queue:flush
```