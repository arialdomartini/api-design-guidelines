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

## References
* [Microsoft - Web API design](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design)
* [Martin Fowler - Richardson Maturity Model](https://martinfowler.com/articles/richardsonMaturityModel.html)
* [Microsoft - Use HATEOAS to enable navigation to related resources](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design#use-hateoas-to-enable-navigation-to-related-resources)
