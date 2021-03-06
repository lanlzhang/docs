---
title: 'resetStyleInheritance'
notes:
  - 'Needs spec reference, example'
readiness: 'In Progress'
relationships:
  applies_to:
    predicate: 'Property of '
    value: dom/shadowdom/ShadowRoot
    href: /dom/shadowdom/ShadowRoot
  return:
    predicate: 'Returns an object of type '
    value: Boolean
    href: /dom/shadowdom/ShadowRoot
standardization_status: 'W3C Editor''s Draft'
summary: 'Indicates whether or not the inheritable CSS properties are set to the initial value at the shadow boundary. If false (default value), the properties continue to inherit. If true, the properties are set to initial value.'
tags:
  - API_Object_Properties
  - API
  - DOM
  - Shadow_DOM
  - Needs_Examples
uri: dom/shadowdom/ShadowRoot/resetStyleInheritance

---
## Summary

Indicates whether or not the inheritable CSS properties are set to the initial value at the shadow boundary. If false (default value), the properties continue to inherit. If true, the properties are set to initial value.

Property of [dom/shadowdom/ShadowRoot](/dom/shadowdom/ShadowRoot)[dom/shadowdom/ShadowRoot](/dom/shadowdom/ShadowRoot)

## Syntax

``` js
var result = element.resetStyleInheritance;
element.resetStyleInheritance = value;
```

## Return Value

Returns an object of type BooleanBoolean

If false (default value), the properties continue to inherit. If true, the properties are set to initial value.

## Usage

     Reflected in the reset-style-inheritance HTML attribute.
