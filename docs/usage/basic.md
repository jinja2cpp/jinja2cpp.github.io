---
layout: default
title: Basic Features
parent: Jinja2Cpp Usage
nav_order: 1
---

### The simplest case

Firstly, you should define the simple jinja2 template (in the C++ manner):
{% raw %}
```c++
std::string enum2StringConvertor = R"(
inline const char* {{enumName}}ToString({{enumName}} e)
{
    switch (e)
    {
{% for item in items %}
    case {{item}}:
        return "{{item}}";
{% endfor %}
    }
    return "Unknown Item";
})";
```
{% endraw %}

As you can see, this template is similar to the C++ sample code above, but some parts replaced by placeholders ("parameters"). These placeholders will be replaced with the actual text during template rendering process. In order to this happen, you should fill up the rendering parameters. This is a simple dictionary which maps the parameter name to the corresponding value:

```c++
jinja2::ValuesMap params {
    {"enumName", "Animals"},
    {"items", {"Dog", "Cat", "Monkey", "Elephant"}},
};
```
An finally, you can render this template with Jinja2Cpp library:

```c++
jinja2::Template tpl;
tpl.Load(enum2StringConvertor);
std::cout << tpl.RenderAsString(params);
```
And you will get on the console the conversion function mentioned above!

You can call 'Render' method many times, with different parameters set, from several threads. Everything will be fine: every time you call 'Render' you will get the result depended only on provided params. Also you can render some part of template many times (for different parameters) with help of 'for' loop and 'extend' statement (described below). It allows you to iterate through the list of items from the first to the last one and render the loop body for each item respectively. In this particular sample it allows to put as many 'case' blocks in conversion function as many items in the 'reflected' enum.
