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

* Hypermedia links: the REST API is driven by hypermedia links that are contained in the representation. Once an application has a reference to a resource, it should be possible to use this reference to find items related to that resource. 


Rather than using the `Location` HTTP header, we prefer to include the URI in the returned resource as a hypermedia link.

For example, the following shows a JSON representation of the above URI including the Hypermedia links. It contains links to get or update the associated customer and items. 

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

See [Microsoft - Use HATEOAS to enable navigation to related resources](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design#use-hateoas-to-enable-navigation-to-related-resources)

* [A uniform interface based on HTTP *verbs*](http-verbs.md) (`GET`, `POST`, `DELETE`, etc)

* A stateless request model, without keeping transient state information between requests. The only place where information is stored is in the resources themselves, and each request should be an atomic operation. Any server can handle any request from any client.

## Maturity Model
We generally aim to design tryly RESTful APIs of the highest level of the [Maturity Model](maturity-model.md), where the state change is driven by consuming hypermedia links (HATEOAS)

Nontheless, we are open to relaxing the constraints accordinging to the circumstances.

## Organize the API around resources
We focus on the business entitites that the Web API exposes. 

### Pseudo resources
A Web API that implements simple calculator operations such as add and substract could provide URIs that expose these operations as pseudo resources and use the query string to specify the parameters required. For example, a `GET` to the URI 

```
/add?operand1=99&operand2=1
```

would return a response message with the body containing the value 100. However, we strive to use these forms of URIs as sparingly as possible. 

We rather prefere to `POST` the payload

```json
{
    "operand1": 99,
    "operand2": 1
}
```

to

```
/addition
```

and get back the pseudo-resource

```
{
    "result": 100
}
```



### Naming conventions

#### URIs
Resource URIs are based on nouns (the resource) and not verbs (the operations on the resouce). For example:

```
[POST] https://my-company.com/orders        // Good
[POST] https://my-company.com/create-order  // Avoid
```

A resource doesn't have to be based on a single pthisical data item. For example, an order resource might be implemented internally as several tables in a database, but presented to the client as a single entity. We avoid creating APIs that simply mirror the internal structure of a database. A client should not be exposed to the internal implementation.

All URIs are generally plural noums, regardless if they represent a collection or a single item. For example, the collectin of all orders might be:

```
[POST] https://my-company.com/orders
```

while a single order might have the URI:


```
[POST] https://my-company.com/orders/12
```

#### Collections
Entities can be grouped together into collections. A collection is a pearatate resource from the item withing the collection, and therefore it must have its own identifier URI. For example, the following might represent the collection of orders:

```
https://my-company.com/orders"
```

Each item in a collection has its own identifier URI. An HTTP GET request to that URI returns the deetails of that item.

Collections must be paginated.
