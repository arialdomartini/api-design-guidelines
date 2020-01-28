Asynchronous Operations
=======================
When an operation requires a long processing time to complete, we take into consideration one of the 2 following approaches: 

* Implicit Asynchronous Resource: the API returns `202 Accepted` to indicate that the request was accepted for processing, but is not completed yet; the API exposes an endpoint that returns the status of the asynchronous request, so the client can monitor the status by polling the status endpoint
* Explicit Asynchronous Resource: the API returns `201 Created` and returns a resource representing the requested operation. The client monitors the state of that resource by polling its ordinary endpoints

The two approaches are very similar, but the latter is more explicit in representing the operation state with a pseudo-resource.

## Implicit Asynchronous Resource
Supposing that 

```
[GET] /api/train/12
```

returns the resource

```json
{
    "name": "Orient Express",
    "wagons": ["1", "2", "3"]
}
```

the client might require do add a new wagon to the train perfoming a `PUT` with the payload:

```json
{
    "name": "Orient Express",
    "wagons": ["1", "2", "3", "4"]
}
```

The API would return `202 Accepted`, providing in the HTTP Header field `Location` the status monitoring endpoint:

```
HTTP/1.1 202 Accepted
Location: /api/status/12345
```

In turn, the status monitoring endpoint would return a payload like:


```json
{
    "status": "In progress",
    "cancel": {
        "method": "delete",
        "href": "/api/status/12345
    }
}
```

The resource state would eventually update.


## Explicit Asynchronous Resource
In order to add a wagon to 

```
[GET] /api/train/12

{
    "name": "Orient Express",
    "wagons": ["1", "2", "3"]
}
```

the client would create a resource `WagonAddition`, by making a `POST` request to

```
[POST] /api/train/12/wagon-addition

{
    "wagon": "4"
}
```

The API would return `201 Created`, providing the respose:

```json
{
    "wagon": "4",
    "train": "/api/train/12",
    "status": "In progress",
    "self": "/api/train/12/wagon-addition/1577"
}
```

The state of this resource, which can be monitored by making `GET` requests to `/api/train/12/wagon-addition/1577`, will eventually update. In turn, the status monitoring endpoint would return a payload like:

The use of an explicit resource representing the operation would allow the client to provide a call back to be invoked at state changes:

```
[POST] /api/train/12/wagon-addition

{
    "wagon": "4",
    "callback": "https://my-client.com/api/train-state-notification"
}
```
