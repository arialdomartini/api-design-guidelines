| HTTP Status Code             | Meaning                                                                                                                                       |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `201 Created`                | The resource has been successfully created. The created resource is included in the response body                                             |
| `200 OK`                     | The requested resource has been found and returned in the response body                                                                       |
| `200 No Content`             | The resource has been successfully created. No resource is included in the responde body                                                      |
| `401 Unauthorized`           | The client must authenticate                                                                                                                  |
| `400 Bad Request`            | The data provided by the client is invalid. Additional information about the error might be included in the response body                     |
| `422 Unprocessable Entity`   | The request is syntactically correct, but it cannot be processed due to semantic errors (i.e. the resource would be move to an invalid state) |
| `406 Not Acceptable`         | The media type specified by the client in `Content-Type` is not supported by the API                                                          |
| `415 Unsupported Media Type` | None of the media types listed in `Accept` are supported by the API                                                                           |

