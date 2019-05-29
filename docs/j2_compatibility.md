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
- big number of filters (**sort, default, first, last, length, max, min, reverse, unique, sum, attr, map, reject, rejectattr, select, selectattr, pprint, dictsort, abs, float, int, list, round, random, trim, title, upper, wordcount, replace, truncate, groupby, urlencode**)
- big number of testers (**eq, defined, ge, gt, iterable, le, lt, mapping, ne, number, sequence, string, undefined, in, even, odd, lower, upper**)
- limited number of functions (**range**, **loop.cycle**)
- 'if' statement (with 'elif' and 'else' branches)
- 'for' statement (with 'else' branch and 'if' part support)
- 'set' statement
- 'extends'/'block' statements
- 'include' statement
- 'import'/'from' statements
- 'macro'/'call' statements
- 'with' statement
- 'do' extension statement
- recursive loops
- space control

**Jinja2 specifiecation implementation notes**:
- Wrong precedence of '\|' (pipe) operator (see (#47)[https://github.com/jinja2cpp/Jinja2Cpp/issues/47]
- Block 'set' statement version doesn't implemented

## Comparison with like types
|Feature                     |Jinja2CppLight|pantor::inja   |Python Jinja2  |
|----------------------------|--------------|---------------|---------------|
|More information            | see [1]      | see [2]       | see [3]       |
|                            |              |               |               |
| {% raw %}{{/}}{% endraw %} | yes          | yes           | yes           |

### References

[1]
[2]
[3]
