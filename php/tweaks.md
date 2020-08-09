# Tweaks

### Helper Functions

#### Time as time ago

```php
function time_elapsed_string($datetime, $full = false) {
    $now = new DateTime;
    $ago = new DateTime($datetime);
    $diff = $now->diff($ago);

    $diff->w = floor($diff->d / 7);
    $diff->d -= $diff->w * 7;

    $string = array(
        'y' => 'year',
        'm' => 'month',
        'w' => 'week',
        'd' => 'day',
        'h' => 'hour',
        'i' => 'minute',
        's' => 'second',
    );
    foreach ($string as $k => &$v) {
        if ($diff->$k) {
            $v = $diff->$k . ' ' . $v . ($diff->$k > 1 ? 's' : '');
        } else {
            unset($string[$k]);
        }
    }

    if (!$full) $string = array_slice($string, 0, 1);
    return $string ? implode(', ', $string) . ' ago' : 'just now';
}
```

### Check Mobile Device

Check if the requested device is mobile or not

```php
function isMobileDevice()
{
    $aMobileUA = array(
        '/iphone/i'     => 'iPhone',
        '/ipod/i'       => 'iPod',
        '/ipad/i'       => 'iPad',
        '/android/i'    => 'Android',
        '/blackberry/i' => 'BlackBerry',
        '/webos/i'      => 'Mobile'
    );

    //Return true if Mobile User Agent is detected
    foreach ($aMobileUA as $sMobileKey => $sMobileOS) {
        if (preg_match($sMobileKey, $_SERVER['HTTP_USER_AGENT'])) {
            return true;
        }
    }
    //Otherwise return false..
    return false;
}
```

### GraphQL query

Graphql query from php application

```php
function graphQLQuery(string $query)
{
    //Log::info("Query : \n".$query);
    $queryUrl = env('BACKEND_URL') . '/graphql';
    $headers = ['Content-Type: application/json', 'User-Agent: Stenvaruhuset Client'];
    if (null !== session('token')) {
        $headers[] = "Authorization: " . session('token');
    }

    if (false === $data = @file_get_contents($queryUrl, false, stream_context_create([
            'http' => [
                'method'  => 'POST',
                'header'  => $headers,
                'content' => json_encode(['query' => $query]),
            ]
        ]))) {
        $error = error_get_last();
        throw new \ErrorException($error['message'], $error['type']);
    }

    $response = json_decode($data, false);
    if (isset($response->errors)) {
        return $response;
    }
    return $response->data;

}
```

