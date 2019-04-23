---
layout: default
title: Home
nav_order: 1
description: "Powerful text template engine for your C++ project!"
permalink: /
---

C++ implementation of big subset of Jinja2 template engine features. This library was inspired by [Jinja2CppLight](https://github.com/hughperkins/Jinja2CppLight) project and brings support of mostly all Jinja2 templates features into C++ world.

Main features of Jinja2Cpp:
- Easy-to-use public interface. Just load templates and render them.
- Conformance to [Jinja2 specification](http://jinja.pocoo.org/docs/2.10/)
- Partial support for both narrow- and wide-character strings both for templates and parameters.
- Built-in reflection for C++ types.
- Powerful full-featured Jinja2 expressions with filtering (via '\|' operator) and 'if'-expressions.
- Control statements (set, for, if).
- Templates extention.
- Macros
- Rich error reporting.

For instance, this simple code:

{% raw %}
```c++
std::string source = R"(
{{ ("Hello", 'world') | join }}!!!
{{ ("Hello", 'world') | join(', ') }}!!!
{{ ("Hello", 'world') | join(d = '; ') }}!!!
{{ ("Hello", 'world') | join(d = '; ') | lower }}!!!
)";

Template tpl;
tpl.Load(source);

std::string result = tpl.RenderAsString(ValuesMap());
```
{% endraw %}

produces the result string:

```
Helloworld!!!
Hello, world!!!
Hello; world!!!
hello; world!!!
```

# Acknowledgments
Thanks to @manu343726 for CMake scripts improvement, bugs hunting and fixing and conan.io packaging.

Thanks to @martinmoene for perfectly implemented xxx-lite libraries.
