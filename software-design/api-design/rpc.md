# Remote procedure call (RPC)

## Summary

In an RPC, a client causes a procedure to execute on a different address space, usually a remote server. The procedure is coded as if it were a local procedure call, abstracting away the details of how to communicate with the server from the client program. Remote calls are usually slower and less reliable than local calls so it is helpful to distinguish RPC calls from local calls. Popular RPC frameworks include Protobuf, Thrift, and Avro.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

In an RPC, a client causes a procedure to execute on a different address space, usually a remote server. The procedure is coded as if it were a local procedure call, abstracting away the details of how to communicate with the server from the client program. Remote calls are usually slower and less reliable than local calls so it is helpful to distinguish RPC calls from local calls. Popular RPC frameworks include Protobuf, Thrift, and Avro.

Sample RPC calls:

```http
GET /someoperation?data=anIdPOST /anotheroperation{  "data":"anId";  "anotherdata": "another value"}
```

RPC is focused on exposing behaviors. RPCs are often used for performance reasons with internal communications, as you can hand-craft native calls to better fit your use cases.

#### Advantage

- Helps clients communicate with servers through the traditional use of procedure calls in different languages.
- Can be used in local and distributed environments.
- Supports process-oriented and thread-oriented models.
- Hides the internal message-passing mechanism from the user, providing abstraction.
- Omits many of the protocol layers to improve performance.

#### Disadvantage

- RPC clients become tightly coupled to the service implementation.
- A new API must be defined for every new operation or use case.
- It can be difficult to debug RPC.
- You might not be able to leverage existing technologies out of the box. For example, it might require additional effort to ensure RPC calls are properly cached on caching servers such as Squid.

### Types

There are several RPC models and distributed computing implementations. One popular model and implementation is the Open Software Foundation's Distributed Computing Environment. The Institute of Electrical and Electronics Engineers defines RPC in its ISO Remote Procedure Call Specification, "ISO/IEC 11578:1996."

Examples of RPC configurations include the following:

- **Synchronous.** This is the standard method of RPC. The client makes a call and waits for a reply from the server.
- **Nonblocking.** The client makes a call, but instead of waiting for a reply, it continues with its own processing.
- **Batch-mode.** A client sends multiple nonblocking calls in a group.
- **Broadcast.** A client sends a message to multiple servers and then receives all the resulting replies.
- **Callback.** A client makes a nonblocking client-server call.

Alternative methods for client-server communication include message queueing, IBM's Advanced Program-to-Program Communication and Representational State Transfer (REST).

### How it works

RPC is a request-response protocol:

- Client program - Calls the client stub procedure. The parameters are pushed onto the stack like a local procedure call.
- Client stub procedure - Marshals (packs) procedure id and arguments into a request message.
- Client communication module - OS sends the message from the client to the server.
- Server communication module - OS passes the incoming packets to the server stub procedure.
- Server stub procedure - Unmarshalls the results, calls the server procedure matching the procedure id and passes the given arguments.
- The server response repeats the steps above in reverse order.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Birrell, A. D., Nelson, B. J. (1984). [*Implementing Remote Procedure Calls*](https://doi.org/10.1145/2080.357392). ACM Transactions on Computer Systems. The classic paper on RPC design: stubs, binding, transport and failure semantics.

TODO: check the content of this note against the sources above and record what was verified and when.
