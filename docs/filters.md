Filter data
===========

Requests (particularly, GET requests over collections resources) can potentially return a large number of items. We design the Web APIs to limit the amount of data returned by any single request. More generally, we design APIs with protection against Denial of Service in mind.

The API can allow passing a filter in the query string of the URI, such as:

```
/orders?minCost=1000&status=open
```

The Web API is then responsible for parsing and handling the `minCost` and `status` parameters and returning the filtered results on the server side.

Where it makes sense, URIs can also support query strings that specify the maximum number of items to retrieve:

```
/orders?limit=25
```

Where possible, we extend this approach to support [pagination](pagination.md):

```
/orders?limit=25&offset=50
```

In any case, the URIs that are likely to return large amount of data are designed to have an upper limit on the number of items or on the size of the payload.

## GraphQL
We consider GraphQL is a viable approach, either in parallel to or as a replacement of REST. Since GraphQL can have a very deep impact on the client and on the possible evolution of the API, the decision to go with GraphQL must be taken together with the Architecture department.

## Order
The URI can include URL parameters to sort items, such as:

```
/orders?sort=product
```

or

```
/orders?sort
```

## Selection of fields
It is technically possible to use URL parameters to linmit the fields returned for an item or a collection of items. For example, the request:

```
orders?fields=product,quantity
```

might be used to filter out all the Order's fields but `product` and `quantity`.

We don't see this approach as very convenient: where such a functionality is really needed, we take into consideration:

* [GraphQL](#graphql) into consideration.
* Field URIs, especially for large or peculiar Value Objects 

### Field URIs
In some cases, we allow that URIs can be augmented to address single fields of an Entity.

For example, if a GET request of

```
/users/12
```

returns

```json
{
    "name": "John ,
    "age": 55,
    "avatar": "TWFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5IGhpcyByZWFzb24sIGJ1dCBieSB0aGlz
        IHNpbmd1bGFyIHBhc3Npb24gZnJvbSBvdGhlciBhbmltYWxzLCB3aGljaCBpcyBhIGx1c3Qgb2Yg
        dGhlIG1pbmQsIHRoYXQgYnkgYSBwZXJzZXZlcmFuY2Ugb2YgZGVsaWdodCBpbiB0aGUgY29udGlu
        dWVkIGFuZCBpbmRlZmF0aWdhYmxlIGdlbmVyYXRpb24gb2Yga25vd2xlZGdlLCBleGNlZWRzIHRo
        ZSBzaG9ydCB2ZWhlbWVuY2Ugb2YgYW55IGNhcm5hbCBwbGVhc3VyZS4=
}
```

the API could allow the client to get the value of `avatar` by requesting

```
/users/12/avatar
```




[Value Objects](value-object.md)
