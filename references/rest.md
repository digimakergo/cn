---
layout: page
title: REST
parent: 参考
permalink: /references/rest
nav_order: 15
has_doc: true
---

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Basis

**Examples**

Get content by id:
Request: `/content/get/3`
Response:
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
Get content list:
Request: `/content/list/folder?parent=3&level=1&sortby=priority%20desc%3Bmodified%20desc&limit=20&offset=0`
Response:
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

## Content fetch

### content/get

### content/version

### content/treemenu

### content/list

## Content operation

### content/create

### content/move

### content/update

### content/delete

### content/setpriority

## Authorization
### auth/auth

### auth/token/revoke

### auth/token/renew-refreshtoken

### auth/token/renew-accesstoken


## User
### user/current

### user/resetpassword

### user/resetpassword-confirm

### user/enable

## Content model
### contenttype/get

## Utility
### util/uploadfile

### util/uploadimage

