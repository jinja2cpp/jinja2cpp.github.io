---
layout: prev_next_page
title: Basic Features
parent: Jinja2C++ Usage
nav_order: 1
---

# The simplest case

Let's say you have the following enum:

```c++
enum Animals
{
    Dog,
    Cat,
    Monkey,
    Elephant
};
```

And you want to automatically produce string-to-enum and enum-to-string convertor. Like this:

```c++
inline const char* AnimalsToString(Animals e)
{
    switch (e)
    {
    case Dog:
        return "Dog";
    case Cat:
        return "Cat";
    case Monkey:
        return "Monkey";
    case Elephant:
        return "Elephant";
    }
    return "Unknown Item";
}
```

Of course, you can write this producer in the way like [this](https://github.com/flexferrum/autoprogrammer/blob/87a9dc8ff61c7bdd30fede249757b71984e4b954/src/generators/enum2string_generator.cpp#L140). It's too complicated for writing 'from scratch'. Actually, there is a better and simpler way.

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

This template is quite basic. Actually, this is the regular text mixed with blocks, which have special meaning. Template parts wrapped with {% raw %}'{{' and '}}'{% endraw %} are expressions. During the template rendering this expression will be evaluated and the result will be inserted into final text. For instance, `{% raw %}{{ enumName }}{% endraw %}` should be replaced with the value of `enumName` param (if any) or should be substituted with an empty string. 

Template parts wrapped in {% raw %}'{%' and '%}'{% endraw %} are "statements" or control blocks. Each of such statement has special meaning and different processing inside Jinja2C++ engine. For instance, `{% raw %}{% for item in items %}...{% endfor %}{% endraw %}` is a loop statement. `items` variable should be a collection and loop body will be inserted into the final text as many times as many items in `items`. The current item can be accessed inside loop body via `item` variable. 

Template author can define new variables via `set` statement, test expressions via `if`, define macros via `macro`, include other templates via `include` and so on. There are many statements in the Jinja2 specification. But in order to be useful there should be a way to pass parameters to the template engine from the 'outside'. For instance, for the template above `items` should be somehow passed to the Jinja2C++ engine in order to be iterated. And there is a way to do it! Here it is!

```c++
jinja2::ValuesMap params {
    {"enumName", "Animals"},
    {"items", {"Dog", "Cat", "Monkey", "Elephant"}},
};
```
`jinja2::ValuesMap` is a data type which can hold associative collection of params. Each of this parameter can be accessed inside the template by it's name. The type of value can be not only string, but integer, float, boolean, array, another map or even reflected regular C++ type.

And now, the template can be rendered:

```c++
jinja2::Template tpl;
tpl.Load(enum2StringConvertor);
std::cout << tpl.RenderAsString(params);
```
And you will get on the console the conversion function mentioned above!

```c++
inline const char* AnimalsToString(Animals e)
{
    switch (e)
    {
    case Dog:
        return "Dog";
    case Cat:
        return "Cat";
    case Monkey:
        return "Monkey";
    case Elephant:
        return "Elephant";
    }
    return "Unknown Item";
}
```

You can call 'Render' method many times, with different parameters set, from different threads simultaniously. Everything will be fine: every time you call 'Render' you will get the result depended only on provided params (or global settings taken from the `TemplateEnv`).
