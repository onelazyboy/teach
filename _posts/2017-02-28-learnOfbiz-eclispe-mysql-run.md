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
准备

    1. Operating system: Windows7 64 bit
    2. MySQL: mysql-5.5.23-winx64 (zip) - the topic is still valid for 32 bit version
    3. MySQL JDBC driver: mysql-connector-java-5.1.14-bin.jar - to be placed in <ofbiz-dir>/framework/entity/lib/jdbc
    4. OfBiz: ofbizCMS

MYSQL数据

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

更改entity配置(frarework/entity/config/entityengine.xml)
    `1.将delegator中引用的datasource-name的值设置为 localmysql：`

    2. 配置mysql数据源连接，修改相关的字符集
    character-set="utf8" 
    collate="utf8_general_ci" 
 
执行
    `ant clean-all;
    ant run-install;`


其他：
    `show grants for ofbiz@localhost;   查看权限`
    `flush  privileges ;  命令更新`






详情：[https://cwiki.apache.org/confluence/display/OFBIZ/How+to+migrate+OfBiz+from+Derby+to+MySQL+database](https://cwiki.apache.org/confluence/display/OFBIZ/How+to+migrate+OfBiz+from+Derby+to+MySQL+database "https://cwiki.apache.org/confluence/display/OFBIZ/How+to+migrate+OfBiz+from+Derby+to+MySQL+database")