# Models

Create a model with optional parameters:

|Shorthand|Option|
|---|---|
|`-c`|`--controller`|
|`-f`|`--factory`|
|`-m`|`--migration`|
|`-s`|`--seed`|

```bash
php artisan make:model -cfms Form
```

Show attributes, relations and key information on a given model:

```bash
php artisan model:show Offer
```

## Casting

```php
protected $casts = [
    'is_admin' => 'boolean',
    'options' => 'array',
];
```

### Date casting

By default, Eloquent will cast the `created_at` and `updated_at` columns to instances of [Carbon](https://github.com/briannesbitt/Carbon). You can also cast your own dates as Carbon objects:

Note that in Laravel 5.8 you use the `$dates` property, and in Laravel 9.x you use `$casts` as below:

```php
/**
* The attributes that should be cast.
*
* @var array
*/
protected $casts = [
    'created_at' => 'datetime:Y-m-d',
];
```
