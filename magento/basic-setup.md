# Basic Setup

### Nginx virtual host

#### Create Virtual Host nginx

```bash
upstream fastcgi_backend {
    # use tcp connection
    # server  127.0.0.1:9000;
    # or socket
    server   unix:/var/run/php/php7.3-fpm.sock;
}

server {
   listen 80;
   server_name website.com www.website.com;
 
   set MAGE_ROOT /var/www/website.com;
   set MAGE_MODE default;
 
   include /var/www/website.com/nginx.conf.sample;
   error_log /var/www/website.com/error_log warn; 
}
```

#### Location

```bash
/etc/nginx/sites-enabled/
```

{% hint style="info" %}
**If you have more than one magento project for Nginx then you can ignore `upstream fastcgi_backend` node for later project’s virtual host.**
{% endhint %}

### Apache virtual host

#### Create Virtual Host Apache2

```bash
<VirtualHost *:80>
	ServerName website.com
	ServerAlias www.website.com
	DocumentRoot /var/www/website.com
	<Directory /var/www/website.com>
		Options Indexes FollowSymLinks MultiViews
		AllowOverride All
		Require all granted
	</Directory> 
	ErrorLog /var/www/website.com/error.log
</VirtualHost>
```

#### Location

```bash
/etc/apache2/sites-enabled/
```

### Magento composer token

#### Set global magento2 token for composer

```bash
sudo chown -R ubuntu ~/.composer
composer.phar global config http-basic.repo.magento.com <public_key> <private_key>
# Example
composer global config http-basic.repo.magento.com f92d6b866405d0799d86b41ffe00e342 378bc0e72c91dcaa404266bdf87ee961
```

### Download Magento

#### Download magento project from git using composer

```bash
cd /var/www/website.com
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.3.5-p1 .
```

#### Project permission

```bash
find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +;
find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} +;
chown -R :www-data .;
chmod u+x bin/magento;
```

#### Create Database

```bash
sudo mysql -e "ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password'";
mysql -uroot -p -e "CREATE DATABASE project_database";
```

### Install Magento 2.3.x

```bash
$ php bin/magento setup:install --base-url=http://magento.test \
--db-host=localhost \
--db-name=database \
--db-user=root \
--db-password=root \
--admin-firstname=System \
--admin-lastname=Admin \
--admin-email=user@example.com \
--admin-user=admin \
--admin-password=admin \
--backend-frontname=admin \
--language=en_US \
--currency=USD \
--timezone=America/Chicago \
--use-rewrites=1
```

### Install Magento 2.4.x

```bash
$ php bin/magento setup:install --base-url=http://magento240.test \
--db-host=127.0.0.1 \
--db-name=database \
--db-user=root \
--db-password=root \
--admin-firstname=System \
--admin-lastname=Admin \
--admin-email=user@example.com \
--admin-user=admin \
--admin-password=admin \
--backend-frontname=admin \
--language=en_US \
--currency=USD \
--timezone=America/Chicago \
--search-engine=elasticsearch7 \
--elasticsearch-host=127.0.0.1 \
--elasticsearch-port=9200 \
--elasticsearch-index-prefix=magento2 \
--elasticsearch-timeout=15 \
--elasticsearch-enable-auth=false \
--use-rewrites=1
```

{% hint style="warning" %}
Other options are `--elasticsearch-username`,`--elasticsearch-password`
{% endhint %}

### Install Sample Data

```bash
$ wget https://github.com/magento/magento2-sample-data/archive/2.3.5.zip -O sampledata.zip
$ unzip sampledata.zip
$ php -f <sample-data_clone_dir>/dev/tools/build-sample-data.php -- --ce-source="<path_to_your_magento_instance>"
# example
$ php -f magento2-sample-data-2.3.5/dev/tools/build-sample-data.php -- --ce-source="."
$ sudo chmod -R 777 magento2-sample-data-2.3.5/pub
```

### Deploy Project

```bash
$ php bin/magento deploy:mode:set production --skip-compilation
$ php bin/magento setup:static-content:deploy sv_SE -a frontend
$ php bin/magento setup:static-content:deploy en_US -a adminhtml
```

