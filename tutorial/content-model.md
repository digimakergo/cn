---
layout: page
title: 内容基本概念
parent: 教程文章
permalink: /tutorial/content-model
nav_order: 1
---

Digimaker CMF的设计理念是, 通过一些模型配置(contenttype.json), 自动生成类似于ORM的实体(Enity), 然后通过api来操作这些Entity来操作数据. 这好像与一般web框架一样, 但Digimaker的基本数据类型是自带功能的. 

比如如果你定义一个数据类型是text(文本), 它在输入时自动就是个文本框(带验证功能), 如果你定义一个image(图片), 它在输入时自动是图片上传的界面且发布后自动存储图片路径. 如下是个后台管理界面, 里面所有的属性都是通过配置添加的, 当然你也可以创建自己的数据类型(我们叫域类型-fieldtype), 当然你可以调用前台api来显示数据, 而不需要管它是怎么存储的.


<img src="./eui-input.png" width="700px" />


典型的域类型有: 文本, 富文本, 图片, 数字, 时间, 关系(与其它内容关联起来).
