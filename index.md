---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title: 首页
nav_order: 0
---

欢迎进入Digimaker CMF(内容管理框架)文档站点!

*说明: 本文档还在编写中, 产品还未发布(目前beta版, 但大部分接口已经定型了). 提问请联系QQ: 164076556, 然后联系人会给你发微信群二维码(因为二维码有时间限制只能这样)*

### 安装
最简单的安装方式是克隆并运行demo项目: [https://github.com/digimakergo/dmdemo](https://github.com/digimakergo/dmdemo), [中文说明](demo).


### 文章&教程 (正在添加)
 - [如何开发网站](tutorial/)
 - [如何使用客户端库(digimaker-ui)和rest api开发web应用](tutorial/)
 - [如何开发服务端(扩展rest api,Content handler, fieldtype)](tutorial/)
 - [内容模型以及如何配置](tutorial/content-model)
 - [在线日志/调试工具](tutorial/)
 - [用户登陆机制](tutorial/)


### [API接口](references/)
 - 模板: [模板](references/template)
 - 客户端/Rest API: [Rest API](references/rest), [客户端react库digimaker-ui](references/digimaker-ui)
 - 服务端: [Go API](references/go)
 - 配置文件: [dm.yaml](references/dm), [contenttype.json](references/contenttype), [template_override.yaml](references/template-override), [policies.yaml](references/policies)

### 后台管理(后台编辑界面/eui)
如下是eui的基本界面, 界面可定制, 如工具, 显示哪些, 列表表, 主题等. 你也可以添加自定义的功能.

<a href="https://raw.githubusercontent.com/digimakergo/eui/master/doc/eui-1.png"><img src="https://raw.githubusercontent.com/digimakergo/eui/master/doc/eui-1.png" width="700px" /></a>

[定制eui](eui/)

### 路线图

我们正在快速迭代, 看我们的[路线图](roadmap), 你可得到下一步的功能.

### 感谢
特别感谢模板库 [Pongo2](https://github.com/flosch/pongo2), 还有高性能数据库库 [SQL Boiler](https://github.com/volatiletech/sqlboiler). 

