---
layout: page
title: contenttype.json
parent: 参考
permalink: /references/contenttype
nav_order: 50
---

# contenttype.json


<details open markdown="block">
  <summary>
    内容列表
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

### 例子

文章
```json

"article": {
    "name": "文章",
    "table_name": "dm_article",
    "has_version": true,
    "has_location": true,
    "name_pattern": "{title}",
    "fields": [{
        "identifier": "title",
        "type": "text",
        "name": "标题",
        "required": true
      },     
      {
        "identifier": "coverimage",
        "type": "image",
        "name": "封面",
        "required": false
      },
      {
        "identifier": "summary",
        "type": "richtext",
        "name": "简介",
        "required": false,
        "parameters": {
          "mode":"compact"
        }
      },
      {
        "identifier": "body",
        "type": "richtext",
        "name": "内容",
        "required": false
      },
      
```
图片
```json
"image": {
    "name": "图片",
    "table_name": "dm_image",
    "has_version": false,
    "has_location": false,
    "data_fields":[ {"identifier":"location_id", "fieldtype":"int"}, {"identifier":"author", "fieldtype":"int"}, {"identifier":"published", "fieldtype":"int"}, {"identifier":"modified", "fieldtype":"int"}, {"identifier":"cuid", "fieldtype":"string"}],
    "fields": [
      {
        "identifier": "name",
        "type": "text",
        "name": "名称",
        "required": true
      },
      {
        "identifier": "image",
        "type": "image",
        "name": "图片",
        "required": true
      }
    ]
  }
```

### 内容类型配置

| 属性        | 描述           | 
| ------------- |-------------|
| name      | 内容类型名 | 
| table_name      | 数据表名      |  
| has_version | 是否有版本, 如有, 发布时会自动保存到版本信息      |   
| has_location | 是否有位置, 如果此内容不需要多位置的话(比如图片), 可以用false |
| name_pattern | 生成的名字模式, 可直接使用属性名作为变量 例如: "{title}"或"{firstname} {lastname}"|
| fields|包含的域(digimaker域类型的域, 如文本(text)) |
| data_fields|包含的数据类型域(基本数据类型的域, 如string)|

### 内容域/属性(fields)配置

| 属性        | 描述           | 
| ------------- |-------------|
| identifier      | 标识符, 只能用小写+下划线 | 
| type      | 类型      |  
| name | 属性名      |   
| is_output|是否是输出属性, 作为表单的头时有用如需要用到h2时|
| required | 是否是必须的 |
| parameters | 参数, 根据域类型不一样参数不一样, 详见各域类型 |
| validation | 验证信息, 根据哉类型不一样参数不一样 |

### 目前支持的域类型

| 类型       | 描述           | 可使用参数 | 
| ------------- |-------------|-------|
| text      | 文本 |  | 
| richtext      | 富文本 | "mode":"compact/full", 简易模式或全模式, 默认全模式 |
| datetime      | 时间日期 | "dateonly": true/false | 
| container      | 容器, 一个用于包含其它域的类型 |  |
| checkbox      | 复选框 |  |
| relation      | 一个关系, 比如一本书的出版商 | "type": "<如publisher>" - 只能是出版商与本内容关联 |
| relationlist  | 多个关系, 比如文章要关系多张图片时 | "type": "<如image>" - 只能是图片与本内容关联 |

***(更多类型的文档正在添加)***


