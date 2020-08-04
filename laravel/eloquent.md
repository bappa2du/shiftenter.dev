## Date methods
> In Eloquent, check the date with functions ​`whereDay()`​, `​whereMonth()`​, `​whereYear()`​,
`whereDate()`​ and `​whereTime()`​.
```php
$products = Product::whereDate('created_at', '2018-01-31')->get();
$products = Product::whereMonth('created_at', '12')->get();
$products = Product::whereDay('created_at', '31')->get();
$products = Product::whereYear('created_at', date('Y'))->get();
$products = Product::whereTime('created_at', '=', '14:13:58')->get();
```

## No timestamp columns
> If in any model `created_at` and `updated_at` absent, then in eloquent model set `$timestamps` property to `false`
```php
class Vendor extends Model
{
	public $timestamps = false;
}
```