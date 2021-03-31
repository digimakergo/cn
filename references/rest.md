---
layout: page
title: 远程访问rest
parent: 参考
permalink: /references/rest
nav_order: 15
has_doc: true
---

***注: 本文档还在编写中***

<details open markdown="block">
  <summary>
    内容列表
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## 基本用法

**例子**

通过id获取内容:
请求: `/content/get/3`
返回:
```json
{
  "cid": 3,
  "version": 0,
  "published": 1560534450,
  "modified": 1615464230,
  "cuid": "bk1trcli6ekibbmo2cj0",
  "status": 1,
  "author": 1,
  "author_name": "Administrator Admin",
  "relations": {},
  "folder_type": "site",
  "summary": "<p>This is a demo site.</p>",
  "title": "Demo",
  "id": 3,
  ...
}
```
取得内容列表:
请求: `/content/list/folder?parent=3&level=1&sortby=priority%20desc%3Bmodified%20desc&limit=20&offset=0`
返回:
```json
{
  "list": [
    {
      "cid": 28,
      "version": 0,
      "published": 1614682043,
      "modified": 1614682043,
      "cuid": "c0v1feuvvhfup2usch5g",
      "status": 0,
      "author": 1,
      "author_name": "Administrator Admin",
      ...
    },
    {
      "cid": 27,
      "version": 0,
      "published": 1614682022,
      "modified": 1614682022,
      "cuid": "c0v1f9mvvhfup2usch4g",
      "status": 0,
      "author": 1,
      "author_name": "Administrator Admin",
      ...
    }
  ],
  "count": 2
}
```

## 查询内容

### content/get

### content/version

### content/treemenu

### content/list

## 操作内容

### content/create

### content/move

### content/update

### content/delete

### content/setpriority

## 用户认证
### auth/auth

### auth/token/revoke

### auth/token/renew-refreshtoken

### auth/token/renew-accesstoken


## 用户相关
### user/current

### user/resetpassword

### user/resetpassword-confirm

### user/enable

## 内容模型
### contenttype/get

## 工具
### util/uploadfile

### util/uploadimage

