# REST

## Summary

REST is an architectural style enforcing a client/server model where the client acts on a set of resources managed by the server. The server provides a representation of resources and actions that can either manipulate or get a new representation of resources. All communication must be stateless and cacheable.

## Prerequisites

- [Hypertext Transfer Protocol (HTTP)](../../computing-foundations/computer-networks-and-communications/http.md)

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

REST is an architectural style enforcing a client/server model where the client acts on a set of resources managed by the server. The server provides a representation of resources and actions that can either manipulate or get a new representation of resources. All communication must be stateless and cacheable.

Sample REST calls:

```http
GET /someresources/anId

PUT /someresources/anId
{"anotherdata": "another value"}
```

#### Advantages

- It is client/server: the business logic is decoupled from presentation. So you can change one without impacting the other. The **cons**, it adds negligible latency, but who cares, the web is the platform and everything is client/server.
- Statelessness means messages between client and server contain all necessary context, allowing for flexible routing and scaling through multiple server instances. Different servers can handle requests based on the message type, optimizing backend performance. However, this results in increased bandwidth usage due to redundant information in each message.
- It is cacheable, so if you were worried about latency you save bandwidth cacheing responses from the server.
- It uses a hypermedia-based uniform interface (HATEOAS), enhancing client-server decoupling. With server responses providing hypermedia for resources and actions related to the last request, clients only need an entry point and basic hypermedia conventions. This allows server-side changes without modifying the client code.

##### Disadvantages

- With REST being focused on exposing data, it might not be a good fit if resources are not naturally organized or accessed in a simple hierarchy. For example, returning all updated records from the past hour matching a particular set of events is not easily expressed as a path. With REST, it is likely to be implemented with a combination of URI path, query parameters, and possibly the request body.
- REST typically relies on a few verbs (GET, POST, PUT, DELETE, and PATCH) which sometimes doesn't fit your use case. For example, moving expired documents to the archive folder might not cleanly fit within these verbs.
- Fetching complicated resources with nested hierarchies requires multiple round trips between the client and server to render single views, e.g. fetching content of a blog entry and the comments on that entry. For mobile applications operating in variable network conditions, these multiple roundtrips are highly undesirable.
- Over time, more fields might be added to an API response and older clients will receive all new data fields, even those that they do not need, as a result, it bloats the payload size and leads to larger latencies.
- Versioning challenges: As an API evolves, versioning can become complex, requiring careful management of breaking changes and migration strategies to ensure backward compatibility.
- Complexity of authentication and authorization: Implementing secure authentication and authorization in RESTful APIs can be more complex than in other communication paradigms, as it often requires managing session state or using token-based authentication.

### How it works

There are four qualities of a RESTful interface:

- Identify resources (URI in HTTP) - use the same URI regardless of any operation.
- Change with representations (Verbs in HTTP) - use verbs, headers, and body.
- Self-descriptive error message (status response in HTTP) - Use status codes, don’t reinvent the wheel.
- HATEOAS (HTML interface for HTTP) - your web service should be fully accessible in a browser.

REST is focused on exposing data. It minimizes the coupling between client/server and is often used for public HTTP APIs. REST uses a more generic and uniform method of exposing resources through URIs, representation through headers, and actions through verbs such as GET, POST, PUT, DELETE, and PATCH. Being stateless, REST is great for horizontal scaling and partitioning.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### RPC vs REST

| Operation | RPC | REST |
| --- | --- | --- |
| Signup | **POST** /signup | **POST** /persons |
| Resign | **POST** /resign{"personid": "1234"} | **DELETE** /persons/1234 |
| Read a person | **GET** /readPerson?personid=1234 | **GET** /persons/1234 |
| Read a person’s items list | **GET** /readUsersItemsList?personid=1234 | **GET** /persons/1234/items |
| Add an item to a person’s items | **POST** /addItemToUsersItemsList{"personid": "1234";"itemid": "456"} | **POST** /persons/1234/items{"itemid": "456"} |
| Update an item | **POST** /modifyItem{"itemid": "456";"key": "value"} | **PUT** /items/456{"key": "value"} |
| Delete an item | **POST** /removeItem{"itemid": "456"} | **DELETE** /items/456 |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fielding, R. T. (2000). [*Architectural Styles and the Design of Network-based Software Architectures*](https://ics.uci.edu/~fielding/pubs/dissertation/top.htm). University of California, Irvine. The dissertation that defined REST and its constraints; chapter 5 is the primary source.
- Fielding, R., Nottingham, M., Reschke, J. (2022). [*RFC 9110: HTTP Semantics*](https://www.rfc-editor.org/rfc/rfc9110.html). IETF. The current specification of HTTP methods, status codes, headers and the meaning of idempotent and safe methods.

TODO: check the content of this note against the sources above and record what was verified and when.
