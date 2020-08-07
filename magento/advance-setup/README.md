# Advance Setup

### Elasticsearch 7

{% hint style="info" %}
Install elasticsearch `v7.x`
{% endhint %}

```bash
# Linux
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.1-linux-x86_64.tar.gz
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.1-linux-x86_64.tar.gz.sha512
shasum -a 512 -c elasticsearch-7.8.1-linux-x86_64.tar.gz.sha512 
tar -xzf elasticsearch-7.8.1-linux-x86_64.tar.gz
cd elasticsearch-7.8.1/ 

# Mac
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.1-darwin-x86_64.tar.gz
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.1-darwin-x86_64.tar.gz.sha512
shasum -a 512 -c elasticsearch-7.8.1-darwin-x86_64.tar.gz.sha512 
tar -xzf elasticsearch-7.8.1-darwin-x86_64.tar.gz
cd elasticsearch-7.8.1/ 
```

#### Running as deamon

```text
$ ./bin/elasticsearch -d -p pid
$ pkill -F pid
```

#### Sample Configuration

```text
cluster.name: Bappa_Cluster
node.name: MYNODE_CYR
node.master: true
node.data: true
transport.host: localhost
transport.tcp.port: 9300
http.port: 9200
network.host: 0.0.0.0
discovery.zen.minimum_master_nodes: 2
```

{% hint style="warning" %}
This will enable the remote access via `9200` port.
{% endhint %}

### Varnish installation

```bash
$ sudo apt install varnish -y
$ varnish -V
$ systemctl start varnish
$ systemctl enable varnish
$ sudo netstat -putln | grep varnishd
```

#### For Apache server:

```bash
$ sudo a2enmod proxy  
$ sudo a2enmod proxy_http 
$ sudo a2enmod headers
$ sudo vi /etc/apache2/ports.conf
```

{% hint style="info" %}
Set listen port to `8080` instead `80` and in virtual host config set port to `8080` as well.
{% endhint %}

```bash
<VirtualHost *:8080>
# Then restart the server
$ sudo systemctl restart apache2
```

#### For Nginx server:

{% hint style="info" %}
Set listen port to `8080` instead of `80`.
{% endhint %}

### Varnish Configuration

```bash
$ sudo vi  /etc/default/varnish
# set VARNISH_LISTEN_PORT=80
# replace -a param in DAEMON_OPTS
DAEMON_OPTS="-a :80 \
   -T localhost:6082 \
   -f /etc/varnish/default.vcl \
   -S /etc/varnish/secret \
   -s malloc,256m"
$ sudo sudo cp /etc/varnish/default.vcl /etc/varnish/default.vcl.bak
# export magento varnish configurations file
$ sudo vi /etc/varnish/default.vcl
# paste in it
# set .host = "127.0.0.1" .port = "8080"
$ sudo vi /lib/systemd/system/varnish.service
# Then change the varnish port 6081 to HTTP port 80
# ExecStart=/usr/sbin/varnishd -j unix,user=vcache -F -a :80 -T localhost:6082 -f /etc/varnish/default.vcl -S /etc/varnish/secret -s malloc,256m
$ sudo systemctl daemon-reload
$ sudo systemctl restart varnish
```

#### Apache virtual host with proxy pass:

```bash
<VirtualHost *:443>
    RequestHeader set X-Forwarded-Proto "https"
    ServerName server.com

    SSLEngine On
    SSLCertificateFile /etc/letsencrypt/live/server.com/fullchain.pem
	  SSLCertificateKeyFile /etc/letsencrypt/live/server.com/privkey.pem
	  Include /etc/letsencrypt/options-ssl-apache.conf

    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:80/
    ProxyPassReverse / http://127.0.0.1:80/
</VirtualHost>
```

{% hint style="warning" %}
if you have redirect issue arise remove rewrite condition in apache2 virtual hosts.
{% endhint %}

#### Nginx ssl config in server node:

```bash
location / {
        proxy_pass http://127.0.0.1:80;
        proxy_set_header Host $http_host;
        proxy_set_header X-Forwarded-Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Ssl-Offloaded "1";
        proxy_set_header X-Forwarded-Proto https;
        proxy_set_header X-Forwarded-Port 443;
        proxy_redirect http://website.com/  /;
        proxy_http_version 1.1;
    }
```

#### Final verification\(Header in development mode\):

```bash
X-Magento-Cache-Control: max-age=86400, public, s-maxage=86400
Age: 0
X-Magento-Cache-Debug: MISS

# Also acceptable value
X-Magento-Cache-Debug: HIT
```

