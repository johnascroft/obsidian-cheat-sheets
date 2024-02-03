# Laravel upgrade

Take a fresh copy of [Laravel 10](https://laravel.com/docs/10.x/installation#creating-a-laravel-project)

Migrate all the existing code over to Laravel 10

Controllers (largely unchanged)
Models (largely unchanged)
Migrations (update to new syntax)
Routes (update to new syntax)

```php
use App\Http\Controllers\UserController;

Route::get('/user', [UserController::class, 'index']);
```

Replace Laravel Mix with [Vite](vite).

Include [Inertia](https://inertiajs.com/) from [[npm]].

Replace blade files with singular file and Vue components