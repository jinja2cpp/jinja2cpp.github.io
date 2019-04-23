---
layout: default
title: Macros
parent: Jinja2Cpp Usage
nav_order: 4
---

## Macros
Ths sample above violates 'DRY' rule. It contains the code which could be generalized. And Jinja2 supports features for such kind generalization. This feature called '**macro**'. The sample can be rewritten the following way:
{% raw %}
```c++
{% macro MethodsDecl(class, access) %}
{% for method in class.methods | rejectattr('isImplicit') | selectattr('accessType', 'in', access) %}
    {{ method.fullPrototype }};
{% endfor %}
{% endmacro %}

class {{ class.name }}
{
public:
    {{ MethodsDecl(class, ['Public']) }}
protected:
    {{ MethodsDecl(class, ['Protected']) }}
private:
    {{ MethodsDecl(class, ['Private', 'Undefined']) }}
};

{% endfor %}
```
{% endraw %}

`MethodsDecl` statement here is a **macro** which takes two arguments. First one is a class with method definitions. The second is a tuple of access specifiers. Macro takes non-implicit methods from the methods collection (`rejectattr('isImplicit')` filter) then select such methods which have right access specifier (`selectattr('accessType', 'in', access)`), then just prints the method full prototype. Finally, the macro is invoked as a regular function call: `MethodsDecl(class, ['Public'])` and replaced with rendered macro body.

There is another way to invoke macro: the **call** statement. Simply put, this is a way to call macro with *callback*. Let's take another sample:

{% raw %}
```c++
{% macro InlineMethod(resultType='void', methodName, methodParams=[]) %}
inline {{ resultType }} {{ methodName }}({{ methodParams | join(', ') }} )
{
    {{ caller() }}
}
{% endmacro %}

{% call InlineMethod('const char*', enum.enumName + 'ToString', [enum.nsScope ~ '::' ~ enum.enumName ~ ' e']) %}
    switch (e)
    {
{% for item in enum.items %}
    case {{enum.nsScope}}::{{item}}:
        return "{{item}}";
{% endfor %}
    }
    return "Unknown Item";
{% endcall %}
```
{% endraw %}

Here is an `InlineMacro` which just describe the inline method definition skeleton. This macro doesn't contain the actual method body. Instead of this it calls `caller` special function. This function invokes the special **callback** macro which is a body of `call` statement. And this macro can have parameters as well. More detailed this mechanics described in the [Jinja2 documentation](http://jinja.pocoo.org/docs/2.10/templates/#macros).

### 'applymacro' filter

With help of `applymacro` filter macro can be called in filtering context. `applymacro` works similar to `map` (or `test`) filter with one exception: instead of name of other filter it takes name of macro via `macro` param and pass the rest of arguments to it. The object which is been filtered is passed as the first positional argument. For example:

{% raw %}
```
{% macro toUpper(str) %}{{ str | upper }}{% endmacro %}
{{ 'Hello World!' | applymacro(macro='toUpper') }}
```
{% endraw %}

produces the result `HELLO WORLD`. `applymacro` can be applied to the sequences via `map` filter. Also, macro name can be `caller`. In this case outer `call` statement will be invoked during macro application.

