---
title: "WordPress"
date: 2021-08-11T10:11:20+08:00
draft: true
---

### Git Path

[https://github.com/doafirst/html.git](https://github.com/doafirst/html.git) (origin 5-WordPress)

因為wordpress是以www-data使用者來處理檔案
所以比須做chown 及 sudo -u www-data來使用git

```bash
cd /var
chwon www-data:www-data www/
cd www
sudo -u www-data git clone https://github.com/doafirst/html.git
cd html
sudo -u www-data git checkout 5-WordPress
```

### 安裝流程

1. **下載wordpress org from [https://wordpress.org/latest.tar.gz](https://wordpress.org/latest.tar.gz) (lastest.tar.gz)**

解壓縮到 /var/www/html/ (反正就是讓local host的php指到它)

```bash
cd /var/www/html
wget [https://wordpress.org/latest.tar.gz](https://wordpress.org/latest.tar.gz) 
tar zxvf latest.tar.gz
```

![WordPress/Screenshot_from_2021-08-08_16-17-56.png](Screenshot_from_2021-08-08_16-17-56.png)

1. **安裝dependency** 

```bash
sudo apt update
sudo apt install apache2 \
                 ghostscript \
                 libapache2-mod-php \
                 mysql-server \
                 php \
                 php-bcmath \
                 php-curl \
                 php-imagick \
                 php-intl \
                 php-json \
                 php-mbstring \
                 php-mysql \
                 php-xml \
                 php-zip
```

1. **MYSQL database → 建立database ,username ,password及grant**

```bash
# mysql -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 39
Server version: 5.1.41-3ubuntu12.10 (Ubuntu)

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> **CREATE DATABASE wordpress;**
Query OK, 1 row affected (0.00 sec)

mysql> **CREATE USER 'wordpress'@'localhost' IDENTIFIED BY 'wordpress';**
Query OK, 0 rows affected (0.00 sec)

mysql> **GRANT ALL PRIVILEGES ON wordpress.* to wordpress@localhost;**
Query OK, 0 rows affected (0.00 sec)

mysql> quit
Bye
```

```
MYSQL Command:
    show databases;
    drop database wordpress;
    flush previleges;
    use wordpress;
    show tables;
```

1. **WordPress connect to MYSQL database**

![WordPress/Screenshot_from_2021-08-08_17-32-18.png](Screenshot_from_2021-08-08_17-32-18.png)

Generate "wp-config.php" file  


```php
<?php
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'wordpress' );

/** MySQL database username */
define( 'DB_USER', 'wordpress' );

/** MySQL database password */
define( 'DB_PASSWORD', 'wordpress' );

/** MySQL hostname */
define( 'DB_HOST', 'localhost' );

/** Database charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8mb4' );

/** The database collate type. Don't change this if in doubt. */
define( 'DB_COLLATE', '' );

define( 'AUTH_KEY',         '7B NxcBWg1W-uP,{)qE@k/z2m:=yS!{3Xm,>geslbpBk.~Onv6^NHhUhA#^o~Wbr' );
define( 'SECURE_AUTH_KEY',  'hZ0qmu6wS8|`ry$nprU_Jyob=::?z-E3r+RF$pn2cY?m4Q3UU~*n*P<Op94e+R=&' );
define( 'LOGGED_IN_KEY',    'P+ftd:`rqX:}1+dUYmp_tf 7oAtfw]5*{[LB`gcw`*54:GG5B@v*uesHJhZQJ-*1' );
define( 'NONCE_KEY',        ']wOoFF}j|T%Z:1<[j1{voK6f;8`ch#Uh NeHCIb(i5O+Ei4zG(#{&c[@<=[w3`uT' );
define( 'AUTH_SALT',        'iZVR]=UpT2^HH|F<$!CUL06@hvV Qd@+ip}|rE)j3wQgl@72!5GV:(iZ6zHUY?E_' );
define( 'SECURE_AUTH_SALT', 'Hb_*!L={5B~3!E.xkz_QGGBb@,~sYON*yR`f9*wj&M#Or~m~,R6v01-w^^d]7R!e' );
define( 'LOGGED_IN_SALT',   '@a)Kmm5i5f!G=bdH+(r.FpU _L=0K8LJ^DS5@96CO`<:P+exrggZE|8`dX_6*|81' );
define( 'NONCE_SALT',       'HeYV/+E:v:,u8)0H0CDuFRdK}n c5,we :cTCNxsN6PQzvq:Bf;H(o??lZJs)H=a' );

define('FS_METHOD','direct');
$table_prefix = 'wp_';

define( 'WP_DEBUG', false );

if ( ! defined( 'ABSPATH' ) ) {
	define( 'ABSPATH', __DIR__ . '/' );
}

/** Sets up WordPress vars and included files. */
require_once ABSPATH . 'wp-settings.php';
```

1. **How to Fix "WordPress Needs Access to Your Web Server"**

![Screenshot_from_2021-08-08_20-10-17.png](Screenshot_from_2021-08-08_20-10-17.png)

Add line **"define('FS_METHOD','direct');"** into wp-config.php file
