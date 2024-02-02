# Scopes

## Scope for searching

There are better ways of doing this in terms of indexing and optimisation of the query, but consider using a search scope rather than putting all of the search logic into a controller.

```php
$users = User::query()  
    ->search(request('search'))  
    ->with('company')  
    ->paginate();  
```

```php  
use Illuminate\Database\Eloquent\Builder;

public function scopeSearch(Builder $query, string $terms = null)  
{  
    collect(explode(' ', $terms))->filter()->each(function($term) use ($query) {  
        $term = '%' . $term . '%';  
        $query->where(function($query) use ($term) {  
            $query->where('first_name', 'like', $term)  
                ->orWhere('last_name', 'like', $term)  
                ->orWhereHas('company', function($query) use ($term) {  
                    $query->where('name', 'like', $term);  
                });  
        })  
    });  
}
```

## Running authorisation policies in the database

Really useful for when you have loads of records and it doesn’t make sense to filter stuff out using [[php]]. You can pass the user model into a scope and do you filtering directly in the database.

```php
use Illuminate\Database\Eloquent\Builder;
use App\Models\User;

public function scopeVisibleTo(Builder $query, User $user)  
{  
    if ($user->is_owner) {  
        return;  
    }  
  
    $query->where('sales_rep_id', $user->id);  
}
```

Usage: 

```php
$customers = Customer::visibleTo($user)->get();
```