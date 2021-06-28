
# Deploy a Laravel App to EC2 (Amazon Linux 2 - RHEL)
Laravel v8.12.3 (PHP v7.4.19) Mysql 8.0  

---  
```sh
$ sudo yum update -y
$ sudo amazon-linux-extras enable php7.4 -y
$ sudo yum clean metadata
$ sudo yum install -y php php-{pear,cgi,common,curl,mbstring,gd,mysqlnd,gettext,bcmath,json,xml,fpm,intl,zip,imap}
$ sudo yum install -y git
$ curl -sS https://getcomposer.org/installer | php
$ sudo  mv composer.phar /usr/bin/composer
$ chmod +x /usr/bin/composer

$ php --version
```
**Dependencies installation will take some time. Then set proper permissions on files.**  
```sh
$ sudo chown -R ec2-user:apache /var/www
$ sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
$ find /var/www -type f -exec sudo chmod 0664 {} \;

$ cd /var/www/html
$ composer create-project --prefer-dist laravel/laravel my-laravel-app "8.*"
$ cd /var/www/html/my-laravel-app
$ composer install


$ cp .env.example .env
$ php artisan key:generate
$ chmod -R 777 storage/
```

**Set the host:**  
```sh
$ sudo vim /etc/httpd/conf/httpd.conf
```

**Add code at the bottom of the file**
*Apache2 server configs*

```blade
<VirtualHost *:80>
	ServerName laravel.example.com
	DocumentRoot /var/www/html/my-laravel-app/public
	<Directory /var/www/html/my-laravel-app>
		AllowOverride All
	</Directory>
</VirtualHost>
```  


**Enabling PHP-FPM:**

```sh
$ sudo systemctl start httpd
$ sudo systemctl start php-fpm
$ sudo systemctl enable php-fpm
```

