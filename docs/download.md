---
layout: default
title: Download and Releases
nav_order: 5
---

# Changelog
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## Version 0.9.2
### Major changes
- User-defined callables implemented. Now you can define your own callable objects, pass them as input parameters and use them inside templates as regular (global) functions, filters or testers. See details here: https://jinja2cpp.dev/docs/usage/ud_callables.html
- Now you can define global (template environment-wide) parameters which are accessible for all templates bound to this environment.
- `include`, `import` and `from` statements implemented. Now it's possible to include other templates and use macros from other templates.
- `with` statement implemented
- `do` statement implemented
- Sample build projects for various Jinja2C++ usage variants created: https://github.com/jinja2cpp/examples-build
- Documentation site created for Jinja2C++: https://jinja2cpp.dev/

### Minor changes
- Render-time error handling added
- Dependency management mode added to the build script
- Fix bugs with error reporting during the parse time
- Upgraded versions of external dependencies

### Breaking changes
- `RenderAsString` method now returns `nonstd::expected` instead of regular `std::string`
- Templates with `import`, `extends` and `include` generate errors if parsed without `TemplateEnv` set
- Release bundles (archives) are configured with `external` dependency management mode by default

## Version 0.9.1
* `applymacro` filter added which allows to apply arbitrary macro as a filter
* dependencies to boost removed from the public interface
* CMake scripts improved
* Various bugs fixed
* Improve reflection
* Warnings cleanup

## Version 0.9
* Support of 'extents'/'block' statements
* Support of 'macro'/'call' statements
* Rich error reporting
* Support for recursive loops
* Support for space control before and after control blocks
* Improve reflection

## Version 0.6
* A lot of filters has been implemented. Full set of supported filters listed here: https://github.com/flexferrum/Jinja2Cpp/issues/7
* A lot of testers has been implemented. Full set of supported testers listed here: https://github.com/flexferrum/Jinja2Cpp/issues/8
* 'Contatenate as string' operator ('~') has been implemented
* For-loop with 'if' condition has been implemented
* Fixed some bugs in parser
