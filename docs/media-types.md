# Media types

Client and servers echange representations of resources. In the HTTP protocol, formats are specified through the use of *media types*, called MIME types. 

For non-binary data, we use JSON (media type `application/json`).

The client can specify the desired media type by using the HTTP header field `Content-Type`. If this is not specified, `application/json` is intended. 

If the server doesn't support the requested media type, it returns `415 Unsupported Media Type`.
