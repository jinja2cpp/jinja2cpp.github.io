---
layout: default
title: Changelog
nav_order: 5
---

# Changelog
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Version 1.2.1

### Changes and improvements
- bump deps versions
- support modern compilers(up to Clang 12) and standards(C++20)
- tiny code style cleanup

###Fixed bugs
- small fixes across code base

### Breaking changes
- internal deps point to make based boost build

## Version 1.1.0
### Changes and improvements
- `batch` filter added
- `slice` filter added
- `format` filter added
- `tojson` filter added
- `striptags` filter added
- `center` filter added
- `xmlattr` filter added
- `raw`/`endraw` tags added
- repeat string operator added (e. g. `'a' * 5` will produce `'aaaaa'`)
- support for templates metadata (`meta`/`endmeta` tags) added
- `-fPIC` flag added to Linux build configuration
- support both static and shared versions of library build

### Fixed bugs
- Fix behavior of lstripblock/trimblocks global settings. Now it fully corresponds to the origina jinja2
- Fix bug with rendering parent `block` content if child doesn't override this block
- Fix compilation issues with user-defined callables with number of arguments more than 2
- Fix access to global Jinja2 functions from included/extended templates
- Fix point of evaluation of macro params
- Fix looping over the strings
- Cleanup warnings

### Breaking changes
- From now with C++17 standard enabled Jinja2C++ uses standard versions of types `variant`, `string_view` and `optional`

## Version 1.0.0
### Changes and improvements
- `default` attribute added to the `map` filter
- escape sequences support added to the string literals
- arbitrary ranges, generated sequences, input iterators, etc. now can be used with `GenericList` type
- nonstd::string_view is now one of the possible types for the `Value`
- `filter` tag support added to the template parser
- `escape` filter support added to the template parser
- `capitalize` filter support added to the template parser
- the multiline version of `set` tag added to the parser
- added built-in reflection for nlohmann JSON and RapidJSON libraries
- `loop.depth` and `loop.depth0` variables support added
- {fmt} is now used as a formatting library instead of iostreams
- robin hood hash map is now used for internal value storage
- rendering performance improvements
- template cache implemented in `TemplateEnv`
- user-defined callables now can accept global context via `*context` special param
- MinGW, clang >= 7.0, XCode >= 9, gcc >= 7.0 are now officially supported as a target compilers

### Fixed bugs
- Fixed pipe (`|`) operator precedence
- Fixed bug in internal char <-> wchar_t converter on Windows
- Fixed crash in parsing `endblock` tag
- Fixed scope control for `include` and `for` tags
- Fixed bug with macros call within expression context

### Breaking changes
- MSVC runtime type is now defined by `JINJA2CPP_MSVC_RUNTIME_TYPE` CMake variable

## Version 0.9.2
### Major changes
- User-defined callables implemented. Now you can define your own callable objects, pass them as input parameters and use them inside templates as regular (global) functions, filters or testers. See details here: [https://jinja2cpp.dev/docs/usage/ud_callables.html](https://jinja2cpp.dev/docs/usage/ud_callables.html)
- Now you can define global (template environment-wide) parameters which are accessible for all templates bound to this environment.
- `include`, `import` and `from` statements implemented. Now it's possible to include other templates and use macros from other templates.
- `with` statement implemented
- `do` statement implemented
- Sample build projects for various Jinja2C++ usage variants created: [https://github.com/jinja2cpp/examples-build](https://github.com/jinja2cpp/examples-build)
- Documentation site created for Jinja2C++: [https://jinja2cpp.dev/](https://jinja2cpp.dev/)

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
* A lot of filters has been implemented. Full set of supported filters listed here: [https://github.com/flexferrum/Jinja2Cpp/issues/7](https://github.com/flexferrum/Jinja2Cpp/issues/7)
* A lot of testers has been implemented. Full set of supported testers listed here: [https://github.com/flexferrum/Jinja2Cpp/issues/8](https://github.com/flexferrum/Jinja2Cpp/issues/8)
* 'Contatenate as string' operator ('~') has been implemented
* For-loop with 'if' condition has been implemented
* Fixed some bugs in parser
