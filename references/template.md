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
    Template
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Template basis

We are using [Pongo2](https://github.com/flosch/pongo2) as template engine, which uses Python Django like style. Check their documentation to see examples:
 - Simple example: [https://github.com/flosch/pongo2#first-impression-of-a-template](https://github.com/flosch/pongo2#first-impression-of-a-template)
 - Examples as test cases: [https://github.com/flosch/pongo2/tree/master/template_tests](https://github.com/flosch/pongo2/tree/master/template_tests)

### Filters
Check here to see all their built in/add-on filters: [https://github.com/flosch/pongo2/blob/master/docs/filters.md](https://github.com/flosch/pongo2/blob/master/docs/filters.md)


## Functions in digimaker

### Contents

#### dm.fetch_byid
Parameter(int): id of the locaiton. 

Result(ContentTyper): content which has the location id
```
{% raw %}{% set content = dm.fetch_byid( 3 ) %}{% endraw %}
```


#### dm.parent
Parameter(ContentTyper)

Result(ContentTyper)

Description: return the parent of the content
```
{% raw %}{%set parent = dm.parent( content ) %}{% endraw %}
```

#### dm.children
Parameter: 

content ContentTyper

contentType string

sortBy string

***TBD***

Return: list of content or empty slice of ContentTyper if it has nothing


### MISC

#### dm.nice_url
Parameter: content ContentTyper

Return: string

Description: get nice url of a content, including site path/'prefix'

```
{% raw %}{{dm.nice_url( content ) }}{% endraw %}
```


#### dm.root
Parameter: string url

Return: string

Description: add site path as prefix to the url. If it's '/' the last / will be removed.

```
{% raw %}{{dm.root( 'mypage/profile' ) }}{% endraw %}
```


## Filters in digimaker


