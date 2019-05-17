---
layout: prev_next_page
title: Error Reporting
parent: Jinja2C++ Usage
nav_order: 7
---

# Error reporting
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Common concepts

TODO:

## Parse-time errors
It's difficult to write complex template completely without errors. Missed braces, wrong characters, incorrect names... Everything is possible. So, it's crucial to be able to get informative error report from the template engine. Jinja2Cpp provides such kind of report. ```Template::Load``` method (and TemplateEnv::LoadTemplate respectively) return instance of ```ErrorInfo``` class which contains details about the error. These details include:
- Error code
- Error description
- File name and position (1-based line, col) of the error
- Location description

For example, this template:
{% raw %}
```
{{ {'key'=,} }}
```
{% endraw %}

produces the following error message:
{% raw %}
```
noname.j2tpl:1:11: error: Expected expression, got: ','
{{ {'key'=,} }}
       ---^-------
```
{% endraw %}

## Runtime errors

TODO:
