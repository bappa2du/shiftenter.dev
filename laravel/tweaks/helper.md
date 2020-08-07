# Helper

### Global helpers

{% hint style="info" %}
For global helper used in laravel `app/helpers.php` or `app/Http/helpers.php` add following in composer's autoload node.
{% endhint %}

```javascript
"files": [
            "app/helpers.php"
        ]
```

### Root htaccess

#### If laravel hosted using cpanel sometimes its difficult to map root folder to public. In that case create a `.htaccess` file with the content below.

```bash
RewriteEngine On
RewriteCond %{REQUEST_URI} !^/public/
RewriteRule ^(.*)$ /public/$1 [L,QSA]
```

### Important Packages

#### Important or Recommanded packages for Laravel which most frequently using -

1. For debugging `barryvdh/laravel-debugbar`
2. Pdf `barryvdh/laravel-dompdf`
3. Graphql `alexaandrov/laravel-graphql-client`
4. Page cache `silber/page-cache`
5. File-manager `unisharp/laravel-filemanager`
6. Image Manage & Upload `intervention/image`
7. Excel & Spreadsheet `maatwebsite/excel`
8. Role Permission `spatie/laravel-permission`

### Slack for Logging

#### You can add all of your project log to a specific slack channel through `channel webhook`

{% hint style="info" %}
Go to your project `.env` file and add the following settings as
{% endhint %}

```bash
LOG_CHANNEL=stack
LOG_SLACK_WEBHOOK_URL=`https://hooks.slack.com/services/TRR3YMWL2/BTFJ8G4RG/xxxxxxkxkxxkxkxxxxx
```

{% hint style="info" %}
Where `LOG_SLACK_WEBHOOK_URL` is the webhook key for the channel.
{% endhint %}

For slack workspace search for an Apps as `Incoming Webhooks`. When adding the apps just specify your desire channel. Finally you will get a webhook url.

{% hint style="warning" %}
For getting all the logs type like `info`,`debug`,`error` through webhook, go to `config/logging.php` and in `channels` section for `slack` set level `info` instead `debug`.
{% endhint %}

