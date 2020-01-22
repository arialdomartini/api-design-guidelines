REST
====

REST (REpresentatnal State Transfer) is an architectural style for building distributed systems, designed around:

* Hypermedia

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
    
    "self": "https://mycompany.com/api/orders/12",
    "customer": "https://mycompany.com/api/customer/100",
    "items": "https://mycompany.com/api/orders/12/items"
}
```

* A uniform interface based on HTTP *verbs* (`GET`, `POST`, `DELETE`, etc)

* A stateless request model, without keeping transient state information between requests. The only place where information is stored is in the resources themselves, and each request should be an atomic operation. Any server can handle any request from any client.
