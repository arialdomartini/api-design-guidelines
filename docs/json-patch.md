JSON Patch
==========

A JSON Patch document specifies the changes as a sequence of operations to apply. Operations include add, replace, copy and test (to validate values).

For example, if the original resource has the following JSON representation:

```json
{
    "name": "gizmo",
    "category": "widgets",
    "color": "blue",
    "price": 10
}
```

a possible JSON Patch document could be:

```json
{
    { "op": "replace", "path": "/price", "value": 12 },
    { "op": "remove",  "path": "/color" },
    { "op": "add",     "path": "/size",  "value": "small" }
}
```

This will:

* update `price` from `10` to `12`
* delete `color`
* add `size`

performing the operations in this exact order.

JSON Patch is defined in [RFC 6902](https://tools.ietf.org/html/rfc6902) and described in the site [jsonpatch.com](http://jsonpatch.com/). The media type is `application/json-patch+json`.
