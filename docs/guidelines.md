REST API Design Guidelines
==========================

A well designed Web API should aim to support:

* [Platform independence](platform-independence.md): clients should be able to consume the API regardless of how the API is implemented internally. This is obtained by using [standard](standards.md) design and procols, and by adopting a [REST](rest.md) approach.
* Service evolution: the Web API should be able to evolve and add functionalitiy independently from client applications. This is obtained by using [versioning](versioning.md). All the functionalities should be discoverable so that client applications can fully use it. This is obtained by [documenting the API](documenting.md).


## REST
We build web services according to [REST](rest.md) on HTTP, aiming to a [high maturity level](rest.md#maturity-model),  designed around:

* *Resources* with URI as URIs like `https://my-company.com/api/orders/12` that plays the role of unique identifiers;
* Clients exchange *representations* of resources states, using JSON;
* Hypermedia links, included in the representation for the API navigation;
* [Operations communicated using HTTP *verbs*](http-verbs.md) ([`GET`](http-verbs.md#get), [`POST`](http-verbs.md#post)[`DELETE`](http-verbs.md#delete), etc)
* A stateless request model.

We avoid creating APIs that simply mirror the internal database structure. On the contrary, [we build APIs around business flows](rest.md#organize-the-API-around-resources), trying to keep the [most convenient granularity level](granularity-level.md), neither too chatty nor too coarse-grained.

We strive to adopt a [consistent naming convention](rest.md#naming-conventions).

### Media types
About [media types](media-types.md), for non-binary payload we default to JSON (`application/json`).

The client can use the HTTP Header field `Content-Type` to request a different media type. If the server doesn't support it, it will return `415 Unsupported Media Type`.

### HTTP Status Codes
We use HTTP Status Codes to convey information about the processed operation, sticking to a consistent semantic. The list of HTTP Status Codes and the meaning we assign them is listed in [HTTP Status Codes](http-status-codes.md).

### Asynchronous Operations
Sometimes, operations might require processing that takes a while to complete. Rather than forcing the client to wait for completion before sending a response (which would cause unacceptable latency), we prefer to [make the operation asynchronous](asynchronous-operations.md), exposing endpoint that return the status of asynchronous requests so the client can monitor the status by polling it. Where possible, we promote the use of Web Hooks.

### Filter and paginate data
We hold back from providing clients too large amount of data when only a subset of the information is required. For example, suppose a client needs to find all orders with a cost over a specifid value. It might either retrieve all orders from `/orders` and the filter these orders on the client side, or let the server do the filtering. We promote the latter over the former. When an API can possibly return large amount of data, we design the endpoints to allow passing filters and pagination directives in the query string. 

In any case, in order to protect the APIs, we design them to have an upper limit to the possible amount of data handled.

## References
* [Microsoft - Web API design](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design)
* [Martin Fowler - Richardson Maturity Model](https://martinfowler.com/articles/richardsonMaturityModel.html)
* [Microsoft - Use HATEOAS to enable navigation to related resources](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design#use-hateoas-to-enable-navigation-to-related-resources)
* [JSON Merge Patch - RFC 7396](https://tools.ietf.org/html/rfc7396)
* [JSON Patch - RFC 6902](https://tools.ietf.org/html/rfc6902)
* [jsonpatch.com](http://jsonpatch.com/)
