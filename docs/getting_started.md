---
layout: default
title: Getting Started
nav_order: 2
description: "How to quickly start using Jinja2C++"
---

# Getting started

## How to get Jinja2++

Get the latest Conan.io package: [
jinja2cpp/1.1.0](https://bintray.com/conan/conan-center/jinja2cpp%3A_/1.1.0%3A_)

Or download the latest release: [Release 1.1.0](https://github.com/jinja2cpp/Jinja2Cpp/releases/latest)

Or:
- Clone the Jinja2C++ [repository](https://github.com/jinja2cpp/Jinja2Cpp)
- Build it according to the [instructions](build_and_install.html)
- Link it with your project.

## A basic example

Simple example project with Jinja2C++ usage can be found here: [https://github.com/jinja2cpp/examples-build/tree/master/conan/1.1.0](https://github.com/jinja2cpp/examples-build/tree/master/conan/1.1.0)

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

Full-featured trivial sample source:{% raw %}
```c++
#include <jinja2cpp/template.h>
#include <iostream>

int main()
{
    std::string source = R"(
{{ ("Hello", 'world') | join }}!!!
{{ ("Hello", 'world') | join(', ') }}!!!
{{ ("Hello", 'world') | join(d = '; ') }}!!!
{{ ("Hello", 'world') | join(d = '; ') | lower }}!!!)";

    jinja2::Template tpl;
    tpl.Load(source);

    std::string result = tpl.RenderAsString(jinja2::ValuesMap()).value();
    std::cout << result << "\n";
}
```{% endraw %}
