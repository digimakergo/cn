---
layout: page
title: Go api
parent: 参考
permalink: /references/go
nav_order: 20
has_toc: true
---

以下是Go API预览, 查看[自动生成的api文档](https://pkg.go.dev/github.com/digimakergo/digimaker#section-documentation)

<details open markdown="block">
  <summary>
    内容列表
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## 获取内容
包 core/query

注: 所有的查询都会使用像下面的条件语法

```go
ids := []int{3, 4, 5, 7, 9, 10}
condition := db.Cond("id", ids).Cond("l.depth", 2).Cond("author", 1).Sortby("modified desc").Limit(0, 2)
```

### 查询一个内容

| Function        | Description       
|:-------------|:---------------------|
| [FetchByID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#FetchByID)       |  通过id(location id)查询一个内容  |
| [FetchByCID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#FetchByCID)     |  通过内容id查询一个内容  |
| [Fetch](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#Fetch)           |   通过条件查询一个内容  |
| [FetchByUID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#FetchByUID)     |  通过location唯一标识符查询一个内容  |
| [FetchByCUID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#FetchByCUID)   |  通过内容唯一标识符查询一个内容  |


### 查询列表

| Function        | Description       
|:-------------|:---------------------|
| [SubList](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#SubList)       |  查询子内容列表, 考虑权限  |
| [ListWithUser](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#ListWithUser)  | 查询子内容列表, 考虑权限 |
| [Children](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#Children)      |  查询直接子内容列表(只有一层),考虑权限  |
| [List](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#List)     |  查询列表, 不考虑权限  |

### 查询子树

| Function        | Description       
|:-------------|:---------------------|
| [SubTree](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#SubTree)        |  查询子树  |

### 查询用户角色

| Function        | Description       
|:-------------|:---------------------|
| UserRole  |  查询用户角色 |

## 操作内容
包core/handler

**操作内容**

| Function        | Description       
|:-------------|:---------------------|
| [Create](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.Create)        |  创建内容 |
| [Update](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.Update)        |  更新内容 |
| [Move](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.Move)        |  移动内容 |
| [DeleteByID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.DeleteByID)        |  根据id删除内容 |
| [DeleteByCID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.DeleteByCID)        |  根据内容id删除内容 |
| [DeleteByContent](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.DeleteByContent)        | 删除一个已经给的内容 |


**用户**

| Function        | Description       
|:-------------|:---------------------|
| [CanLogin](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#CanLogin)        |  查看用户是否能登陆 |
| [Enable](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#Enable)        |  启用/禁用用户 |

## 权限
包 core/permission

| Function        | Description       
|:-------------|:---------------------|
| [HasAccessTo](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#HasAccessTo)        |  Check if a user can accces to a operation |
| [CanRead](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#CanRead)        |  Check if a user can read a content |
| [CanUpdate](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#CanUpdate)        |  Check if a user can update a content |
| [CanDelete](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#CanDelete)        |  Check if a user can delete a content |
| **Fetch policies and access**        |   |
| [GetUserAccess](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#GetUserAccess)        |  Get user limit list|
| [GetUserPolicies](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#GetUserPolicies)        |  Get user polices|
| **Operations**| |
| [AssignToUser](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#AssignToUser)        |  Assign a role to a user|
| [RemoveAssignment](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#RemoveAssignment)        |  Remove the assignment of user role|

## 数据库
包 core/db


### 条件

一个条件包含如下信息: 属性, 操作, 值(例如. "id > ", 10). 操作 '=', 'in'可忽略. 值可以是基本数据类型, 也可以是struct, 但需要实现[database.sql.driver.Valuer](https://golang.org/pkg/database/sql/driver/#Valuer)接口.


目前支持的操作: `">", ">=", "<", "==", "<=", "!=", "=", "in", "like"`. 

*注: "==" 用于连接查询.*

多个条件时使用面向方法的使用风格:

```go
//Below 2 are the same. Note: when using 'in/like' there should be a space before the operator
db.Cond("id>", ids)
db.Cond("id >", ids)

//id equals 3
db.Cond("id", 3)

//id in 1, 3
db.Cond("id", []int{1, 3})

//id in 1, 3 and author is 1
db.Cond("id", []int{1, 3}).Cond("author", 1)
```

[Check here to see typical condition examples.](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#example-Cond)

| Function        | Description       
|:-------------|:---------------------|
| [Cond](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Cond)        |  Create a condition |
| [EmptyCond](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#EmptyCond)        |  Empty condition |
| [TrueCond](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#TrueCond)        |  Always true |
| [FalseCond](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#FalseCond)        |  Always false |
| **Condition struct**| |
| [Cond](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Condition.Cond)     |  Same as And&Cond combined |
| [And](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Condition.And)   | Same as And with itself as first parameter |
| [Or](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Condition.Or)    | Same as Or with itself as first parameter |
| [Sortby](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Condition.Sortby)        |  Sort by |
| [Limit](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Condition.Limit)        |  Limit |
| [WithCount](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Condition.WithCount)   |  Always include count in result regarless limit |

### 数据库层面的查询
There are 2 types of entities: content entities and normal entities. A content entity can be a combination from different tables. A typical normal entity is from a table.

Most of content related query can be done via apis in [core/query](#package-corequery).

If you want to fetch normal table data, `BindEntity` is the way to go. You can create a struct or anonymous struct to bind into. There is also a `db.Datamap` and `DatamapList` which can be used for binding entities to a maplist or map. Check `BindEntity` link in below table to see examples.

| Function        | Description       
|:-------------|:---------------------|
| [BindContent](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#BindContent)        |  Bind content(s) with a condition |
| [CountContent](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#CountContent)        |  Count content(s) with a condition |
| [BindEntity](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#BindEntity)        |  Bind entity(s) with a condition |
| [Count](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Count)        |   Count entity with a condition |
| [BindContentWithQuery](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#BindContentWithQuery)        |  Bind conentent(s) with a query|
| [BindEntityWithQuery](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#BindEntityWithQuery)        |  Bind conentent(s) with a query|

### 数据库层面的操作
Below are low level data operations. Content manipulation normally is done via apis in core/handler since they includes validation, permission check, relation cache update, versioning, etc.

| Function        | Description       
|:-------------|:---------------------|
| [Insert](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Insert)        |  Insert a record |
| [Update](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Update)        |  Update a record |
| [Delete](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Delete)        |  Delete a record |




## 工具
package core/util

## 日志 & 调式
package core/log
