---
layout: page
title: 演示项目
permalink: /demo/
nav_order: 2
---

***(注: 本demo还在改进, 界面和功能会有变化)***

运行demo
-------

**系统需求:**
- Go version >= 1.2(推荐>= 1.3)
- Mysql(其它数据库的支持正在开发中)
- npm(只需开发时用)

### 安装, 运行
```sh
 //clone
 git clone https://github.com/digimakergo/dmdemo.git

 //建议运行如下命令(只用于发布前的beta版)
 go get -u github.com/digimakergo/digimaker

 //建数据库并导入数据
 //注: 同时要修改configs/dm.yaml数据库连接信息.
 mysql -u {username} -p {database} < data/dmdemo.sql

 //启动服务器, 注: windows - 因windows不支持命令行集成环境变量, 须把环境变量dmapp设置到dmdemo目录, 然后运行go run cmd/main.go
 dmapp=. go run cmd/main.go
```

### 访问网站
  访问: [http://localhost:9200](http://localhost:9200)
  
  <a href="../assets/images/dmdemo-site.png"><img src="../assets/images/dmdemo-site.png" width="600px"/></a>

### 访问前台web app

```sh
   cd web/app
   npm install
   npm run build
   (或者直接 "npm start" 然后访问http://localhost:3000)
```
  访问: [http://localhost:9200/mypage](http://localhost:9200/mypage) (登陆信息: `member/digimaker`) 以下是大致截图: 
  
  <a href="../assets/images/dmdemo-login.png"><img src="../assets/images/dmdemo-login.png" width="600px"/></a>
  
  <a href="../assets/images/dmdemo-photo.png"><img src="../assets/images/dmdemo-photo.png" width="600px"/></a>

  <a href="../assets/images/dmdemo-add.png"><img src="../assets/images/dmdemo-add.png" width="600px"/></a>
  
### 运行后台(管理员界面)
 
  建议把eui放在dmdemo/web下, 详见本文章底端的说明
  ```sh
   git clone https://github.com/digimakergo/eui.git
   cd eui
   npm install
   npm start
   ```
查看后台: [http://localhost:3000](http://localhost:3000) 登陆信息: `admin/Digimaker`


代码说明
-------

### 网站, 模板

模板例子:
- [显示文件夹](https://github.com/digimakergo/dmdemo/tree/master/web/templates/demo/folder/full.html)
- [显示首页](https://github.com/digimakergo/dmdemo/tree/master/web/templates/demo/folder/frontpage.html)
- [布局](https://github.com/digimakergo/dmdemo/tree/master/web/templates/demo/base.html)

如何配置模板: [https://digimaker.org/doc/references/template-override](https://digimaker.org/cn/references/template-override)

模板文档: [https://digimaker.org/doc/references/template](https://digimaker.org/cn/references/template)


### Web应用

- [Photos.tsx](https://github.com/digimakergo/dmdemo/tree/master/web/app/src/Photos.tsx) 演示了如何通过res api查询, 显示内容(图片)
- [Profile.tsx](https://github.com/digimakergo/dmdemo/tree/master/web/app/src/Profile.tsx) 演示了如何通过digimaker-ui的api显示和编辑内容(用户)
- [Login.tsx](https://github.com/digimakergo/dmdemo/tree/master/web/app/src/Login.tsx) 演示了如何用认证的api来登陆

rest api: [https://digimaker.org/doc/references/rest](https://digimaker.org/doc/references/rest)

react组件digimaker-ui: [https://digimaker.org/doc/references/digimaker-ui](https://digimaker.org/doc/references/digimaker-ui)


### 权限配置
所有权限的策略信息都配置在[policies.json](configs/policies.json), 然后策略会通过后台界面关联到角色, 然后到用户上. policies.json可定义如下权限 
 - 查询哪些类型的内容, 哪个节点下的, 作者是谁等
 - 内容操作(创建/更新/删除) : 哪些类型, 在哪个节点下, 作者是否是自己等
 - 更新哪些属性 - 属性级别的权限
 - 非内容相关的权限, 如登陆, 后台界面的左栏菜单等.

以下是个例子:
```json
  {
    "operation": ["content/update", "content/read"],
    "limited_to": {
      "contenttype": ["article"],
      "author": "self"
    }
  },
  {
      "operation": ["content/create"],
      "limited_to": {
      "contenttype": ["image"],
      "under": [461]
   }
  }
```

policies配置文档: [https://digimaker.org/doc/references/policies](https://digimaker.org/doc/references/policies)

### 内容模型
Digimaker首先定义内容模型, 然后根据定义的模型生成类似于ORM里的实体(entity).

内容模型定义在[contenttype.json](configs/contenttype.json). 如果模型有更新, 可以通过运行如下命令来生成实体.

```
cd dmdemo
dmapp=. go run /Users/xc/go/src/github.com/digimakergo/digimaker/codegen/contenttypes/gen.go
```

默认会输出如下信息

```
Generating content entities for /Users/xc/go/src/github.com/digimakergo/dmdemo
Generating article
Generating usergroup
Generating role
Generating user
Generating image
Generating file
Generating folder
Generating frontpage
```


部署
----------

项目结构
-------

项目结构参考了go的项目布局建议: https://github.com/golang-standards/project-layout

```
Project A
│───cmd
│     └─main.go
│──configs    
│     │─dm.yaml
│     │─contenttype.yaml
│     │-policies.yaml
│     └ template_override.yaml
│──entity
│──handlers
│──api
│──web
│  └templates
│
└───var
```

- cmd/main.go 启动文件
- configs
   - dm.yaml: 主要配置文件
   - contenttype.yaml: 数据模型配置
   - policies.yaml: 权限策略配置
   - [可选]temlate_override.yaml (模板覆盖规则)
- entity: 自动生成的像ORM实体
- [可选]handlers: 回调go代码
- [可选]fieldtype: 自定义域类型
- [可选]web/templates: 模板
- [可选]rest/api: 远程rest api
- [可选]var 生成的资源(如上传的图片, 文件等), 在production建议用外部web服务器(如nginx)来托管这个文件夹
