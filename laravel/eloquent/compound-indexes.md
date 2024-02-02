# Compound indexes

Ordering with multiple columns won't have any speed improvements when both fields are individual indexes. They can be compounded if you are using them both.

```php
$table->string('first_name')->index();  
$table->string('last_name')->index();  
  
$table->string('first_name');  
$table->string('last_name');  
$table->index(['last_name', 'first_name']);
```