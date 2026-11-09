# Partition tolerance

## Summary

A partition is when the network fails to deliver some messages to one or more nodes by losing them (not by delaying them - eventual delivery is not a partition).

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

A partition is when the network fails to deliver some messages to one or more nodes by losing them (not by delaying them - eventual delivery is not a partition).

The term is sometimes used to refer to a period during which *no* messages are delivered between two sets of nodes. This is a more restrictive failure model. We'll call these kinds of partitions *total partitions*.

The proof of CAP relied on a total partition. In practice, these are arguably the most likely since all messages may flow through one component; if that fails then message loss is usually total between two nodes.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gilbert, S., Lynch, N. (2002). [*Brewer's conjecture and the feasibility of consistent, available, partition-tolerant web services*](https://doi.org/10.1145/564585.564601). ACM SIGACT News. The formal proof of the CAP theorem, with precise definitions of consistency, availability and partition tolerance.

TODO: check the content of this note against the sources above and record what was verified and when.
