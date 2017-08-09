---
layout:     post
title:      "跟我一起学习ofbiz"
subtitle:   "切换MYSQL数据"
author:     "PYJ"
header-img: "static/img/post-bg-06.jpg"
catalog: true
tags:
    - ofbiz
---
##  准备
	1. perating system: Windows7 64 bit
	2. MySQL: mysql-5.5.23-winx64 (zip) - the topic is still valid for 32 bit version
	3. MySQL JDBC driver: mysql-connector-java-5.1.14-bin.jar - to be placed in <ofbiz-dir>/framework/entity/lib/jdbc
	4. OfBiz: ofbizCMS

##  MYSQL数据
	C:\mysql-5.5.23-winx64\bin>mysql -u root
	mysql>create database ofbiz;
	mysql>create database ofbizolap;
	mysql>create database ofbiztenant;
	mysql>use mysql;
	mysql>select database();
	mysql>create user ofbiz@localhost;
	mysql>create user ofbizolap@localhost;
	mysql>create user ofbiztenant@localhost;
	mysql>update user set password=PASSWORD("ofbiz") where User='ofbiz';
	mysql>update user set password=PASSWORD("ofbizolap") where User='ofbizolap';
	mysql>update user set password=PASSWORD("ofbiztenant") where User='ofbiztenant';
	mysql>grant all privileges on *.* to 'ofbiz'@localhost identified by 'ofbiz';
	mysql>grant all privileges on *.* to 'ofbizolap'@localhost identified by 'ofbizolap';
	mysql>grant all privileges on *.* to 'ofbiztenant'@localhost identified by 'ofbiztenant';

##  更改entity配置(frarework/entity/config/entityengine.xml)
	1.将delegator中引用的datasource-name的值设置为 localmysql：
	2. 配置mysql数据源连接，修改相关的字符集
		character-set="utf8" 
		collate="utf8_general_ci" 

##  其他：
    show grants for ofbiz@localhost;   查看权限
    flush  privileges ;  命令更新

##  高版本:
    update user set authentication_string=PASSWORD("ofbiz") where User='ofbizcms';
    
####  问题1:
	```java
	WARN: Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default if explicit option isn't set. For compliance with existing applications not using SSL the verifyServerCertificate property is set to 'false'. You need either to explicitly disable SSL by setting useSSL=false, or set useSSL=true and provide truststore for server certificate verification.
	```
	解决方案: (增加参数:&useSSL=false)
	url=jdbc:mysql://127.0.0.1:3306/framework?characterEncoding=utf8&amp;useSSL=false这就行了
	
####	问题2
	ubuntu16.04下mysql5.7支持utf-8编码格式配置文件修改步骤
	1，打开终端

	sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
	```
	 [mysqld]
	 #
	 # * Basic Settings
	 #
	 user            = MySQL
	 pid-file        = /var/run/mysqld/mysqld.pid
	 socket          = /var/run/mysqld/mysqld.sock
	 port            = 3306
	 basedir         = /usr
	 datadir         = /var/lib/mysql
	 tmpdir          = /tmp
	 lc-messages-dir = /usr/share/mysql

	 character-set-server=utf8 #增加这个设置
	 skip-external-locking
	 ```
	然后打开文件

	sudo vi /etc/mysql/conf.d/mysql.cnf
	```
	  [mysql]
	  default-character-set=utf8 #增加这个设置
	```

	/etc/init.d/mysql restart 
	最后重启服务就好了。

详情：[https://cwiki.apache.org/confluence/display/OFBIZ/How+to+migrate+OfBiz+from+Derby+to+MySQL+database](https://cwiki.apache.org/confluence/display/OFBIZ/How+to+migrate+OfBiz+from+Derby+to+MySQL+database "https://cwiki.apache.org/confluence/display/OFBIZ/How+to+migrate+OfBiz+from+Derby+to+MySQL+database")