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

