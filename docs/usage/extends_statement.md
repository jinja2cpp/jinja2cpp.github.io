---
layout: prev_next_page
title: "'extends' Statement"
parent: Jinja2C++ Usage
nav_order: 3
---

# 'extends' statement
In general, C++ header files look similar to each other. Almost every header file has got header guard, block of 'include' directives and then block of declarations wrapped into namespaces. So, if you have several different Jinja2 templates for header files production it can be a good idea to extract the common header structure into separate template. Like this:
{% raw %}
```c++
{% if headerGuard is defined %}
 #ifndef {{headerGuard}}
 #define {{headerGuard}}
{% else %}
 #pragma once
{% endif %}

{% for fileName in inputFiles | sort %}
 #include "{{fileName}}"
{% endfor %}

{% for fileName in extraHeaders | sort %}
{% if fileName is startsWith('<') %}
 #include {{fileName}}
{% else %}
 #include "{{fileName}}"
{% endif %}
{% endfor %}

{% block generator_headers %}{% endblock %}

{% block namespaced_decls %}
{% set ns = rootNamespace %}
{#ns | pprint}
{{rootNamespace | pprint} #}
{% block namespace_content scoped %}{%endblock%}
{% for ns in rootNamespace.innerNamespaces recursive %}namespace {{ns.name}}
{
{{self.namespace_content()}}
{{ loop(ns.innerNamespaces) }}
}
{% endfor %}
{% endblock %}

{% block global_decls %}{% endblock %}

{% if headerGuard is defined %}
 #endif // {{headerGuard}}
{% endif %}
```
{% endraw %}

In this sample you can see the '**block**' statements. They are placeholders. Each block is a part of generic template which can be replaced by more specific template which 'extends' generic:
{% raw %}
```c++
{% extends "header_skeleton.j2tpl" %}

{% block namespaced_decls %}{{super()}}{% endblock %}

{% block namespace_content %}
{% for class in ns.classes | sort(attribute="name") %}

class {{ class.name }}
{
public:
    {% for method in class.methods | rejectattr('isImplicit') | selectattr('accessType', 'equalto', 'Public') %}
    {{ method.fullPrototype }};
    {% endfor %}
protected:
    {% for method in class.methods | rejectattr('isImplicit') | selectattr('accessType', 'equalto', 'Protected') %}
    {{ method.fullPrototype }};
    {% endfor %}
private:
    {% for method in class.methods | rejectattr('isImplicit') | selectattr('accessType', 'in', ['Private', 'Undefined']) %}
    {{ method.fullPrototype }};
    {% endfor %}
};

{% endfor %}
{% endblock %}
```
{% endraw %}

'**extends**' statement here defines the template to extend. Set of '**block**' statements after defines actual filling of the corresponding blocks from the extended template. If block from the extended template contains something (like ```namespaced_decls``` from the example above), this content can be rendered with help of '**super()**' function. In other case the whole content of the block will be replaced. More detailed description of template inheritance feature can be found in [Jinja2 documentation](http://jinja.pocoo.org/docs/2.10/templates/#template-inheritance).

