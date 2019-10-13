---
layout: default
title: Getting Started
nav_order: 2
description: "How to quickly start using Jinja2C++"
---

# Getting started

## How to get Jinja2++

Get the latest Conan.io package: [
jinja2cpp/0.9.1@Manu343726/testing](https://bintray.com/manu343726/conan-packages/jinja2cpp%3AManu343726/0.9.1%3Atesting)

Or download the latest release: [Release 0.9.2](https://github.com/jinja2cpp/Jinja2Cpp/releases/latest)

Or:
- Clone the Jinja2C++ [repository](https://github.com/jinja2cpp/Jinja2Cpp)
- Build it according to the [instructions](build_and_install.html)
- Link it with your project.

## A basic example

Using Jinja2C++ in your code is pretty simple:
1. Include Jinja2C++ template declaration:
```c++
#include <jinja2/template.h>
```
2. Declare the jinja2::Template object:
```c++
jinja2::Template tpl;
```
3. Populate it with template:{% raw %}
```c++
tpl.Load("{{'Hello World' }}!!!");
```{% endraw %}
4. Render the template:
```c++
std::cout << tpl.RenderAsString(jinja2::ValuesMap{}).value() << std::endl;
```

and you will get:

`
Hello World!!!
`

That's all!
