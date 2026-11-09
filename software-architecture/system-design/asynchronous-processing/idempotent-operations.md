# Idempotent operations

## Summary

Idempotent operations are operations that can be applied multiple times without changing the result beyond the initial application. In other words, if an operation is idempotent, it will have the same effect whether it is executed once or multiple [times.It](http://times.It) is also important to understand the benefits of idempotent operations, especially when using message or task queues that do not guarantee exactly once processing. Many queueing systems guarantee at least once message delivery or processing. These systems are not completely synchronized, for instance, across geographic regions, which simplifies some aspects of their implementation or design.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

Idempotent operations are operations that can be applied multiple times without changing the result beyond the initial application. In other words, if an operation is idempotent, it will have the same effect whether it is executed once or multiple [times.It](http://times.It) is also important to understand the benefits of idempotent operations, especially when using message or task queues that do not guarantee *exactly once* processing. Many queueing systems guarantee *at least once* message delivery or processing. These systems are not completely synchronized, for instance, across geographic regions, which simplifies some aspects of their implementation or design. Designing the operations that a task queue executes to be idempotent allows one to use a queueing system that has accepted this design trade-off.

#### Importance

- **Fault Tolerance**: Ensures that repeated operations (due to network issues, retries, or errors) do not cause unintended changes.
- **Consistency**: Maintains data consistency and integrity, preventing duplication or incorrect data states.
- **Simplified Error Handling**: Simplifies error recovery processes since repeated operations will not alter the end state.

### How to achieve

**Idempotence ensures that the same request leads to the same system state, and no action is unintentionally executed more than once.**

**Generation of Idempotence Key**

- **Client-Side Generation**: The client generates a unique key (often using UUIDs, timestamps, or a combination of unique parameters) and includes it with each request.
- **Server-Side Generation**: In some cases, the server might generate and provide the key to the client for use in subsequent operations.

**Storing the Idempotence Key**

- **Database or Cache**: The server stores the key along with the result of the operation in a database or cache. This storage acts as a record to check against future requests.

**Checking for Duplicates**

- **Request Handling**: Upon receiving a request, the server checks if the key already exists in the storage.
- **Duplicate Detection**: If the key is found, the server recognizes the request as a duplicate and returns the previously stored response, ignoring the operation.
- **New Request**: If the key is not found, the server processes the request, stores the result along with the key, and returns the response.

**Key Expiry**

- **Retention Policy**: Implementing a retention policy to remove old keys after a certain period to manage storage and performance.
- **Garbage Collection**: Periodically cleaning up expired keys to maintain efficiency.

#### Idempotence key

A unique identifier associated with a specific request or operation. This key is used to recognize and discard duplicate requests, ensuring that an operation is processed only once.

#### Idempotence and REST

Let’s have a brief look at how idempotency applies to HTTP verbs, which are important to understand when we want to build a REST API. A very detailed reference of all HTTP verbs can be found in [RFC 7231](https://tools.ietf.org/html/rfc7231).

The following table shows which verbs are (or should be) idempotent.

| Operation | Idempotent |
| --- | --- |
| GET | Y |
| HEAD | Y |
| OPTION | Y |
| POST | N |
| PUT | Y |
| PATCH | N |
| DELETE | Y |
| TRACE | Y |

**GET, HEAD, and OPTION are clearly idempotent as they only read data**, but don’t create, update or delete any resources.

**PUT is idempotent as it updates a resource or creates a new one if it doesn’t exist.** If we sent the same update multiple times, the resource shouldn’t change.

POST doesn’t have to be idempotent as it creates a new resource and, if called again, usually creates another resource. However, it can be implemented as an idempotent operation as well.

The PATCH operation updates a resource partially and doesn’t necessarily have to be idempotent.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Martin, D.. [*The System Design Primer*](https://github.com/donnemartin/system-design-primer). GitHub. A widely used open overview of system design building blocks such as asynchronism, queues, back pressure, caching and consistency.
- Fielding, R., Nottingham, M., Reschke, J. (2022). [*RFC 9110: HTTP Semantics*](https://www.rfc-editor.org/rfc/rfc9110.html). IETF. The current specification of HTTP methods, status codes, headers and the meaning of idempotent and safe methods.

TODO: check the content of this note against the sources above and record what was verified and when.
