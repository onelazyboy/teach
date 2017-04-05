---
layout: post
title: OFBiz进阶--OFBiz配置之[widget.properties]分析(装饰器) 
tags: OFBiz widget
categories: OFBiz
---


```
#compress.HTML=true
#--压缩生成的HTML页面代码
```
```
widget.verbose=true
#--开启页面冗余, 可控制screen生成的页面自动创建的注释代码(由哪些文件构造成功的文件路径)
```
```
widget.form.defaultViewSize=20
 #--分页的页面默认查看数据的条数
```
```
widget.autocompleter.defaultViewSize=10
 #--页面自动完成控件默认的字符长度
```
```
widget.autocompleter.defaultMinLength=2
#--页面自动完成控件默认启动自动完成功能的最小字符长度
```
```
widget.autocompleter.displayReturnField=Y
#--自动完成的返回值显示方式开关, 实现方式如下
<#if ("Y" == displayReturnField)>
    <#assign displayString = displayString +  "[" + returnField + "]">
</#if>
```
```
widget.lookup.showDescription=Y
#--Form中的lookup控件显示标签 tooltip 属性默认显示查到的结果值
```
```
widget.form.defaultTextFindOption=contains
#--查询表单输入框默认查询方式为 包含
```
```
widget.form.displayhelpText=Y
#--form中field标签tooltip属性雷同与title属性值
```
```
widget.defaultNoConditionFind=N
#--查询功能的noConditionFind属性默认值为 N
```
```
# html output
#--HTML类型的显示界面用到的 宏 资源文件路径配置如下:
```
```
screen.name=html
 #--宏 资源文件 类型
```
```
screen.screenrenderer=component://widget/templates/htmlScreenMacroLibrary.ftl
 #--页面构造器标签 宏 资源
```
```
screen.formrenderer=component://widget/templates/htmlFormMacroLibrary.ftl
#--表单构造器标签 宏 资源
```
```
screen.menurenderer=component://widget/templates/htmlMenuMacroLibrary.ftl
#--菜单构造器标签 宏 资源
```
```
screen.treerenderer=component://widget/templates/htmlTreeMacroLibrary.ftl
#--目录树构造器标签 宏 资源
```
```

screen.encoder=html
#--默认页面生成文件类型为 HTML
```
```
screen.compress=false
#--不开启生成的HTML页面代码压缩功能
```
```
screen.default.contenttype=UTF-8
#--生成的HTML页面代码编码类型
```
```
screen.default.encoding=none
 #--生成的HTML页面代码编码格式
```     
[原文地址][1]
  [1]: http://ofbizer.iteye.com/blog/2030198