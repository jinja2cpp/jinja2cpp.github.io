---
layout: prev_next_page
title: User-defined Callables
parent: Jinja2C++ Usage
nav_order: 6
---

# User-defined callables

Not only C++ types can be reflected into Jinja2 template context, but the functions (and lambdas, and any other callable objects) as well. These refelected callable objects are called 'user-defined callables' and can be accessed from Jinja2 templates in the same manner as any other callables (like macros or global functions). In order to reflect callable object into Jinja2 context the `jinja2::MakeCallable` method should be used:

```c++
jinja2::ValuesMap params;
    params["concat"] = MakeCallable(
                [](const std::string& str1, const std::string& str2) {
                    return str1 + " " + str2;
                },
                ArgInfo{"str1"}, ArgInfo{"str2", false, "default"}
    );
```

As a first parameter this method takes the callable itself. It can be lambda, the std::function<> instance or pointer to function. The rest of params are callable arguments descriptors, which are provided via `ArgInfo` structure. In the sample above user-defined callable `concat` is introduced, which take two argument: `str1` and `str2`. This callable can be accessed from the template in the following ways:

{% raw %}
```
{{ concat('Hello', 'World!') }}
{{ concat(str2='World!', str1='Hello') }}
{{ concat(str2='World!') }}
{{ concat('Hello') }}
```
{% endraw %}
