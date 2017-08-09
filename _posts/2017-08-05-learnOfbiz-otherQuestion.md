---
layout:     post
title:      "跟我一起学习ofbiz"
subtitle:   "问题整理"
author:     "PYJ"
header-img: "static/img/post-bg-06.jpg"
catalog: true
tags:
    - ofbiz
---
##  在jdk从1.5升级到1.6的时候控制台出现以下错误
```
[Java](http://lib.csdn.net/base/java).lang.NoSuchMethodError: org.eclipse.jdt.internal.compiler.CompilationResult.getProblems()[Lorg/eclipse/jdt/core/compiler/IProblem;
at org.apache.jasper.compiler.JDTCompiler$2.acceptResult(JDTCompiler.java:341)
```
####  解决办法如下：
jdk从5升级到6,已经使用新的类进行编译，以前的工程中有的jar包，可能会引起编译的莫明其妙的错误
去掉web应用中的jasper-runtime-5.5.9.jar，jasper-compiler-5.5.9.jar之后，运行正常.

##  问题描述
```java
ofbiz.base.start.StartupException: Cannot start() org.ofbiz.commons.vfs.CommonsVfsContainer (Initializing StandardFileSystemManager (Could not load VFS configuration from "file:/D:/object/ofbiz/bin/META-INF/vfs-providers.xml".))at org.ofbiz.base.[Container](http://lib.csdn.net/base/docker).ContainerLoader.start(ContainerLoader.java:103)at org.ofbiz.base.start.Start.startStartLoaders(Start.java:263)at org.ofbiz.base.start.Start.startServer(Start.java:312)at org.ofbiz.base.start.Start.start(Start.java:316)at org.ofbiz.base.start.Start.main(Start.java:399)org.ofbiz.base.container.ContainerException: Initializing StandardFileSystemManager (Could not load VFS configuration from "file:/D:/object/ofbiz/bin/META-INF/vfs-providers.xml".)at org.ofbiz.commons.vfs.CommonsVfsContainer.start(CommonsVfsContainer.java:48)at org.ofbiz.base.container.ContainerLoader.start(ContainerLoader.java:101)at org.ofbiz.base.start.Start.startStartLoaders(Start.java:263)at org.ofbiz.base.start.Start.startServer(Start.java:312)at org.ofbiz.base.start.Start.start(Start.java:316)at org.ofbiz.base.start.Start.main(Start.java:399)Caused by: org.apache.commons.vfs.FileSystemException: Could not load VFS configuration from "file:/D:/object/ofbiz/bin/META-INF/vfs-providers.xml".at org.apache.commons.vfs.impl.StandardFileSystemManager.configure(StandardFileSystemManager.java:199)at org.apache.commons.vfs.impl.StandardFileSystemManager.configurePlugins(StandardFileSystemManager.java:156)at org.apache.commons.vfs.impl.StandardFileSystemManager.init(StandardFileSystemManager.java:129)at org.webslinger.commons.vfs.VFSUtil.createStandardFileSystemManager(VFSUtil.java:351)at org.webslinger.commons.vfs.VFSUtil.createStandardFileSystemManager(VFSUtil.java:345)at org.ofbiz.commons.vfs.CommonsVfsContainer.start(CommonsVfsContainer.java:43)... 5 moreCaused by: org.apache.commons.vfs.FileSystemException: Multiple providers registered for URL scheme "ofbiz-home".at org.apache.commons.vfs.impl.DefaultFileSystemManager.addProvider(DefaultFileSystemManager.java:174)at org.apache.commons.vfs.impl.StandardFileSystemManager.addProvider(StandardFileSystemManager.java:362)at org.apache.commons.vfs.impl.StandardFileSystemManager.configure(StandardFileSystemManager.java:262)at org.apache.commons.vfs.impl.StandardFileSystemManager.configure(StandardFileSystemManager.java:195)... 10 moreorg.ofbiz.base.container.ContainerException: Initializing StandardFileSystemManager (Could not load VFS configuration from "file:/D:/object/ofbiz/bin/META-INF/vfs-providers.xml".)at org.ofbiz.commons.vfs.CommonsVfsContainer.start(CommonsVfsContainer.java:48)at org.ofbiz.base.container.ContainerLoader.start(ContainerLoader.java:101)at org.ofbiz.base.start.Start.startStartLoaders(Start.java:263)at org.ofbiz.base.start.Start.startServer(Start.java:312)at org.ofbiz.base.start.Start.start(Start.java:316)at org.ofbiz.base.start.Start.main(Start.java:399)Caused by: org.apache.commons.vfs.FileSystemException: Could not load VFS configuration from "file:/D:/object/ofbiz/bin/META-INF/vfs-providers.xml".at org.apache.commons.vfs.impl.StandardFileSystemManager.configure(StandardFileSystemManager.java:199)at org.apache.commons.vfs.impl.StandardFileSystemManager.configurePlugins(StandardFileSystemManager.java:156)at org.apache.commons.vfs.impl.StandardFileSystemManager.init(StandardFileSystemManager.java:129)at org.webslinger.commons.vfs.VFSUtil.createStandardFileSystemManager(VFSUtil.java:351)at org.webslinger.commons.vfs.VFSUtil.createStandardFileSystemManager(VFSUtil.java:345)at org.ofbiz.commons.vfs.CommonsVfsContainer.start(CommonsVfsContainer.java:43)... 5 moreCaused by: org.apache.commons.vfs.FileSystemException: Multiple providers registered for URL scheme "ofbiz-home".at org.apache.commons.vfs.impl.DefaultFileSystemManager.addProvider(DefaultFileSystemManager.java:174)at org.apache.commons.vfs.impl.StandardFileSystemManager.addProvider(StandardFileSystemManager.java:362)at org.apache.commons.vfs.impl.StandardFileSystemManager.configure(StandardFileSystemManager.java:262)at org.apache.commons.vfs.impl.StandardFileSystemManager.configure(StandardFileSystemManager.java:195)... 10 more2010-03-20 14:50:20,898 (OFBiz_Shutdown_Hook) [     ContainerLoader.java:114:INFO ] Shutting down containersjava.lang.NullPointerExceptionat org.ofbiz.service.rmi.RmiServiceContainer.stop(RmiServiceContainer.java:169)at org.ofbiz.base.container.ContainerLoader.unload(ContainerLoader.java:122)at org.ofbiz.base.start.Start.shutdownServer(Start.java:301)at org.ofbiz.base.start.Start.access$0(Start.java:295)at org.ofbiz.base.start.Start$2.run(Start.java:278)
```
####  解决办法
把\framework\base\config\ofbiz-containers.xml中的这两行注释掉：    
 <container name="commons-vfs-container" class="org.ofbiz.commons.vfs.CommonsVfsContainer"/>    
 <container name="webslinger-container" class="org.ofbiz.webslinger.WebslingerContainer"/>

原文: http://blog.csdn.net/marcsterling/article/details/9051833