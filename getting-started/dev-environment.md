---
description: LAMP/LEMP setup for your environment
---

# Dev Environment

### Install Server

{% hint style="info" %}
Install Nignx/Apache, PHP, Mysql & other utilities
{% endhint %}

```bash
$ sudo apt update
$ sudo add-apt-repository ppa:ondrej/php;
$ sudo apt install php7.3 php7.3-soap php7.3-zip php7.3-curl php7.3-xml php7.3-gd php7.3-intl php7.3-bcmath php7.3-mysql mysql-server php7.3-fpm nginx php7.3-mbstring git vim zip htop -y;
```

{% hint style="warning" %}
If you want to install **apache** server then replace **nginx** with **apache2** in the above command.
{% endhint %}

### Switch default PHP <a id="switch-default-php"></a>

{% hint style="info" %}
If you have multiple php version you can switch as below.
{% endhint %}

```bash
$ sudo update-alternatives --set php /usr/bin/php7.3
```

### Install Composer

```bash
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer;
```

### Server Restart

```bash
# for apache
sudo service apache2 restart;
# for nginx
sudo service nginx restart;
sudo service php7.3-fpm restart # if required
```

{% hint style="info" %}
Automatically start server after reboot
{% endhint %}

```bash
sudo systemctl enable apapche2;
sudo systemctl enable php7.3-fpm;
sudo systemctl enable nginx;
sudo systemctl enable mysql;
```

### Install Nodejs

{% hint style="info" %}
Install nodejs using Binary Distributions
{% endhint %}

#### Node.js v14.x:

```bash
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_14.x | bash -
apt-get install -y nodejs
```

#### Node.js v12.x:

```bash
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_12.x | bash -
apt-get install -y nodejs
```

### Valet\(Mac OS\)

#### Valet for MacOS development platform

```bash
brew install php
composer global require laravel/valet
echo 'export PATH="/Users/user/.composer/vendor/bin:$PATH"' >> ~/.bashrc
valet start
brew install mysql@5.7
brew services start mysql@5.7
valet use php@7.2
# secure site
valet secure laravel
# unsecure site
valet unsecure laravel
```

{% hint style="danger" %}
**Valet Mysql issues**
{% endhint %}

#### Sometime it says yout mysql blow away. Edit file `/etc/my.cnf`

```bash
# Default Homebrew MySQL server config
[mysqld]
# Only allow connections from localhost
bind-address = 127.0.0.1
default-authentication-plugin = mysql_native_password
max_allowed_packet = 256M
wait_timeout = 28800
```

