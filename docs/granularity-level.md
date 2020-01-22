Granularity Level
=================

We try to avoid too chatty Web API that expose a large number of small resources, by denormalizing the data and combining related information into bigger resources that can be handled with a single request.

In the meanwhile, we need to balance this approach against the overhead of fetching data that the client doesn't need and which would just increase the latency of the request, incurring additional bandwidth cost.

