---
description: Say hello to Livewire.
---

# Liveware

### Install Livewire

```bash
composer require livewire/livewire
```

Include the JavaScript \(on every page that will be using Livewire\).

```text
...
    @livewireStyles
</head>
<body>
    ...

    @livewireScripts
</body>
</html>
```

### Create a component <a id="create-a-component"></a>

Run the following command to generate a new Livewire component called `counter`.

```bash
php artisan make:livewire counter
```

Running this command will generate the following two files:

{% code title="app/Http/Liveware/Counter.php" %}
```php
namespace App\Http\Livewire;

use Livewire\Component;

class Counter extends Component
{
    public function render()
    {
        return view('livewire.counter');
    }
}
```
{% endcode %}

{% code title="resources/views/liveware/counter.blade.php" %}
```php
<div>
    ...
</div>
```
{% endcode %}

{% hint style="warning" %}
Livewire components MUST have a single root element.
{% endhint %}

```php
<div>
    <h1>Hello World!</h1>
</div>
```

### Include the component <a id="include-the-component"></a>

```php
<head>
    ...
    @livewireStyles
</head>
<body>
    @livewire('counter')

    ...

    @livewireScripts
</body>
</html>
```

### Livewire Route <a id="route-registration"></a>

If you find yourself writing controllers and views that only return a Livewire component, you might want to use Livewire's routing helper to cut out the extra boilerplate code. Take a look at the following example:

**Before -**

```php
// Route
Route::get('/home', 'HomeController@show');

// Controller
class HomeController extends Controller
{
    public function show()
    {
        return view('home');
    }
}

// View
@extends('layouts.app')

@section('content')
    @livewire('counter')
@endsection
```

**After -**

```php
// Route
Route::livewire('/home', 'counter');
```

{% hint style="warning" %}
Note: for this feature to work, Livewire assumes you have a layout stored in `resources/views/layouts/app.blade.php` that yields a "content" section \(`@yield('content')`\)
{% endhint %}

