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

| 函数        | 描述       
|:-------------|:---------------------|
| [FetchByID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#FetchByID)       |  通过id(location id)查询一个内容  |
| [FetchByCID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#FetchByCID)     |  通过内容id查询一个内容  |
| [Fetch](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#Fetch)           |   通过条件查询一个内容  |
| [FetchByUID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#FetchByUID)     |  通过location唯一标识符查询一个内容  |
| [FetchByCUID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#FetchByCUID)   |  通过内容唯一标识符查询一个内容  |


### 查询列表

| 函数        | 描述       
|:-------------|:---------------------|
| [SubList](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#SubList)       |  查询子内容列表, 考虑权限  |
| [ListWithUser](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#ListWithUser)  | 查询子内容列表, 考虑权限 |
| [Children](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#Children)      |  查询直接子内容列表(只有一层),考虑权限  |
| [List](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#List)     |  查询列表, 不考虑权限  |

### 查询子树

| 函数        | 描述       
|:-------------|:---------------------|
| [SubTree](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#SubTree)        |  查询子树  |

### 查询用户角色

| 函数        | 描述       
|:-------------|:---------------------|
| UserRole  |  查询用户角色 |

## 操作内容
包core/handler

**操作内容**

| 函数        | 描述       
|:-------------|:---------------------|
| [Create](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.Create)        |  创建内容 |
| [Update](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.Update)        |  更新内容 |
| [Move](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.Move)        |  移动内容 |
| [DeleteByID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.DeleteByID)        |  根据id删除内容 |
| [DeleteByCID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.DeleteByCID)        |  根据内容id删除内容 |
| [DeleteByContent](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.DeleteByContent)        | 删除一个已经给的内容 |


**用户**

| 函数        | 描述       
|:-------------|:---------------------|
| [CanLogin](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#CanLogin)        |  查看用户是否能登陆 |
| [Enable](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#Enable)        |  启用/禁用用户 |

## 权限
包 core/permission

| 函数        | 描述       
|:-------------|:---------------------|
| [HasAccessTo](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#HasAccessTo)        | 查看一个用户是否有某个操作的权限|
| [CanRead](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#CanRead)        |  查看一个用户可读取某个内容 |
| [CanUpdate](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#CanUpdate)        |  看一个用户可更新某个内容 |
| [CanDelete](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#CanDelete)        |  看一个用户可删除某个内容 |
| **Fetch policies and access**        |   |
| [GetUserAccess](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#GetUserAccess)        |  取得某个用户的限制(limit)列表|
| [GetUserPolicies](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#GetUserPolicies)        |  取得用户的策略|
| **Operations**| |
| [AssignToUser](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#AssignToUser)        |  把角色分配到用户上|
| [RemoveAssignment](https://pkg.go.dev/github.com/digimakergo/digimaker/core/permission#RemoveAssignment)        |  把角色从某个用户中移除|

## 数据库
包 core/db


### 条件

一个条件包含如下信息: 属性, 操作, 值(例如. "id > ", 10). 操作 '=', 'in'可忽略. 值可以是基本数据类型, 也可以是struct, 但需要实现[database.sql.driver.Valuer](https://golang.org/pkg/database/sql/driver/#Valuer)接口.


目前支持的操作: `">", ">=", "<", "==", "<=", "!=", "=", "in", "like"`. 

*注: "==" 用于连接查询.*

多个条件时使用面向方法的使用风格:

```go
//以下两个是一样的, 注: 当使用'in/like'时, 必须前面一个空格(如"a like")
db.Cond("id>", ids)
db.Cond("id >", ids)

//id等于3
db.Cond("id", 3)

//在1, 3中
db.Cond("id", []int{1, 3})

//id在1, 3中,而且author等于1
db.Cond("id", []int{1, 3}).Cond("author", 1)
```

[点击这里查看典型的条件例子](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#example-Cond)

| 函数        | 描述       
|:-------------|:---------------------|
| [Cond](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Cond)        |  创建条件 |
| [EmptyCond](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#EmptyCond)        |  创建空条件 |
| [TrueCond](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#TrueCond)        |  创建true条件 |
| [FalseCond](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#FalseCond)        |  创建false条件 |
| **Condition struct**| |
| [Cond](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Condition.Cond)     |  与And&Cond相同 |
| [And](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Condition.And)   |  相当于And, 把自己作为第一参数 |
| [Or](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Condition.Or)    | 相当于Or, 把自己作为第一参数 |
| [Sortby](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Condition.Sortby)        |  排序 |
| [Limit](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Condition.Limit)        |  用于分页 |
| [WithCount](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Condition.WithCount)   |  总包含计数信息, 不管有没有分页 |

### 数据库层面的查询

有两种实体(entity): 内容实体和一般实体. 一个内容实体可能来自于多个数据表, 但一个一般实体基本上来自一于一个表.

如果你查询一般表, 推荐使用`BindEntity`. 你可以把结果绑定到struct或者匿名结构(anonymous struct). 除此之外, 还可以用 `db.Datamap`/`DatamapList`, 它们可以直接返回一个表, 而不需要创建结构. 点击下面的 `BindEntity` 链接查看更多例子

| 函数        | 描述       
|:-------------|:---------------------|
| [BindContent](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#BindContent)        |  根据条件绑定到内容变量 |
| [CountContent](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#CountContent)        |  根据条件内容计数 |
| [BindEntity](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#BindEntity)        | 根据条件绑定到实体变量 |
| [Count](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Count)        |   根据条件实体计数 |
| [BindContentWithQuery](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#BindContentWithQuery)        | 根据查询(Query)绑定到内容变量|
| [BindEntityWithQuery](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#BindEntityWithQuery)        |  Bind conentent(s) with a query|

### 数据库层面的操作
以下是底层的数据操作. 内容操作建议通过内容的api进行(core/handler), 内容的api包含了验证, 权限, 关系, 缓存更新, 版本等.

| 函数        | 描述       
|:-------------|:---------------------|
| [Insert](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Insert)        |  插入记录 |
| [Update](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Update)        |  更新记录 |
| [Delete](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Delete)        |  删除记录 |




## 工具
包 core/util

## 日志 & 调式
包 core/log
