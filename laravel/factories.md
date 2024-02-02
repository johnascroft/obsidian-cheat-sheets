# Factories

[Laravel 5.8 - Official Documentation](https://laravel.com/docs/5.8/database-testing)
[Laravel 9.x - Official Documentation](https://laravel.com/docs/9.x/eloquent-factories)

Number with a certain amount of digits:

```php
'mprn' => fake()->numerify('##########'),
```

Random ID from another table:

```php
'form_type_id' => function () use ($formType) {  
    return FormType::all()->random()->id;  
},
```