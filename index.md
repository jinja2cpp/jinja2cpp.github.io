---
layout: default
title: Home
nav_order: 1
description: "Powerful text template engine for your C++ project!"
permalink: /
---

# Bring powerful text template engine to your C++ project!
{: .no_toc }

{: .fs-9 }
Jinja2Cpp is a modern C++ implementation of the [Python Jinja2 template engine](http://jinja.pocoo.org/docs/2.10/). Originally inspired by [Jinja2CppLight](https://github.com/hughperkins/Jinja2CppLight) library now Jinja2Cpp brings support of mostly all Jinja2 templates engine features into C++ world.
{: .fs-6 .fw-300 }

## Main features of Jinja2Cpp:
{: .no_toc }

- C++14/17 library
- Supports mainstream compilers (Visual C++, gcc, clang)
- Easy-to-use interface.
- Conformance to [Jinja2 specification](http://jinja.pocoo.org/docs/2.10/)
- Partial support for both narrow- and wide-character strings both for templates and parameters.
- Built-in reflection for C++ types.
- Powerful full-featured Jinja2 expressions with filtering (via '\|' operator) and 'if'-expressions.
- Control flow statements ('set', 'for', 'if').
- Templates extention ('extends', 'block').
- Macros ('macro', 'call').
- Rich error reporting.

[View it on GitHub](https://github.com/jinja2cpp/Jinja2Cpp){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View it on Conan](https://bintray.com/manu343726/conan-packages/jinja2cpp%3AManu343726){: .btn .fs-5 .mb-4 .mb-md-0 }

## How to get Jinja2Cpp
{: .no_toc }

The simpliest way: to get the latest conan.io package: [
jinja2cpp/0.9.1@Manu343726/testing](https://bintray.com/manu343726/conan-packages/jinja2cpp%3AManu343726/0.9.1%3Atesting)

Or follow the [build and install instructions](/docs/build_and_install.html)

## About the project
{: .no_toc }

Jinja2Cpp is &copy; 2018-2019 by [Flex Ferrum](https://github.com/flexferrum). 

### License
{: .no_toc }

Jinja2Cpp is distributed by an [Mozilla Public License 2.0](https://github.com/jinja2cpp/Jinja2Cpp/blob/master/LICENSE).

### Contributing
{: .no_toc }

When contributing to this repository, please first discuss the change you wish to make via issue,
email, or any other method with the owners of this repository before making a change.

### Acknowledgments
{: .no_toc }

Thanks to authors of original Jinja2 specification for the exceptional work!

Thanks to [**manu343726**](https://github.com/Manu343726) for CMake scripts improvement, conan.io packaging and bugs hunting and fixing.

Thanks to [**martinmoene**](https://github.com/martinmoene) for perfectly implemented xxx-lite libraries.
