Richardson's Maturity Model
===========================

The [Maturity Model](https://martinfowler.com/articles/richardsonMaturityModel.html) defines the following levels for Web APIs:

* Level 0: the API defines one single URI, accessed via `POST`; all operations are specified in the body.
* Level 1: the API defines separate URIs for individual resources.
* Level 2: operations on resources are defined using HTTP methods
* Level 3: the state change is driven by consuming hypermedia links (HATEOAS)

Level 3 corresponds to a truly RESTful API according to Roy Fielding's definition. In pracice, may published Web APIs fall somethere around Level 2.

We generally aim to design APIs of the highest level, but we compromise to use the Level 2 accordinging to the circumstances.
