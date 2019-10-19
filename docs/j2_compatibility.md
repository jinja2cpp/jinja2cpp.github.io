---
layout: default
title: Jinja2 Compatibility
nav_order: 7
---

# Jinja2C++ Compatibility
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Current Jinja2 support
Currently, Jinja2C++ supports the limited number of Jinja2 features. By the way, Jinja2C++ is planned to be full [jinja2 specification](http://jinja.pocoo.org/docs/2.10/templates/)-conformant. The current support is limited to:
- expressions. You can use every style of expressions: simple, filtered, conditional, and so on.
- amost all Jinja2 filters (except of `xmlattr` and `tojson`)
- big number of testers (**eq, defined, ge, gt, iterable, le, lt, mapping, ne, number, sequence, string, undefined, in, even, odd, lower, upper**)
- limited number of functions (**range**, **loop.cycle**)
- 'if' statement (with 'elif' and 'else' branches)
- 'for' statement (with 'else' branch and 'if' part support)
- 'set' statement (both single-line and block version)
- 'extends'/'block' statements
- 'include' statement
- 'import'/'from' statements
- 'macro'/'call' statements
- 'with' statement
- 'raw' statement
- 'do' extension statement
- 'filter' extension statement
- recursive loops
- space control

**Jinja2 specifiecation implementation notes**:

## Comparison with other implementations

| Feature                                                  | Jinja2C++                            | Jinja2CppLight                       | pantor::inja                         | Python Jinja2                        |
|----------------------------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|
| More information                                         |                                      | see [1]                              | see [2]                              | see [3]                              |
| {% raw %}{{ / }}{% endraw %}                             | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span> |
| {% raw %}{% / %}{% endraw %}                             | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span> |
| {% raw %}{# / #}{% endraw %}                             | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span> |
| Single-line statements                                   | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:green">yes</span> | <span style="color:green">yes</span> |
| raw/endraw                                               | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:green">yes</span> |
| Whitespace control                                       | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> | <span style="color:green">yes</span> |
| **Statements**                                           |                                      |                                      |                                      |                                      |
| set                                                      |                                      |                                      |                                      |                                      |
| block set                                                |                                      |                                      |                                      |                                      |
| if / endif                                               |                                      |                                      |                                      |                                      |
| else                                                     |                                      |                                      |                                      |                                      |
| elif                                                     |                                      |                                      |                                      |                                      |
| for / endfor                                             |                                      |                                      |                                      |                                      |
| recursive for loop                                       |                                      |                                      |                                      |                                      |
| conditional for loop                                     |                                      |                                      |                                      |                                      |
| extends / block                                          |                                      |                                      |                                      |                                      |
| import                                                   |                                      |                                      |                                      |                                      |
| include                                                  |                                      |                                      |                                      |                                      |
| macro / endmacro                                         |                                      |                                      |                                      |                                      |
| call                                                     |                                      |                                      |                                      |                                      |
| filter                                                   |                                      |                                      |                                      |                                      |
| do                                                       |                                      |                                      |                                      |                                      |
| **Expressions**                                          |                                      |                                      |                                      |                                      |
| String literals                                          |                                      |                                      |                                      |                                      |
| Integer numbers                                          |                                      |                                      |                                      |                                      |
| Floating numbers                                         |                                      |                                      |                                      |                                      |
| Lists (`[1, 3, 4]`)                                      |                                      |                                      |                                      |                                      |
| Tuples (`(1, "one", 3.14)`)                              |                                      |                                      |                                      |                                      |
| Dicts (`{'dict': 'of', 'key': 'and', 'value': 'pairs'}`) |                                      |                                      |                                      |                                      |
| `True` / `False`                                         |                                      |                                      |                                      |                                      |
| `+` operator                                             |                                      |                                      |                                      |                                      |
| `-` operator                                             |                                      |                                      |                                      |                                      |
| `/` operator                                             |                                      |                                      |                                      |                                      |
| `//` operator                                            |                                      |                                      |                                      |                                      |
| `%` operator                                             |                                      |                                      |                                      |                                      |
| `*` operator                                             |                                      |                                      |                                      |                                      |
| `**` operator                                            |                                      |                                      |                                      |                                      |
| `==` operator                                            |                                      |                                      |                                      |                                      |
| `!=` operator                                            |                                      |                                      |                                      |                                      |
| `>` / `<` / `>=` / `<=` operators                        |                                      |                                      |                                      |                                      |
| `and` / `or` / `not` logical operators                   |                                      |                                      |                                      |                                      |
| `in` operator                                            |                                      |                                      |                                      |                                      |
| `is` operator                                            |                                      |                                      |                                      |                                      |
| `|` (filter application operator)                        |                                      |                                      |                                      |                                      |
| `~` (string concatenation operator)                      |                                      |                                      |                                      |                                      |
| `()` (call operator)                                     |                                      |                                      |                                      |                                      |
| `.`/`[]` (attribute access)                              |                                      |                                      |                                      |                                      |
| **Filters**                                              |                                      |                                      |                                      |                                      |
| abs                                                      |                                      |                                      |                                      |                                      |
| attr                                                     |                                      |                                      |                                      |                                      |
| batch                                                    |                                      |                                      |                                      |                                      |
| capitalize                                               |                                      |                                      |                                      |                                      |
| center                                                   |                                      |                                      |                                      |                                      |
| default                                                  |                                      |                                      |                                      |                                      |
| dictsort                                                 |                                      |                                      |                                      |                                      |
| escape                                                   |                                      |                                      |                                      |                                      |
| filesizeformat                                           |                                      |                                      |                                      |                                      |
| first                                                    |                                      |                                      |                                      |                                      |
| float                                                    |                                      |                                      |                                      |                                      |
| forceescape                                              |                                      |                                      |                                      |                                      |
| format                                                   |                                      |                                      |                                      |                                      |
| groupby                                                  |                                      |                                      |                                      |                                      |
| indent                                                   |                                      |                                      |                                      |                                      |
| int                                                      |                                      |                                      |                                      |                                      |
| join                                                     |                                      |                                      |                                      |                                      |
| last                                                     |                                      |                                      |                                      |                                      |
| length                                                   |                                      |                                      |                                      |                                      |
| list                                                     |                                      |                                      |                                      |                                      |
| lower                                                    |                                      |                                      |                                      |                                      |
| map                                                      |                                      |                                      |                                      |                                      |
| max                                                      |                                      |                                      |                                      |                                      |
| min                                                      |                                      |                                      |                                      |                                      |
| pprint                                                   |                                      |                                      |                                      |                                      |
| random                                                   |                                      |                                      |                                      |                                      |
| reject                                                   |                                      |                                      |                                      |                                      |
| rejectattr                                               |                                      |                                      |                                      |                                      |
| replace                                                  |                                      |                                      |                                      |                                      |
| reverse                                                  |                                      |                                      |                                      |                                      |
| round                                                    |                                      |                                      |                                      |                                      |
| safe                                                     |                                      |                                      |                                      |                                      |
| select                                                   |                                      |                                      |                                      |                                      |
| selectattr                                               |                                      |                                      |                                      |                                      |
| slice                                                    |                                      |                                      |                                      |                                      |
| sort                                                     |                                      |                                      |                                      |                                      |
| string                                                   |                                      |                                      |                                      |                                      |
| striptags                                                |                                      |                                      |                                      |                                      |
| sum                                                      |                                      |                                      |                                      |                                      |
| title                                                    |                                      |                                      |                                      |                                      |
| tojson                                                   |                                      |                                      |                                      |                                      |
| trim                                                     |                                      |                                      |                                      |                                      |
| truncate                                                 |                                      |                                      |                                      |                                      |
| unique                                                   |                                      |                                      |                                      |                                      |
| upper                                                    |                                      |                                      |                                      |                                      |
| urlencode                                                |                                      |                                      |                                      |                                      |
| urlize                                                   |                                      |                                      |                                      |                                      |
| wordcount                                                |                                      |                                      |                                      |                                      |
| wordwrap                                                 |                                      |                                      |                                      |                                      |
| **Testers**                                              |                                      |                                      |                                      |                                      |
| callable                                                 |                                      |                                      |                                      |                                      |
| defined                                                  |                                      |                                      |                                      |                                      |
| devisibleby                                              |                                      |                                      |                                      |                                      |
| eq                                                       |                                      |                                      |                                      |                                      |
| escaped                                                  |                                      |                                      |                                      |                                      |
| even                                                     |                                      |                                      |                                      |                                      |
| ge                                                       |                                      |                                      |                                      |                                      |
| gt                                                       |                                      |                                      |                                      |                                      |
| in                                                       |                                      |                                      |                                      |                                      |
| iterable                                                 |                                      |                                      |                                      |                                      |
| le                                                       |                                      |                                      |                                      |                                      |
| lower                                                    |                                      |                                      |                                      |                                      |
| lt                                                       |                                      |                                      |                                      |                                      |
| mapping                                                  |                                      |                                      |                                      |                                      |
| ne                                                       |                                      |                                      |                                      |                                      |
| none                                                     |                                      |                                      |                                      |                                      |
| number                                                   |                                      |                                      |                                      |                                      |
| odd                                                      |                                      |                                      |                                      |                                      |
| sameas                                                   |                                      |                                      |                                      |                                      |
| sequence                                                 |                                      |                                      |                                      |                                      |
| string                                                   |                                      |                                      |                                      |                                      |
| undefined                                                |                                      |                                      |                                      |                                      |
| upper                                                    |                                      |                                      |                                      |                                      |
| **Testers**                                              |                                      |                                      |                                      |                                      |
| range                                                    |                                      |                                      |                                      |                                      |
| lipsum                                                   |                                      |                                      |                                      |                                      |
| dict                                                     |                                      |                                      |                                      |                                      |
| cycler                                                   |                                      |                                      |                                      |                                      |
| joiner                                                   |                                      |                                      |                                      |                                      |
| namespace                                                |                                      |                                      |                                      |                                      |

### References

- [1]
- [2]
- [3]

## Jinja2C++ performance

 Template                                                                                           | Python    | Jinja2C++ (MSVC build) | Jinja2C++ (MinGW Build) 
----------------------------------------------------------------------------------------------------|-----------|------------------------|-------------------------
 `Hello World from Parser!` (1 mln. iterations)                                                     | 4.333 sec | 1.883 sec              | 0.831 sec               
 `{% raw %}{{ message }} from Parser!{% endraw %}` message='Hello World!' (1 mln. iterations)                            | 5.083     | 2.188                  | 1.082                   
 `{% raw %}{{ message }} from Parser!{% endraw %}` message=100500 (1 mln. iterations)                                    | 5.126     | 2.211                  | 1.087                   
 `{% raw %}{{ message | upper }} from Parser!{% endraw %}`  message='Hello World!' (1 mln. iterations)                   | 5.583     | 3.559                  | 1.850                   
 `{% raw %}{{ message }} from Parser! - {{number}}{% endraw %}` message='Hello World!', number=100500 (1 mln. iterations)| 5.800     | 2.594                  | 1.504                   
 `{% raw %}{% for i in range(20)%} {{i}} {%endfor%}{% endraw %}` (20 thsd. iterations)                                   | 2.485     | 2.917                  | 1.966                   
 `{% raw %}{% for i in range(num)%} {{i}} {%endfor%}{% endraw %}` num=20 (20 thsd. iterations)                           | 2.575     | 2.768                  | 2.040                   
 `{% raw %}{% for i in range(20)%} {{i ~ "-" ~ loop.index}} {%endfor%}{% endraw %}` (20 thsd. iterations)                | 11.720    | 6.334                  | 4.340                   
 `{% raw %}{% for i in range(20) if i is odd %} {{i}} {%endfor%}{% endraw %}` (20 thsd. iterations)                      | 2.620     | 3.710                  | 2.733                   

