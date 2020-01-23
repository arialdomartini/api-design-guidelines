# Media types

Client and servers echange representations of resources. In the HTTP protocol, formats are specified through the use of *media types*, called MIME types. 

For non-binary data, we use JSON (media type `application/json`).

## Content Type

The client can specify the desired media type by using the HTTP header field `Content-Type`. If this is not specified, `application/json` is intended. 

For example:

```
POST https://my-company.com/orders HTTP/1.1
Content-Type: application/json; charset=utf-8
Content-Length: 57

{"Id":1,"Name":"Gizmo","Category":"Widgets","Price":1.99}
```

If the server doesn't support the requested media type, it returns `415 Unsupported Media Type`.


## Accept
A client request can include an `Accept` header that contains a list of media types the client will accept from the server. For example:

```
GET https://my-company.com/orders/2 HTTP/1.1
Accept: application/json,application/xml
```

The list of default media type is available on [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation/List_of_default_Accept_values). 

Services are generally required to support at least `application/json`. All other media types are supported based on the specific business or technical needs.
