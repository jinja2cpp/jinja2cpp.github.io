---
layout: default
title: "Main statements"
parent: Jinja2C++ Usage
nav_order: 2
---

# Main Jinja2C++ statements

### 'set' statement
But what if enum `Animals` will be in the namespace?

```c++
namespace world
{
enum Animals
{
    Dog,
    Cat,
    Monkey,
    Elephant
};
}
```
In this case you need to prefix both enum name and it's items with namespace prefix in the generated code. Like this:
{% raw %}
```c++
std::string enum2StringConvertor = R"(
inline const char* {{enum.enumName}}ToString({{enum.nsScope}}::{{enum.enumName}} e)
{
    switch (e)
    {
{% for item in enum.items %}
    case {{enum.nsScope}}::{{item}}:
        return "{{item}}";
{% endfor %}
    }
    return "Unknown Item";
})";
```
{% endraw %}

This template will produce 'world::' prefix for our new scoped enum (and enum itmes). And '::' for the ones in global scope. But you may want to eliminate the unnecessary global scope prefix. And you can do it this way:
{% raw %}
```c++
{% set prefix = enum.nsScope + '::' if enum.nsScope else '' %}
std::string enum2StringConvertor = R"(inline const char* {{enum.enumName}}ToString({{prefix}}::{{enum.enumName}} e)
{
    switch (e)
    {
{% for item in enum.items %}
    case {{prefix}}::{{item}}:
        return "{{item}}";
{% endfor %}
    }
    return "Unknown Item";
})";
```
{% endraw %}

This template uses two significant jinja2 template features:
1. The 'set' statement. You can declare new variables in your template. And you can access them by the name.
2. if-expression. It works like a ternary '?:' operator in C/C++. In C++ the code from the sample could be written in this way:
```c++
std::string prefix = !descr.nsScope.empty() ? descr.nsScope + "::" : "";
```
I.e. left part of this expression (before 'if') is a true-branch of the statement. Right part (after 'else') - false-branch, which can be omitted. As a condition you can use any expression convertible to bool.

{% assign children_list = site.html_pages | sort:"nav_order" %}
{% for child in children_list %}
  {% unless forloop.first %}
    {% assign prev_page = current %}
  {% endunless %}
  {% unless cur_page == nil %}
    {% assign next_page = child %}
    {% break %}
  {% endunless %}
  {% assign current = cur_page %}
  {% if child.title == page.parent %}
    {% assign parent_page = child %}
    parent.nav_order (1) = {{ parent_page.nav_order }}<br/>
    parent.url (1) = {{ parent_page.url }}<br/>
    parent.title (1) = {{ parent_page.title }}<br/>
  {% endif %}
  {% if child.parent == page.parent and  child.title == page.title %}
    {% assign cur_page = child %}
    child.nav_order = {{ child.nav_order }}<br/>
    child.url = {{ child.url }}<br/>
    parent.nav_order = {{ parent_page_info.nav_order }}<br/>
    parent.url = {{ parent_page_info.url }}<br/>
    parent.title = {{ parent_page_info.title }}<br/>
    forloop.index = {{ forloop.index }}<br/>
    url[current] = {{ children_list[forloop.index0].url }}<br/>
    title[current] = {{ children_list[forloop.index0].title }}<br/>
    <a href="{{ child.url | absolute_url }}">{{ child.title }}</a>
  {% endif %}
{% endfor %}
parent.nav_order = {{ parent_page.nav_order }}<br/>
parent.url = {{ parent_page.url }}<br/>
parent.title = {{ parent_page.title }}<br/><br/>
prev.nav_order = {{ prev_page.nav_order }}<br/>
prev.url = {{ prev_page.url }}<br/>
prev.title = {{ prev_page.title }}<br/><br/>
cur.nav_order = {{ cur_page.nav_order }}<br/>
cur.url = {{ cur_page.url }}<br/>
cur.title = {{ cur_page.title }}<br/><br/>
next.nav_order = {{ next_page.nav_order }}<br/>
next.url = {{ next_page.url }}<br/>
next.title = {{ next_page.title }}<br/><br/>
<p><div align="center">&lt; Prev | <a href="{{ page.parent.url }}">Up</a> | <a href="main_statements.html">Next &gt;</a></div></p>

