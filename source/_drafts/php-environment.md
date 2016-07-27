---
title: php-environment
tags:
---

## Vagrant

box：centos-6.5-x86_64-minimal.box
vagrant init centos6.5_64

network：

shell：

rpm -Uvh http://ftp.iij.ad.jp/pub/linux/fedora/epel/6/x86_64/epel-release-6-8.noarch.rpm >/etc/null 2>&1
rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm >/etc/null 2>&1
yum --enablerepo=remi --enablerepo=remi-php56 install -y php php-opcache php-devel php-mbstring php-mcrypt php-mysqlnd php-phpunit-PHPUnit  php-pecl-xhprof php-fpm php-pdo php-mysql php-gd php-xml php-xmlrpc php-pear >/etc/null 2>&1
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
chmod +x /usr/local/bin/composer
yum install wget >/etc/null 2>&1
wget http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm -P /data >/etc/null 2>&1
rpm -ivh nginx-release-centos-6-0.el6.ngx.noarch.rpm
yum install nginx >/etc/null 2>&1
chkconfig nginx on
service nginx start
/etc/init.d/mysqld restart  #重启MySql
/etc/init.d/nginx  restart  #重启nginx
/etc/rc.d/init.d/php-fpm start  #启动php-fpm
chkconfig php-fpm on  #设置开机启动



```shell
Vagrant.configure(2) do |config|

	config.vm.box = "~/box/centos-6.5-x86_64-minimal.box"
	config.vm.box_check_update = false

	config.vm.network "forwarded_port", guest: 80, host: 8080

	config.vm.synced_folder "./data", "/data", create: true
	config.vm.synced_folder "./www", "/var/www", create: true, group: "www", owner: "www"

	config.vm.provision "shell", path: "provision/setup.sh"

end
```



同步文件夹：

方案一

站点根目录：./www	=>	/var/www 
文件同步： ./data	=> /data（可供shell中使用）

方案二

数据同步： ./data => /data
站点: ln -fs /var/www /data/www  使得guest主机中的/var/www对应到其/data/www，而/data目录是同步文件，则在host主机中也能访问

## PHP

版本：5.6.23

path：php: /usr/bin/php /etc/php.ini /etc/php.d /usr/lib64/php /usr/include/php /usr/share/php /usr/share/man/man1/php.1.gz

扩展：
php 
php-opcache 
php-devel 
php-mbstring
php-mcrypt 
php-mysqlnd 
php-phpunit-PHPUnit 
php-pecl-xdebug (未安装)
php-pecl-xhprof 
php-fpm 
php-pdo 
php-mysql 
php-gd 
php-xml 
php-xmlrpc 
php-pear

## Nginx

主进程所有者：root

path：nginx: /usr/sbin/nginx /etc/nginx /usr/share/nginx /usr/share/man/man3/nginx.3pm.gz /usr/share/man/man8/nginx.8.gz

工作进程所有者：www/www

用户/用户组 www/www

站点目录  /var/www/[site.com]  可读可写

上传目录：/var/www/[site.com]/uploads 可读可执行

配置文件：

cp /etc/nginx /data/nginx
编辑
cp /data/nginx/ /etc/nginx

