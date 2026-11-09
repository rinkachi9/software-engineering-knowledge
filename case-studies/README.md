# Case studies

Case studies describe how real systems were built and scaled, and connect the concepts in the knowledge areas to concrete engineering decisions.

This entry point is not part of the SWEBOK Guide. It holds case studies of real systems, and each case study links to the notes in the knowledge areas that explain the concepts it uses.

## Reading order

1. [Scaling Memcached at Facebook](facebook-memcached-scaling.md): Facebook used Memcached as a demand-filled look-aside cache in front of MySQL to serve billions of requests per second.
2. [Reddit architecture](reddit-architecture.md): Reddit serves traffic through a content delivery network and load balancers to application services that started as a Python monolith and are moving to Go microservices behind a federated GraphQL...

## Related elsewhere in the library

- [Caching](../software-architecture/system-design/caching.md): The caching concepts used in the Facebook and Reddit case studies.

## Planned topics

- Discord message storage
- Netflix microservices and resilience
- Shopify modular monolith
- Stack Overflow monolith at scale
- WhatsApp on Erlang
