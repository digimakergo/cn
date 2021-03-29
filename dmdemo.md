---
layout: page
title: Demo项目
permalink: /demo/
nav_order: 0
---


运行demo
-------

#### 系统需求:
- Go version >= 1.2(recommand >= 1.3)
- Mysql database(其它数据库正在进行中)
- npm(dev only)

#### 前端
```sh
 //clone
 git clone https://github.com/digimakergo/dmdemo.git

 //导入数据
 //remember to change configs/dm.yaml's database connection.
 mysql -u {username} -p {database} < data/dmdemo.sql

 //启动服务器
 dmapp=. go run cmd/main.go
```
  访问: http://localhost:9200

Build前台web app

```sh
   cd web/app
   npm install
   npm run build
   (or just "npm start" and visit http://localhost:3000)
```
  访问: http://localhost:9200/mypage

  (登陆信息: `member/digimaker`)


 #### 后端
  建议把eui放在dmdemo/web下, 详见本文章底端的说明
  ```sh
   git clone https://github.com/digimakergo/eui.git
   cd eui
   npm install
   npm start
   ```
查看后台: http://localhost:3000 登陆信息: `admin/Digimaker`


开发
-------

### 网站, 模板

First you need to define a template override rule under [configs/template_override.yaml](https://github.com/digimakergo/dmdemo/blob/master/configs/template_override.yaml) (and template_override-dmdemo.yaml), then you can do the templating in that template file.  

Example:
- [Display a folder](https://github.com/digimakergo/dmdemo/tree/master/web/templates/demo/folder/full.html)
- [Display frontpage](https://github.com/digimakergo/dmdemo/tree/master/web/templates/demo/folder/frontpage.html)
- [Layout](https://github.com/digimakergo/dmdemo/tree/master/web/templates/demo/base.html)

Check docs to see all template override rules: [https://digimaker.org/doc/references/template-override](https://digimaker.org/doc/references/template-override)

Check docs to see all references: [https://digimaker.org/doc/references/template](https://digimaker.org/doc/references/template)


### Web应用
See [web/app](web/app) for examples.

- [Photos.tsx](web/app/src/Photos.tsx) Shows how to query images, add content(image) using rest api
- [Profile.tsx](web/app/src/Profile.tsx) Shows how to show/edit content(user) using components in digimaker-ui
- [Login.tsx](web/app/src/Login.tsx) Shows how to get authorization token using rest api

Check docs to see rest api: [https://digimaker.org/doc/references/rest](https://digimaker.org/doc/references/rest)

Check docs to see full react components: [https://digimaker.org/doc/references/digimaker-ui](https://digimaker.org/doc/references/digimaker-ui)


### 权限配置
The permission policies is defined under [policies.json](configs/policies.json), and then connect to role and user in the content. policies.json defines permission like
 - fetching  based on content type, parent,etc
 - operations(eg. create content, update, delete) based on content type, parent, author(self)
 - updated fields when updating - attribute level permission
 - non-content operation like login, left menu of eui, etc

Example on policies.json:
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

Check docs to see policies configuration: [https://digimaker.org/doc/references/policies](https://digimaker.org/doc/references/policies)

### 内容模型
Digimaker defines content model in file and generates entities based on the definition. Developers use those entities to manipulate content similar to ORM.

[contenttype.json](configs/contenttype.json) defines content model. If there is changes on contenttype.json, run below so it can generate entities under entity folder

```
cd dmdemo
dmapp=. go run /Users/xc/go/src/github.com/digimakergo/digimaker/codegen/contenttypes/gen.go
```

Default output example after run

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

A project structure example which follows some recommendation from Go standard project layout: https://github.com/golang-standards/project-layout

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

- cmd/main.go which is the starting point. It can be any nam&any structure as long as it can run as entry point.
- configs
   - dm.yaml: main configuration
   - contenttype.yaml: content model configuration
   - policies.yaml: policies configuration for permission related
   - [optional]temlate_override.yaml (only needed if you use templating)
- entity: generated ORM-like entities
- [optional]handlers: callback for events
- [optional]fieldtype: if you have custom fieldtype
- [optional]web/templates: only needed if you need templating for website
- [optional]rest/api: can be use for rest api
- [optional]var for generated web resources(eg. uploaded images): It doesn't need to be under this directory(configurable in dm.yaml) as long as it's visitable from web(for instance via nginx).

Note: all the .go related folders can be in any structure as long as they can be imported. The only required structure for Digimaker is the config files structure.
