# Conditional aggregates

Using `toBase()` means you will return a collection, not an instance of the model you’re using. In this case, Feature.

```php
$statuses = Feature::toBase()  
    ->selectRaw("count(case when status = 'Requested' then 1 end) as requested") 
    ->selectRaw("count(case when status = 'Planned' then 1 end) as planned")  
    ->selectRaw("count(case when status = 'Completed' then 1 end) as completed") 
    ->first();
```

This will give you something like this:

| requested    | planned    | completed    |
| --- | --- | --- |
| 4    | 7    | 1    |
