Pagination
==========

For requests that can potentially return a large number of items, we support pagination: the URI can contain standardized URL parameters specifying the subset of information to return.

```
/orders?limit=25&offset=3
```

When not provided, the two parametrs default to meaningful values (for example: `limit` could default to `100` and `offset` to `0`). The default values can be defined case by case depending on the specific payload, or there could be a default for the whole API.


## Metainformation and links to other pages

The returned payload should provide details about:

* the current page (its number and size)
* the total number of pages or items
* links to previous and next pages, and optionally the first and the last pages

For example:


```
/orders?limit=10&offset=50
```

could return


```json
{
    "orders": [
        ...
    ],
    "pages": 184,
    "next": "/orders?limit=25&offset=4",
}
```

or even a more comprehensive:

```json
{
    "orders": [
        ...
    ],
    pagination: {
        "offset": 3,
        "limit": 25,
        "total": 4600,
        "pages": 184,
        "next": "/orders?limit=25&offset=4",
        "previous": "/orders?limit=25&offset=2",
        "first": "/orders?limit=25&offset=0",
        "last": "/orders?limit=25&offset=0"
    }
}
```
