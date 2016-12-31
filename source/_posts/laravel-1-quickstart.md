---
title: Laravel学习之快速指南
date: 2016-12-31 14:43:37
tags:laravel
---

## 环境（Mac）
### composer的安装
[Composer](https://getcomposer.org/download/)上介绍通过命令行安装未能成功，要不是下载过程超时就是过程中出错，最后还是采用手动下载方式。

具体步骤如下：

1. 通过页面Manual Download中提供的下载链接下载即可
2. 下载完后，将文件移动到`~/usr/local/bin`目录中，赋予可执行权限即可,可通过终端命令完成


	```
	sudo mv composer.phar /usr/local/bin/composer
	chmod +x /usr/local/bin/composer
	```
如果上面步骤都没错的话，则可以在终端使用composer命令了。

### Laravel的项目创建
[Laravel中文文档](http://www.golaravel.com/laravel/docs/5.1/)中提到两种方式来创建Laravel项目。一是通过Laravel安装器，另外一种就是通过composer，在此我选择了laravel安装器方式，因为文中提及此种方式更快。

通过`composer global require "laravel/installer"`全局安装laravel安装器，成功后还需进一步其执行文件的路径`~/.composer/vendor/bin`加入环境变量中，这时就可以在终端执行laravel命令了。

