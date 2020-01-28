Filter data
===========

Requests (particularly, GET requests over collections resources) can potentially return a large number of items. We design the Web APIs to limit the amount of data returned by any single request. More generally, we design APIs with protection against Denial of Service in mind.

The API can allow passing a filter in the query string of the URI, such as:

```
/orders?minCost=1000&status=open
```

The Web API is then responsible for parsing and handling the `minCost` and `status` parameters and returning the filtered results on the server side.

Where it makes sense, URIs can also support query strings that specify the maximum number of items to retrieve. Where possible, we extend this approach to support pagination.

In any case, the URIs that are likely to return large amount of data are designed to have an upper limit on the number of items or on the size of the payload.

## GraphQL
We consider GraphQL is a viable approach, either in parallel to or as a replacement of REST. Since GraphQL can have a very deep impact on the client and on the possible evolution of the API, the decision to go with GraphQL must be taken together with the Architecture department.
