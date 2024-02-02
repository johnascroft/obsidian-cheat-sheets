# OOP Tips

Always put the method in the right class. The method should go into the class of the thing that “owns” it.

An **{Object}**  
Can Be **{Method}**  
(Using a **{Parameter}**.)  

Other examples:

```js
names.split(delimiter)
names.reverse()
```

```php
$date->format('l');
$user->save();
```

These examples are poor:

```php
$gardener->water($plant);

$user->redeemLicence($licence);
```

This examples are better:
  
```php
$plant->water($gardner);

$licence->redeem($user);
```