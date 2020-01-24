Security
========

## GET
### Unauthenticated users and private information
When unauthenticated clients tries to access private URIs, we generally return

```
403 Anauthorized
```

signifying that an authentication is needed.

Depending on the authentication process, the response' body and header may point the client toward the authentication entry-point.

### Authenticated users and private information
As a general rule, when the clients attempt to access protected data without having the relative right, we try to expose as few information as possible. 

For example, if an authenticated user `mallory` tries to read some private information owned by user `alice` by hitting:


```
[GET] https://my-company.com/api/user/alice/document/10
```

we prefer returning

```
404 Not Found
```

rather than

```
403 Forbidden
```

By returning `404 Not Found`, we avoid disclosing to `mallory` the existence of the target resource alltogether.
