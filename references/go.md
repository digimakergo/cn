---
layout: page
title: Go api
parent: 参考
permalink: /references/go
nav_order: 20
has_toc: true
---

Below is a overview Go APIs, see [auto generated go documentation](https://pkg.go.dev/github.com/digimakergo/digimaker#section-documentation)

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Fetch contents
package core/query

Note: in all queries, the condition syntax as below is used

```go
ids := []int{3, 4, 5, 7, 9, 10}
condition := db.Cond("id", ids).Cond("l.depth", 2).Cond("author", 1).Sortby("modified desc").Limit(0, 2)
```

### Fetch a content

| Function        | Description       
|:-------------|:---------------------|
| [FetchByID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#FetchByID)       |  Fetch a content by id  |
| [FetchByCID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#FetchByCID)     |  Fetch a content by content id  |
| [Fetch](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#Fetch)           |  Fetch a content by condition  |
| [FetchByUID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#FetchByUID)     |  Fetch a content by unique id  |
| [FetchByCUID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#FetchByCUID)   |  Fetch a content by content unique id  |


### Fetch List

| Function        | Description       
|:-------------|:---------------------|
| [SubList](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#SubList)       |  Fetch content list under a content, with permission considered  |
| [ListWithUser](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#ListWithUser)  |  Fetch content list with permission considered |
| [Children](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#Children)      |  Fetch children(direct children) with permission considered  |
| [List](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#List)     |  Fetch list by conditions(without permission considered)  |

### Fetch subtree

| Function        | Description       
|:-------------|:---------------------|
| [SubTree](https://pkg.go.dev/github.com/digimakergo/digimaker/core/query#SubTree)        |  Fetch sub tree of a content  |

### Fetch user/role

| Function        | Description       
|:-------------|:---------------------|
| UserRole  |  Fetch users, roles based on condition |

## Operate contents
package core/handler

**Manipulate content**

| Function        | Description       
|:-------------|:---------------------|
| [Create](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.Create)        |  Create content |
| [Update](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.Update)        |  Update a content |
| [Move](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.Move)        |  Move a content location |
| [DeleteByID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.DeleteByID)        |  Delete a content by location id |
| [DeleteByCID](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.DeleteByCID)        |  Delete a content by content id |
| [DeleteByContent](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#ContentHandler.DeleteByContent)        |  Delete a content |


**User**

| Function        | Description       
|:-------------|:---------------------|
| [CanLogin](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#CanLogin)        |  Check if a user can login or not |
| [Enable](https://pkg.go.dev/github.com/digimakergo/digimaker/core/handler#Enable)        |  Enable/Disable a user |

## Permission
package core/permission

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

## Database
package core/db


### Conditions

A condition includes information of field, operator and value(eg. "id > ", 10). Operator can be ignored if it's '=' or 'in'. Typical values are like 1(int), "hello"(string), or int/string slices(in will be used when querying), or datetime. So the value should be a baisc types or struct implementing  [database.sql.driver.Valuer](https://golang.org/pkg/database/sql/driver/#Valuer).

Supported operators: `">", ">=", "<", "==", "<=", "!=", "=", "in", "like"`. 

*Note: "==" is for join between 2 targets.*

It uses object-method style to build logical conditions.

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

### Queries
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

### Data operations
Below are low level data operations. Content manipulation normally is done via apis in core/handler since they includes validation, permission check, relation cache update, versioning, etc.

| Function        | Description       
|:-------------|:---------------------|
| [Insert](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Insert)        |  Insert a record |
| [Update](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Update)        |  Update a record |
| [Delete](https://pkg.go.dev/github.com/digimakergo/digimaker/core/db#Delete)        |  Delete a record |




## Utilities
package core/util

## Log & Debug
package core/log
