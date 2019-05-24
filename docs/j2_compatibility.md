---
layout: default
title: Jinja2 Compatibility
nav_order: 7
---

# Current Jinja2 support
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
- 'import'/'from' statement
- 'macro'/'call' statements
- recursive loops
- space control
