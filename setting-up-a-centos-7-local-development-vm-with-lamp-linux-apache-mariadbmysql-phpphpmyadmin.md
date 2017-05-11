# Code from withdave.com
This code is for:
> https://withdave.com/2017/02/setting-up-a-centos-7-local-development-vm-with-lamp-linux-apache-mariadbmysql-phpphpmyadmin/

Only sections with relevant code will be shown below.

# Code snippets

## Step 2

```
yum update
```

## Step 3

```
yum -y install nano wget
```

## Step 4

```
yum -y install httpd
```

```
systemctl start httpd
systemctl enable httpd
systemctl status httpd
```

```
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload
```

## Step 5

```
yum -y install mariadb-server
```

```
systemctl start mariadb
systemctl enable mariadb
```

```
mysql_secure_installation
```

```
mysql -u root -p
```

## Step 6

```
yum -y install php
```

```
service httpd restart
```

```
nano /var/www/html/phpinfo.php
```

```
<?php

echo phpinfo();

?>
```

```
yum -y install php-gd php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-snmp php-soap curl curl-devel php-mysql
```

```
service httpd restart
```

## Step 7

```
yum -y install epel-release
rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
```

```
yum -y install phpmyadmin
```

```
service httpd restart
```

```
nano /etc/httpd/conf.d/phpMyAdmin.conf
```

```
<IfModule mod_authz_core.c>
# Apache 2.4
<RequireAny>
Require ip 127.0.0.1
Require ip ::1
Require all granted
</RequireAny>
</IfModule>
<IfModule !mod_authz_core.c>
# Apache 2.2
Order Deny,Allow
Deny from All
Allow from 127.0.0.1
Allow from ::1
</IfModule>
```

```
service httpd restart
```

## Installing Webmin

```
nano /etc/yum.repos.d/webmin.repo
```

```
[Webmin]
name=Webmin Distribution Neutral
#baseurl=http://download.webmin.com/download/yum
mirrorlist=http://download.webmin.com/download/yum/mirrorlist
enabled=1
```

```
wget http://www.webmin.com/jcameron-key.asc
rpm --import jcameron-key.asc
yum -y install webmin
```

```
/usr/libexec/webmin/changepass.pl /etc/webmin root NEWPASSWORD
```
