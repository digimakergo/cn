---
layout: page
title: 模板
parent: 参考
permalink: /references/template
nav_order: 9
has_toc: true
---

<details open markdown="block">
  <summary>
    模板
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## 模板初步

我们使用 [Pongo2](https://github.com/flosch/pongo2) 作为模板引擎, 有些类似于Python Django的语法风格. 请查看Pongo2的文档得到基本用法:
 - 基本例子: [https://github.com/flosch/pongo2#first-impression-of-a-template](https://github.com/flosch/pongo2#first-impression-of-a-template)
 - 更多例子(以测试用例的方式): [https://github.com/flosch/pongo2/tree/master/template_tests](https://github.com/flosch/pongo2/tree/master/template_tests)

### Filters
这里有Pongo2的默认和和扩展的filter: [https://github.com/flosch/pongo2/blob/master/docs/filters.md](https://github.com/flosch/pongo2/blob/master/docs/filters.md)


## Digimaker的模板函数

### 内容相关

#### dm.fetch_byid
参数(int): location id. 
返回(ContentTyper): 指定id的内容
```
{% raw %}{% set content = dm.fetch_byid( 3 ) %}{% endraw %}
```


#### dm.parent
参数(ContentTyper)

返回(ContentTyper)

说明: 返回内容的父节点
```
{% raw %}{%set parent = dm.parent( content ) %}{% endraw %}
```

#### dm.children


***TBD***

Return: list of content or empty slice of ContentTyper if it has nothing


### 其它

#### dm.nice_url
参数: ContentTyper

返回: string

描述: 得到内容的nice url

```
{% raw %}{{dm.nice_url( content ) }}{% endraw %}
```


#### dm.root
参数: string url

返回: string

描述: 添加前缀, 如果是 '/', 最后的/将被忽略.

```
{% raw %}{{dm.root( 'mypage/profile' ) }}{% endraw %}
```


## Digimaker的filter


