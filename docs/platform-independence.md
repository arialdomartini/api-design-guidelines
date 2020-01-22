Platform Independence
=====================

Any client should be able to call the API, regardless of how the API is implemented internally. This require using [standard protocols](standard-protocols), and having a mechanism wherebny the client and the web service can agree on the format of the data to exchange.

We avoid introducing dependencies between the Web API and the underlying data sources. For example, if data is strored in a relational database, the Web API doesn't need to expose each table as a collection of resources. We prefer thinking of the Web API as an abstraction of the business logic.
