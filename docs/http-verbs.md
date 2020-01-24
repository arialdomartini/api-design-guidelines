HTTP Verbs
==========

The HTTP protocol defines a number of methods that assign semantic meaning to a request. We use the following semantic:

* `GET` retrieves the representation of the resource at the specified URI.
* `POST` creates a new resource at the specified URI. The body of the request message provides the state representation of the new resource. The response contains the created resource, included the URI to itself.

* `PUT` either creates or replaces the resource at the specified URI. jthe body of the request messages provides the resource.

* `DELETE` removes the resource at the specified URI.

* `PATCH` perform a partial update of a resource. The request body specified the set of changes to apply to the resource.

Resources needn't support all the verbs.

The effect of a specific request should depend on wheter the resouce is a collection or an individual item. For example, a `[DELETE]` call to `/api/items` would delete the whole collection of items.

## Example

| Resource                | POST                               | GET                                     | PUT                                        | DELETE                                     |
| ----------------------- |------------------------------------| ----------------------------------------|--------------------------------------------|--------------------------------------------|
| `/customers`            | Create a new customer              | Retrieves all customers                 | Bulk update all customers                  | Delete all customers                       |
| `/customers/1`          | Unsupported/Error                  | Retrieves specific customer             | Update specific customer                   | Delete specific customer                   |
| `/customers/1/orders`   | Create order for specific customer | Get orders of specific customer         | Bulk update orders of specific customer    | Delete all orders of specific customer     |
| `/customers/1/orders/2` | Unsupported/Error                  | Get specific order of specific customer | Update specific order of specific customer | Delete specific order of specific customer |


## Difference between POST, PUT and PATCH

The difference between `POST`, `PUT` AND `PATCH` is subtle and can be confusing.

* A `POST` creates a resource letting the server assign the URI. The URI of the created resource is returned to the client with a hypermedia links. When the client invokes `POST`, the resulting URI of the resource is still unknown.
* A `PUT` creates or updates a resource whose URI is known to the client. 
  * If no resource exists at the provided URI, the resource is created
  * If a resouce exists at the provided URI, the resource is updated.

  In either cases, when the client invoked `PUT`, the resource's URI is known.

Usually `POST` and `PUT` are invoked against the URI of a collection: in this case, the new resource is added to the collection.

Support creation via `PUT` is optional and depends on:

* whether the client can meaningfully assign a URI to a resource before it exists;
* the associated implementation cost.

`GET`, `PUT` and `PATCH` should be idempotent: if a client submits the same `GET` or `PUT` request multiple time, the results should always be the same (the same resource is returned/the same resource is modified with the same values`.

`POST` and `DELETE` are not guaranteed to be idempotent.


## Supported verbs
### GET
A successful `GET` returns `200 OK`; the body generally contains the resource.

If the resource cannot be found, `GET` returns `404 Not Found`. The body may contain some detail.

When the resource cannot be accessed, the returned status code depends on [security concerns](security.md#get):

* if authentication was required and the user provided none, the API returns `401 Unauthorized`
* if the user is authenticated but does not have the rights to access that resource, we generally return `404 Not Found`. [We prefer not to return `403 Forbidden`](security.md#authenticated-users-and-private-information).

