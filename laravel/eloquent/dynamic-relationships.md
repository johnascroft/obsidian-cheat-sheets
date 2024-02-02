# Dynamic relationships using subqueries

| Name | Email | Last Login |
| --- | --- | --- |
| Adam Campbell | adam@hotmeteor.com | Nov 10, 2018 at 12:01pm |
| Taylor Otwell | taylor@laravel.com | Never |
| Jonathan Reinink | jonathan@reinink.ca | Jun 2, 2018 at 5:30am |
| Adam Wathan | adam.wathan@gmail.com | Nov 20, 2018 at 7:49pm |

This is clever! The last_login_id field doesn't exist in the users table, but you can add a select to dynamically create it, and then eager load the relationship as if it was a *real* relation. One caveat with this is that you can’t lazy load it… because it doesn’t exist. You have to use all the logic in the scope to firstly create the field, then eager load the relationship.

## Lazy-loading dynamic relationships

One thing to be aware of with this technique is that you **cannot** lazy-load dynamic relationships out of the box. This is because our scope will not be added by default.

```php
class User extends Model
{
    public function lastLogin()
    {
        return $this->belongsTo(Login::class);
    }

    public function scopeWithLastLogin($query)
    {
        $query->addSelect(['last_login_id' => Login::select('id')
            ->whereColumn('user_id', 'users.id')
            ->latest()
            ->take(1)
        ])->with('lastLogin');
    }
}

$users = User::withLastLogin()->get();
```

## Can this not be done with a hasOne?

The short answer is no!