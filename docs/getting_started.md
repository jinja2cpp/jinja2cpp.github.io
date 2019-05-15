---
layout: default
title: Getting Started
nav_order: 2
description: "Quick start of Jinja2C++ usage"
---

# Getting started

## How to get Jinja2++

Get the latest Conan.io package: [
jinja2cpp/0.9.1@Manu343726/testing](https://bintray.com/manu343726/conan-packages/jinja2cpp%3AManu343726/0.9.1%3Atesting)

Or download the latest release: [Release 0.9.1](https://github.com/flexferrum/Jinja2Cpp/releases/latest)

Or:
- Clone the Jinja2C++ [repository](https://github.com/jinja2cpp/Jinja2Cpp)
- Build it according with the [instructions](build_and_install.html)
- Link to your project.

## The basic example

Usage of Jinja2C++ in the code is pretty simple:
1. Include Jinja2C++ template declaration:

```c++
#include <jinja2/template.h>
```

1. Declare the jinja2::Template object:

```c++
jinja2::Template tpl;
```

2. Populate it with template:

{% raw %}
```c++
tpl.Load("{{'Hello World' }}!!!");
```
{% endraw %}

3. Render the template:

```c++
std::cout << tpl.RenderAsString(jinja2::ValuesMap{}) << std::endl;
```

and get:

`
Hello World!!!
`

That's all!
