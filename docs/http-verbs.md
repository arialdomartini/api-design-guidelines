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

| Resource                | POST                               | GET                                     | PUT                                        | DELETE                                     |
| ----------------------- |------------------------------------| ----------------------------------------|--------------------------------------------|--------------------------------------------|
| `/customers`            | Create a new customer              | Retrieves all customers                 | Bulk update all customers                  | Delete all customers                       |
| `/customers/1`          | Unsupported/Error                  | Retrieves specific customer             | Update specific customer                   | Delete specific customer                   |
| `/customers/1/orders`   | Create order for specific customer | Get orders of specific customer         | Bulk update orders of specific customer    | Delete all orders of specific customer     |
| `/customers/1/orders/2` | Unsupported/Error                  | Get specific order of specific customer | Update specific order of specific customer | Delete specific order of specific customer |
