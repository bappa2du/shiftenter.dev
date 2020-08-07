# Developer

### Magento profiler

```php
$_SERVER['MAGE_PROFILER'] = 'html';
# at beginning of index.php page
```

### Cron list

#### Get magento cron job list:

```bash
$ wget https://files.magerun.net/n98-magerun2.phar
$ chmod +x ./n98-magerun2.phar; 
$ ./n98-magerun2.phar --version
$ ./n98-magerun2.phar sys:cron:list
```

### Create admin

#### Create admin from cli

```bash
php bin/magento admin:user:create \
--admin-user="admin" \
--admin-password="123123q" \
--admin-email="admin@example.com" \
--admin-firstname="Admin" \
--admin-lastname="Admin"
```

{% hint style="warning" %}
If admin user with same email already exists then user will be updated
{% endhint %}

### Add Js to CMS Page

First create the custom.js at below location \(in your case you have already did this\)

```bash
app/design/{Vendor_name}/{theme}/web/js/custom.js
```

Now Just traverse to the below location

```bash
Admin > Content > Elements > Pages > Design > Layout Update XML
```

Put the below code there in that section

```bash
<head>
    <link src="js/custom.js"/>
</head>
```

{% hint style="success" %}
Save the page & flush the cache & you will see it is working
{% endhint %}

### System Config Field Magento 2

Magento 2 system configuration provides below fields type -

1. checkbox, 
2. checkboxes, 
3. column, 
4. date, 
5. editablemultiselect, 
6. editor, 
7. fieldset, 
8. file, 
9. gallery, 
10. hidden, 
11. image, 
12. imagefile, 
13. label, 
14. link, 
15. multiline, 
16. multiselect, 
17. note, 
18. obscure, 
19. password, 
20. radio, 
21. radios, 
22. reset, 
23. select, 
24. submit, 
25. text, 
26. textarea, 
27. time

