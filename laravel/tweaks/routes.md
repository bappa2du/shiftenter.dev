# Routes

### Route view:

{% hint style="info" %}
If you want a route just for view use route view as
{% endhint %}

```php
Route::view('faq', 'details.faq');
```

### Parameters to Routes:

If you pass additional parameters to the route, in the array, those key / value pairs will automatically be added to the generated URL's query string.

```php
Route::get('user/{id}/profile', function ($id) {
 //
})->name('profile');
$url = route('profile', ['id' => 1, 'photos' => 'yes']);
// Result: /user/1/profile?photos=yes
```

### Faster routing:

Instead of routing like this

```php
Route::get('page', 'HomeController@action');
```

> You can specify the Controller as a class -

```php
Route::get('page', [\App\Http\Controllers\HomeController::class, 'action']);
```

