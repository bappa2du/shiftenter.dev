# Basic

### Nginx config

```bash
server {
    listen 80;
    server_name www.domain.com domain.com;

    root /home/ubuntu/domain.com;
    index index.php;


    # log files
    access_log /home/ubuntu/domain.com/access.log;
    error_log /home/ubuntu/domain.com/error.log;

    location = /favicon.ico {
        log_not_found off;
        access_log off;
    }

    location = /robots.txt {
        allow all;
        log_not_found off;
        access_log off;
    }

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.3-fpm.sock;
    }

    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg)$ {
        expires max;
        log_not_found off;
    }

}
```

### Nginx redirect

#### Redirect page using nginx config

```bash
server {
    server_name webpage.com;
    return 301 $scheme://www.webpage.com$request_uri;
}
```

### Swap memory

```bash
sudo fallocate -l 1G /swapfile;
sudo chmod 600 /swapfile;
sudo mkswap /swapfile;
sudo swapon /swapfile;
echo '/swapfile swap swap sw 0 0' | sudo tee -a /etc/fstab
```

### Let's Encrypt

#### Installing Certbot

```bash
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python-certbot-nginx
# for apache
sudo apt-get install python-certbot-apache
sudo certbot --nginx -d example.com -d www.example.com
```

### Nginx 302

#### Nginx 302 bad gateway

```bash
$ sudo vi /etc/nginx/nginx.conf
# in http node add
fastcgi_buffers 16 16k; 
fastcgi_buffer_size 32k;

$ sudo service nginx reload/restart
```

### Composer issue

#### Composer issues during installation

```bash
composer install --ignore-platform-reqs
php -d memory_limit=-1 /usr/local/bin/composer install
```

### SSH Tunneling

#### When we need to connect a server using a middle server

```bash
$ ssh -L 8090:B_IP:22 A 
$ ssh B@127.0.0.1 -p 8090 -i ~/.ssh/B_key.pem
```

{% hint style="info" %}
here `B_IP` is final destination IP, `A` is intermediate/middle server which config setup on ~/.ssh/config as
{% endhint %}

```bash
Host A
	Hostname A_IP
	User ubuntu
	IdentityFile ~/.ssh/A_key.pem
```

{% hint style="success" %}
finally we connect to B\_IP via A\_IP
{% endhint %}

### Server git webhook

#### Set up `git` and `server` webhook as below

```bash
$ sudo apt install webhook supervisor -y
$ sudo systemctl stop webhook
$ whoami
# {username}
$ mkdir ~/webhooks
$ mkdir ~/webhooks/deployment
$ touch ~/webhooks/hooks.json
$ touch ~/webhooks/deployment/deploy.sh
$ chmod +x ~/webhooks/deployment/deploy.sh
$ vi ~/webhooks/deployment/deploy.sh
```

{% hint style="info" %}
Edit file with your required commands
{% endhint %}

```bash
#!/bin/bash

git pull origin master
# composer dumpautoload
# php artisan c:c
# php bin/magento c:f
# rm -rf generated/*
```

#### Then edit `$ vi ~/webhooks/hooks.json`

```bash
[
  {
    "id": "website-webhook",
    "execute-command": "/home/ubuntu/webhooks/deployment/deploy.sh",
    "command-working-directory": "/home/ubuntu/example.com",
    "response-message": "Executing deploy script..."
  }
]
```

#### Finally edit `supervisor` as `sudo vi /etc/supervisor/conf.d/webhook.conf`

```bash
[program:webhooks]
command=bash -c "/usr/bin/webhook -hooks /home/ubuntu/webhooks/hooks.json -verbose"
redirect_stderr=true
autostart=true
autorestart=true
user=ubuntu
numprocs=1
process_name=%(program_name)s_%(process_num)s
stdout_logfile=/home/ubuntu/webhooks/supervisor.log
environment=HOME="/home/ubuntu",USER="ubuntu"
```

#### Now enable and restart supervisor

```bash
$ sudo systemctl enable supervisor
$ sudo systemctl restart supervisor
```

{% hint style="info" %}
Now you can add webhook to you `github`,`gitlab` or `bitbucket` repo
{% endhint %}

```bash
http://id:9000/hooks/{hook_id}
# Example
http://111.222.178.598:9000/hooks/website-webhook
```



