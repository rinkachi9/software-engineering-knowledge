# Abstract data types

## Summary

An abstract data type (ADT) defines a type by the operations it supports and their behavior, not by how the data is stored. A stack, for example, is defined by push and pop, whether it is built on an array or a linked list. Programming against ADTs gives modularity and lets the concrete implementation change without affecting its users.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

Abstract data types are organized around behaviors, not around the

construction of the data.

The concrete type of the object can change while still conforming to the

abstract data type.

We can also determine the type of an object dynamically, based on whether the object allows a

particular operation or not. We can invoke the operation directly, so it is rejected at runtime if it is

not supported, or the presence of the operation can be checked before with a query.

An abstraction and its set of allowable operations gives us modularity. This modularity gives us an

opportunity to design with interfaces. As programmers, we can use these interfaces to reveal our

intentions. When we design abstract data types to illustrate our intentions, then type becomes a

natural form of documentation, that never goes stale. Understanding types helps us to write better

code, so that others can understand our thinking at that point in time.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Cormen, T. H., Leiserson, C. E., Rivest, R. L., Stein, C. (2022). *Introduction to Algorithms, 4th Edition*. MIT Press. The standard reference for data structures and algorithms with proofs of their running times.
- Liskov, B., Zilles, S. (1974). [*Programming with Abstract Data Types*](https://doi.org/10.1145/942572.807045). ACM SIGPLAN Notices. The paper that introduced abstract data types as a programming language concept.

TODO: check the content of this note against the sources above and record what was verified and when.
