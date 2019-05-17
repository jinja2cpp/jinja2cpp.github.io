---
layout: prev_next_page
title: Reflection
parent: JinjaC++ Usage
nav_order: 5
---

# Reflection
Let's imagine you don't want to fill the enum descriptor by hand, but want to fill it with help of some code parsing tool ([autoprogrammer](https://github.com/flexferrum/autoprogrammer) or [cppast](https://github.com/foonathan/cppast)). In this case you can define structure like this:

```c++
// Enum declaration description
struct EnumDescriptor
{
// Enumeration name
std::string enumName;
// Namespace scope prefix
std::string nsScope;
// Collection of enum items
std::vector<std::string> enumItems;
};
```
This structure holds the enum name, enum namespace scope prefix, and list of enum items (we need just names). Then, you can populate instances of this descriptor automatically using chosen tool (ex. here: [clang-based enum2string converter generator](https://github.com/flexferrum/flex_lib/blob/accu2017/tools/codegen/src/main.cpp) ). For our sample we can create the instance manually:
```c++
EnumDescriptor descr;
descr.enumName = "Animals";
descr.nsScope = "";
descr.enumItems = {"Dog", "Cat", "Monkey", "Elephant"};
```

And now you need to transfer data from this internal enum descriptor to Jinja2 value params map. Of course it's possible to do it by hands:
```c++
jinja2::ValuesMap params {
    {"enumName", descr.enumName},
    {"nsScope", descr.nsScope},
    {"items", {descr.enumItems[0], descr.enumItems[1], descr.enumItems[2], descr.enumItems[3]}},
};
```

But actually, with Jinja2Cpp you don't have to do it manually. Library can do it for you. You just need to define reflection rules. Something like this:

```c++
namespace jinja2
{
template<>
struct TypeReflection<EnumDescriptor> : TypeReflected<EnumDescriptor>
{
    static auto& GetAccessors()
    {
        static std::unordered_map<std::string, FieldAccessor> accessors = {
            {"name", [](const EnumDescriptor& obj) {return obj.name;}},
            {"nsScope", [](const EnumDescriptor& obj) { return obj.nsScope;}},
            {"items", [](const EnumDescriptor& obj) {return Reflect(obj.items);}},
        };

        return accessors;
    }
};
```
And in this case you need to correspondingly change the template itself and it's invocation:
{% raw %}
```c++
std::string enum2StringConvertor = R"(
inline const char* {{enum.enumName}}ToString({{enum.enumName}} e)
{
    switch (e)
    {
{% for item in enum.items %}
    case {{item}}:
        return "{{item}}";
{% endfor %}
    }
    return "Unknown Item";
})";

// ...
    jinja2::ValuesMap params = {
        {"enum", jinja2::Reflect(descr)},
    };
// ...
```
{% endraw %}

Every specified field will be reflected into Jinja2Cpp internal data structures and can be accessed from the template without additional efforts. Quite simply! As you can see, you can use 'dot' notation to access named members of some parameter as well, as index notation like this: `enum['enumName']`. With index notation you can access to the particular item of a list: `enum.items[3]` or `enum.items[itemIndex]` or `enum['items'][itemIndex]`.

The render procedure is stateless, so you can perform several renderings simultaneously in different threads. Even if you pass parameters:

```c++
    ValuesMap params = {
        {"intValue", 3},
        {"doubleValue", 12.123f},
        {"stringValue", "rain"},
        {"boolFalseValue", false},
        {"boolTrueValue", true},
    };

    std::string result = tpl.RenderAsString(params);
    std::cout << result << std::endl;
```

Parameters could have the following types:
- std::string/std::wstring
- integer (int64_t)
- double
- boolean (bool)
- Tuples (also known as arrays)
- Dictionaries (also known as maps)

Tuples and dictionaries can be mapped to the C++ types. So you can smoothly reflect your structures and collections into the template engine:

```c++
namespace jinja2
{
template<>
struct TypeReflection<reflection::EnumInfo> : TypeReflected<reflection::EnumInfo>
{
    static auto& GetAccessors()
    {
        static std::unordered_map<std::string, FieldAccessor> accessors = {
            {"name", [](const reflection::EnumInfo& obj) {return Reflect(obj.name);}},
            {"scopeSpecifier", [](const reflection::EnumInfo& obj) {return Reflect(obj.scopeSpecifier);}},
            {"namespaceQualifier", [](const reflection::EnumInfo& obj) { return obj.namespaceQualifier;}},
            {"isScoped", [](const reflection::EnumInfo& obj) {return obj.isScoped;}},
            {"items", [](const reflection::EnumInfo& obj) {return Reflect(obj.items);}},
        };

        return accessors;
    }
};

// ...
    jinja2::ValuesMap params = {
        {"enum", jinja2::Reflect(enumInfo)},
    };
```
