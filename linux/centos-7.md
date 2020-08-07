# CentOS 7

### Server Setup

```bash
sudo yum install epel-release

sudo yum install nginx mariadb-server mariadb

sudo systemctl enable nginx;
sudo systemctl start nginx;

firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload

rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

sudo yum install -y php71w-cli php71w php71w-common php71w-fpm php71w-intl php71w-mbstring php71w-mcrypt php71w-mysql php71w-pdo php71w-pecl-imagick php71w-soap php71w-xml

sudo systemctl start mariadb
sudo systemctl enable mariadb

sudo mysql_secure_installation

sudo mkdir /etc/nginx/sites-available
sudo mkdir /etc/nginx/sites-enabled
sudo vim /etc/nginx/nginx.conf

Add these lines to the end of the http {} block:

include /etc/nginx/sites-enabled/*.conf;
server_names_hash_bucket_size 64;

#allow 81 port
sudo iptables -I INPUT -p tcp --dport 81 -j ACCEPT
sudo iptables -I INPUT -p tcp --dport 81 -j REJECT

# unset SSH_ASKPASS

# cat ~/.ssh/id_rsa.pub | ssh root@[your.ip.address.here] "cat >> ~/.ssh/authorized_keys"
// selinux to allow write content in folder
#chcon -R -t httpd_sys_rw_content_t storage
#chown -R mysql:mysql /var/lib/mysql //for cerate new database mysql

setsebool -P httpd_can_network_connect on
setsebool -P httpd_can_sendmail on
```

