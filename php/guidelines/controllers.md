# Controllers

Controllers that control a resource must use the plural resource name, e.g. `PostsController`, `ProductsController`.

If you need other actions in a controller that aren't `index`, `create`, `store`, `show`, `edit`, `update`, `destroy`, consider extracting them into a new controller.

As an example, `favourite` and `unfavourite` can be extracted to a `FavouritePostsController` with standard CRUD actions.

```php
class PostsController
{
    public function favorite(Post $post)
    {
        request()->user()->favorites()->attach($post);

        return response(null, 200);
    }

    public function unfavorite(Post $post)
    {
        request()->user()->favorites()->detach($post);

        return response(null, 200);
    }
}
```

Would translate to:

```php
class FavoritePostsController
{
    public function store(Post $post)
    {
        request()->user()->favorites()->attach($post);

        return response(null, 200);
    }

    public function destroy(Post $post)
    {
        request()->user()->favorites()->detach($post);

        return response(null, 200);
    }
}
```