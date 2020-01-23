| HTTP Status Code             | Methods       | Meaning                                                                                                                   |
|------------------------------|---------------|---------------------------------------------------------------------------------------------------------------------------|
| `201 Created`                | `POST`, `PUT` | The resource has been successfully created. The created resource is included in the response body                         |
| `200 OK`                     | `GET`         | The requested resource has been found and returned in the response body                                                   |
| `200 No Content`             | `POST`, `PUT` | The resource has been successfully created. No resource is included in the responde body                                  |
| `400 Bad Request`            |               | The data provided by the client is invalid. Additional information about the error might be included in the response body |
| `406 Not Acceptable`         |               | The media type specified by the client in `Content-Type` is not supported by the API                                      |
| `415 Unsupported Media Type` |               | None of the media types listed in `Accept` are supported by the API                                                       |

