# Raw indexes

In this example, we want to order by people's birthday, using the format `month-date`.

This will order as you want it to, but the column won't be indexed:

```php
public function scopeOrderByBirthday($query)  
{  
    $query->orderByRaw('date_format(birth_date, "%m-%d")');  
}
```

As we are ordering by a raw expression (that isn’t indexed), you can improve performance by adding a `rawIndex` to the migration. This will ensure that when you are ordering by the raw expression, it will use the index and not have to scan all rows.

```php
Scheme::create('users', function (Blueprint $table) {  
    $table->id();  
    $table->string('name');  
    $table->date('birth_date')->nullable();  
    // other fields...  
    $table->rawIndex("(date_format(birth_date, '%m-%d')), name", "users_birthday_name_index");  
});
```