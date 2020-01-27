JSON Merge Patch
================
The patch document has the same structure as the original JSON resource, but includes just the subset of fields that should be changes or added. 

Optionally, a field can be deleted by specifying `null` for the field value. Consequently, JSON Merge Patch is not suitable if the original resource can have explicit null values.

For example, if the original resource has the following JSON representation:

```json
{
    "name": "gizmo",
    "category": "widgets",
    "color": "blue",
    "price": 10
}
```

a possible JSON Merge Patch document can be:

```json
{
    "price": 12,
    "color": null,
    "size": "small"
}
```

This will:

* update `price` from `10` to `12`
* delete `color`
* add `size`

JSON Merge Patch is not suitable if the original resource can caontain explicit null values, due to the special meaning of `null` in the patch document.

Also, the patch document doesn't specify the order that the server should apply the updates. That may or may not matter, depending on the domain.

JSON Merge Patch is defined in [RFC 7396](https://tools.ietf.org/html/rfc7396). The media type is `application/merge-patch+json`.
