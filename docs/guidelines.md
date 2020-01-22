REST API Design Guidelines
==========================

A well designed Web API should aim to support:

* [Platform independence](platform-independence.md): clients should be able to consume the API regardless of how the API is implemented internally. This is obtained by using [standard](standards.md) design and procols.
* Service evolution: the Web API should be able to evolve and add functionalitiy independently from client applications. This is obtained by using [versioning](versioning.md). All the functionalities should be discoverable so that client applications can fully use it. This is obtained by [documenting the API](documenting.md).


## REST
We design web services according to [REST](rest.md) on HTTP.

* Hypermedia
* *Resources* with URI as unique *identifiers* like `https://mycompany.com/api/orders/12`
* Clients exchange *representations* of resources states, using JSON.
* Operations are communicated using HTTP *verbs* (`GET`, `POST`, `DELETE`, etc)
* A stateless request model

## References
[Microsoft Azure Web API design](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design)
