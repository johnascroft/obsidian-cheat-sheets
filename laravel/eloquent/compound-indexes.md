# Compound indexes

Ordering with multiple columns won't have any speed improvements when both fields are individual indexes. They can be compounded if you are using them both.

```php
User::query()
    ->orderBy('last_name')
    ->orderBy('first_name')
    ->get();
```

With this migration, the following code wouldn't use the indexes as you would expect.

```php
$table->string('first_name')->index();  
$table->string('last_name')->index();  
```

With this migration, the indexes would be used for this purpose.

```php  
$table->string('first_name');  
$table->string('last_name');  
$table->index(['last_name', 'first_name']);
```