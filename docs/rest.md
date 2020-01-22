REST
====

REST (REpresentatnal State Transfer) is an architectural style for building distributed systems, designed around:



* *Resources*, which are any kind of object, data or services that can be accessed. Each resource has an *identifier*, a URI which uniquely identifies that resource. For example, the URI for a particular customer order might be:
```
https://mycompany.com/api/orders/12
```

* Clients interacts with the service by exchangind *representations* of resources and their states (usually in JSON). For example, a `GET` request to the URI listed above might return this response body:

```JSON
{
    "customerName": "John Smith",
    "orderValue": 99.90,
    "quantity": 2,
}
```

* Hypermedia links: the REST API is driven by hypermedia links that are contained in the representation. For example, the following shows a JSON representation of the above URI including the Hypermedia links. It contains links to get or update the associated customer and items:

```JSON
{
    "customerName": "John Smith",
    "orderValue": 99.90,
    "quantity": 2,
    
    "self": "https://mycompany.com/api/orders/12",
    "customer": "https://mycompany.com/api/customer/100",
    "items": "https://mycompany.com/api/orders/12/items"
}
```

* A uniform interface based on HTTP *verbs* (`GET`, `POST`, `DELETE`, etc)

* A stateless request model, without keeping transient state information between requests. The only place where information is stored is in the resources themselves, and each request should be an atomic operation. Any server can handle any request from any client.


## Maturity Model
The [Maturity Model](https://martinfowler.com/articles/richardsonMaturityModel.html) defines the following levels for Web APIs:

* Level 0: the API defines one single URI, accessed via `POST`; all operations are specified in the body.
* Level 1: the API defines separate URIs for individual resources.
* Level 2: operations on resources are defined using HTTP methods
* Level 3: the state change is driven by consuming hypermedia links (HATEOAS)

Level 3 corresponds to a truly RESTful API according to Roy Fielding's definition. In pracice, may published Web APIs fall somethere around Level 2.

We generally aim to design APIs of the highest level, but we compromise to use the Level 2 accordinging to the circumstances.
