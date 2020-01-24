Failures
========

## Unaccessible resources

No operation should disclose the existence of resources to unauthorized users.  and should return `404 Not Found` instead of `403 Forbidded`.

When the resource cannot be accessed, the returned status code depends on [security concerns](security.md#get):

* if authentication was required and the user provided none, the API returns `401 Unauthorized`
* if the user is authenticated but does not have the rights to access that resource, we generally return `404 Not Found`. [We prefer not to return `403 Forbidden`](security.md#authenticated-users-and-private-information).

## Malformed requests
If the request is not syntactically correct (e.g. the payload is not a valid JSON), the API returns `400 Bad Request` signifying that the request cannot be even understood.

## Unprocessable requests
If the request is syntactically well-formed but was undable to be processed due to semantic errors, the API returns `422 Unprocessable Entity`. 

This typically happens when the request execution would take the system to an inconsistent state because a domain validation would fail, for example:

* a negative age is provided
* a unique constraint is violated
* a deletion would violate referential integrity

