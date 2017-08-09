---
layout:     post
title:      "跟我一起学习ofbiz"
subtitle:   "mysql,ubuntu"
author:     "PYJ"
header-img: "static/img/post-bg-06.jpg"
catalog: true
tags:
    - ofbiz
    - ubuntu
    - phpmyadmin
    - LAMP
---
##	安装LAMP
LAMP是Linux、Apache、MySql（MariaDB）、PHP（Python、Perl）等软件的合称。

我们现在要在Ubuntu16.04上安装，因此只需要安装其他三个软件就可以了。
```
sudo apt install mysql-server-5.7 mysql-client-5.7 php7.0 apache2
```
对于这些软件可能还需要各自进行配置，这里就不再细述了

##	启用PHP支持
然后安装apache的php扩展：
```
sudo apt install libapache2-mod-php7.0
```
安装完成之后需要重启apache：
```
sudo systemctl restart apache2
```
然后在apache的默认目录中新建一个PHP文件：
```
sudo nano /var/www/html/info.php
```
文件内容如下：
```php
<?php
phpinfo();
?>
```
然后在浏览器中查看一下是否成功：info (http://localhost/info.php)。 

成功之后别忘了删除info.php，它包含了很多服务器的敏感信息。
```
sudo rm -f /var/www/html/info.php
```

##	启用SSL：
```
sudo a2enmod ssl
sudo a2ensite default-ssl
```

##	启用PHP扩展
安装所需的PHP扩展，也可以全部安装，全部安装可能会降低性能：
```
sudo apt -y install php7.0-mysql php7.0-curl php7.0-gd php7.0-intl php-pear php-imagick php7.0-imap php7.0-mcrypt php-memcache  php7.0-pspell php7.0-recode php7.0-sqlite3 php7.0-tidy php7.0-xmlrpc php7.0-xsl php7.0-mbstring php-gettext
```
然后重启apache：
```
sudo systemctl restart apache2
```
##	安装APCu

APCu是一个缓存扩展，可以缓存并优化PHP中间代码，强烈建议安装。
```
sudo apt -y install php-apcu
```
然后重启apache：
```
sudo systemctl restart apache2
```
##	安装phpmyadmin

上面的工作全部完成之后，就可以安装phpmyadmin了。
```
sudo apt -y install phpmyadmin
```
##	其他问题
安装完成后，去服务器目录下检查( /var/www/html)，发现并没有phpmyadmin

系统在安装软件时，默认将软件安装在了/usr/share/下(ls -a | grep phpmyadmin)，

所以你的phpmyadmin在/usr/share下可以找到

所以必须建立一个软连接，使得第三步中显示的文件和/var/www/html下的某个文档链接起来，

回到/var/www/html，输入一下代码
```
sudo ln -s /usr/share/phpmyadmin phpmyadmin
```

##	结尾
会出现一个图形界面要求你输入各种配置选项。全部配置完成之后，在浏览器中输入http://localhost/phpmyadmin/，应该就可以进入phpmyadmin的界面了。如果有些步骤没有按照顺序来，可能无法顺利打开这个web界面，这时候可以先把前面的工作都完成，然后运行一下sudo dpkg-reconfigure phpmyadmin命令，重新配置一遍phpmyadmin。然后应该就能顺利打开了。

成功进入web界面之后，就可以利用图形化方式对mysql进行各种配置了。这里就不再详细说明了。
