# Blade Template

### loop variable

#### Inside of foreach loop, check if current entry is first/last by just using $loop variable.

```text
 @foreach ($users as $user)
	 @if ($loop->first)
	 This is the first iteration.
	 @endif
	 @if ($loop->last)
	 This is the last iteration.
	 @endif
 <p>This is user {{ $user->id }}</p>
 @endforeach
```

### Check view file

#### You can check if View file exists before actually loading it.

```php
if (view()->exists('custom.page')) {
	return view('custom.page');
} 
```

#### Other way

```php
return view()->first(['custom.dashboard', 'user.dashboard'], $data);
```

