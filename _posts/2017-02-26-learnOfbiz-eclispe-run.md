---
layout:     post
title:      "跟我一起学习ofbiz"
subtitle:   "项目eclipse启动"
author:     "PYJ"
header-img: "static/img/post-bg-06.jpg"
catalog: true
tags:
    - ofbiz
---

通过eclipse导入ofbizCms（运行时错误及解决方案） 

----------

**1. Can't find bundle for base name cache, locale en**

    Exception in thread "main" java.lang.ExceptionInInitializerError
    	at org.ofbiz.base.util.Debug.<clinit>(Debug.java:86)
    	at org.ofbiz.base.container.ContainerLoader.load(ContainerLoader.java:78)
    	at org.ofbiz.base.start.Start.initStartLoaders(Start.java:169)
    	at org.ofbiz.base.start.Start.init(Start.java:139)
    	at org.ofbiz.base.start.Start.main(Start.java:69)
    Caused by: java.util.MissingResourceException: Can't find bundle for base name cache, locale en
    	at java.util.ResourceBundle.throwMissingResourceException(Unknown Source)
    	at java.util.ResourceBundle.getBundleImpl(Unknown Source)
    	at java.util.ResourceBundle.getBundle(Unknown Source)
    	at org.ofbiz.base.util.cache.UtilCache.setPropertiesParams(UtilCache.java:212)
    	at org.ofbiz.base.util.cache.UtilCache.setPropertiesParams(UtilCache.java:208)
    	at org.ofbiz.base.util.cache.UtilCache.<init>(UtilCache.java:138)
    	at org.ofbiz.base.util.cache.UtilCache.createUtilCache(UtilCache.java:1015)
    	at org.ofbiz.base.util.UtilProperties.<clinit>(UtilProperties.java:71)
    	... 5 more
    
![](http://ww1.sinaimg.cn/large/71be7325ly1fd3ycrv49aj21110k777e)


----------

2.Cannot start() org.ofbiz.commons.vfs.CommonsVfsContainer (Initializing StandardFileSystemManager (Could not load VFS configuration from "jar:file:/E:/Ofbiz/ofbiz-cms/framework/webslinger/lib/webslinger-20091211-3897-7ab22baea4b6.jar!/META-INF/vfs-providers.xml".))

![](http://ww1.sinaimg.cn/large/71be7325ly1fd3ycrv4aoj20xo0emq52)


----------

3.java.lang.noclassdeffounderror: org/eclipse/birt/core/framework/eclipse/eclipseextensionregistry
2017/2/26 17:33:12 
关于此问题jar冲突，缺少
需从官网重新下载 [birt-runtime-2_6_2.zip](http://archive.eclipse.org/birt/downloads/build.php?build=R-R1-2_6_2-201102191842 "下载地址") 解压，copy WebViewerExample\WEB-INF\lib 中jar 置 E:\Ofbiz\ofbiz-cms\framework\birt\lib 即可解决


