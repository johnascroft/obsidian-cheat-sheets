# Ordering by a hasOne relationship

It’s much more efficient to do this using a join rather than a subquery. This is the join approach:

```php
$users = User::query()  
    ->select('users.*')  
    ->join('companies', 'companies.user_id', '=', 'users.id')  
    ->orderBy('companies.name')  
    ->with('company')  
    ->paginate();
```

This is the subquery approach, which is quite a bit slower.

```php
$users = User::query()  
    ->orderBy(Company::select('name')  
        ->whereColumn('user_id', 'users.id')  
        ->orderBy('name')  
        ->take(1)  
    )  
    ->with('company')  
    ->paginate();
```