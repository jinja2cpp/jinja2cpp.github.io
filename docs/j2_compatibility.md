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

| Feature                                                  | Jinja2C++                            | Jinja2CppLight                       | pantor::inja                                       | Python Jinja2                        |
|----------------------------------------------------------|--------------------------------------|--------------------------------------|----------------------------------------------------|--------------------------------------|
| More information                                         |                                      | see [1]                              | see [2]                                            | see [3]                              |
| {% raw %}{{ / }}{% endraw %}                             | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| {% raw %}{% / %}{% endraw %}                             | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| {% raw %}{# / #}{% endraw %}                             | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| Single-line statements                                   | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| raw/endraw                                               | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| Whitespace control                                       | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| **Statements**                                           |                                      |                                      |                                                    |                                      |
| set                                                      | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| block set                                                | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| if / endif                                               | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| else                                                     | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| elif                                                     | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| for / endfor                                             | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| recursive for loop                                       | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| conditional for loop                                     | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| extends / block                                          | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| import                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| include                                                  | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| macro / endmacro                                         | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| call                                                     | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| filter                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| do (extension)                                           | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| with (extension)                                         | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| i18n (extension)                                         | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| continue/break (extension)                               | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| autoescape (extension)                                   | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| **Expressions**                                          |                                      |                                      |                                                    |                                      |
| String literals                                          | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| Integer numbers                                          | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| Floating numbers                                         | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| Lists (`[1, 3, 4]`)                                      | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| Tuples (`(1, "one", 3.14)`)                              | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| Dicts (`{'dict': 'of', 'key': 'and', 'value': 'pairs'}`) | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `True` / `False`                                         | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `+` operator                                             | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `-` operator                                             | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `/` operator                                             | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `//` operator                                            | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `%` operator                                             | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `*` operator                                             | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `**` operator                                            | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `==` operator                                            | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| `!=` operator                                            | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| `>` / `<` / `>=` / `<=` operators                        | <span style="color:green">yes</span> | <span style="color:green">yes</span> | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| `and` / `or` / `not` logical operators                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| `in` operator                                            | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| `is` operator                                            | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `|` (filter application operator)                        | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `~` (string concatenation operator)                      | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `()` (call operator)                                     | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| `.` (attribute access)                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span>               | <span style="color:green">yes</span> |
| `[]` (attribute access)                                  | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| `[]` (arrays slicing)                                    | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| **Filters**                                              |                                      |                                      |                                                    |                                      |
| abs                                                      | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| attr                                                     | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| batch                                                    | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| capitalize                                               | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| center                                                   | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| default                                                  | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| dictsort                                                 | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| escape                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| filesizeformat                                           | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| first                                                    | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| float                                                    | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| forceescape                                              | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| format                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| groupby                                                  | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| indent                                                   | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| int                                                      | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| join                                                     | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| last                                                     | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| length                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| list                                                     | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| lower                                                    | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| map                                                      | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| max                                                      | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| min                                                      | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| pprint                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| random                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| reject                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| rejectattr                                               | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| replace                                                  | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| reverse                                                  | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| round                                                    | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| safe                                                     | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| select                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| selectattr                                               | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| slice                                                    | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| sort                                                     | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| string                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| striptags                                                | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| sum                                                      | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| title                                                    | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| tojson                                                   | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| trim                                                     | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| truncate                                                 | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| unique                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| upper                                                    | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| urlencode                                                | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| urlize                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| wordcount                                                | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| wordwrap                                                 | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| **Testers**                                              |                                      |                                      |                                                    |                                      |
| callable                                                 | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| defined                                                  | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| devisibleby                                              | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| eq                                                       | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| escaped                                                  | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| even                                                     | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| ge                                                       | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| gt                                                       | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| in                                                       | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| iterable                                                 | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| le                                                       | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| lower                                                    | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| lt                                                       | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| mapping                                                  | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| ne                                                       | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| none                                                     | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| number                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| odd                                                      | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| sameas                                                   | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| sequence                                                 | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| string                                                   | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| undefined                                                | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| upper                                                    | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| **Global functions and classes**                         |                                      |                                      |                                                    |                                      |
| range                                                    | <span style="color:green">yes</span> | <span style="color:red">no</span>    | <span style="color:green">yes</span> (as function) | <span style="color:green">yes</span> |
| lipsum                                                   | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| dict                                                     | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| cycler                                                   | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| joiner                                                   | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |
| namespace                                                | <span style="color:red">no</span>    | <span style="color:red">no</span>    | <span style="color:red">no</span>                  | <span style="color:green">yes</span> |

### References

- [1] https://github.com/hughperkins/Jinja2CppLight
- [2] https://github.com/pantor/inja
- [3] https://jinja.palletsprojects.com/en/2.10.x/

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

