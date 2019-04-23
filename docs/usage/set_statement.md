---
layout: default
title: 'set' Statement
parent: Jinja2Cpp Usage
nav_order: 2
---

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
