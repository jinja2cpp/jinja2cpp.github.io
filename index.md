---
layout: default
title: Home
nav_order: 1
description: "Powerful text template engine for your C++ project!"
permalink: /
---

# Bring powerful text template engine to your C++ project!
{: .no_toc }

Jinja2Cpp is a modern C++ implementation of the [Python Jinja2 template engine](http://jinja.pocoo.org/docs/2.10/). Originally inspired by [Jinja2CppLight](https://github.com/hughperkins/Jinja2CppLight) library now Jinja2Cpp brings support of mostly all Jinja2 templates engine features into C++ world.

## Main features of Jinja2Cpp:
{: .no_toc }

- Easy-to-use public interface. Just load templates and render them.
- Conformance to [Jinja2 specification](http://jinja.pocoo.org/docs/2.10/)
- Partial support for both narrow- and wide-character strings both for templates and parameters.
- Built-in reflection for C++ types.
- Powerful full-featured Jinja2 expressions with filtering (via '\|' operator) and 'if'-expressions.
- Control flow statements ('set', 'for', 'if').
- Templates extention ('extends', 'block').
- Macros ('macro', 'call').
- Rich error reporting.

## Basic example
{: .no_toc }

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

## Acknowledgments
{: .no_toc }

Thanks to authors of original Jinja2 specification for the exceptional work!

Thanks to @manu343726 for CMake scripts improvement, conan.io packaging and bugs hunting and fixing.

Thanks to @martinmoene for perfectly implemented xxx-lite libraries.
