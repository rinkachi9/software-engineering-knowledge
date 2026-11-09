# Eventual consistency

## Summary

Eventual consistency is a consistency model used in distributed computing, where updates to a data system are propagated across nodes asynchronously. Although the data may not be immediately consistent across all nodes, it eventually reaches a consistent state.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

Eventual consistency is a consistency model used in distributed computing, where updates to a data system are propagated across nodes asynchronously. Although the data may not be immediately consistent across all nodes, it eventually reaches a consistent state.

This model is common in distributed systems (e.g., cloud databases) where high availability and partition tolerance are prioritized, as in AP systems in the CAP theorem.

### Solving the challenges

#### Data replication and synchronization

- **Asynchronous Replication**: Updates are sent to other nodes in the background, reducing latency but requiring mechanisms to ensure all nodes eventually receive the update.
- **Gossip Protocols**: Nodes randomly communicate and exchange data updates, allowing eventual convergence without a centralized controller.

##### Conflict resolution

- **Timestamps and Vector Clocks**: Each update has a timestamp or a vector clock (a more complex form of tracking) to help nodes determine the latest version of the data.
- **Conflict-Free Replicated Data Types (CRDTs)**: CRDTs enable merging different states without conflicts, ensuring that all replicas converge to a single, consistent state eventually.

###### Read repair and anti-entropy

- **Read Repair**: When data is read, the system checks for consistency and triggers synchronization if nodes have different versions of the data.
- **Anti-Entropy Protocols**: Background processes compare and synchronize data between nodes periodically to ensure convergence.

###### Caching and stale data management

- **Cache Expiry**: Caches are designed to expire after a certain period, encouraging applications to check for more recent data.
- **Stale Tolerant UI Design**: Design interfaces to be resilient to slightly stale data by providing user feedback (e.g., "Last updated X seconds ago").

### Avoiding the problems

#### Choose strong consistency models

- **Strong Consistency**: Data updates are immediately visible to all users, but at the cost of potential delays and reduced availability. This model is best for applications requiring real-time data consistency, like banking.

##### Use transactions and consensus protocols

- **Two-Phase Commit (2PC)**: A distributed algorithm to ensure all nodes commit to a transaction. However, it’s resource-intensive and may not be scalable for large systems.
- **Paxos or Raft Protocols**: These consensus algorithms ensure consistency by making all nodes agree on a value before committing it. While more consistent, they add latency.

###### Design for idempotency

- **Idempotent operations**: Ensure that repeated operations (like retries) do not lead to inconsistent states. This way, even if nodes apply updates more than once, the final state remains correct.

###### Utilize distributed databases with strong consistency options

- Some databases offer configuration settings for consistency levels, allowing developers to set specific transactions or operations to prioritize consistency (e.g., “read your own writes”).

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Impact

- **Delayed data consistency**: Users may see outdated data temporarily, as updates take time to propagate to all nodes.
- **Improved availability**: Because nodes don’t wait for every update to reach all other nodes, the system can continue to function and remain available even under high loads or network partitions.
- **Scalability**: Eventual consistency allows distributed systems to scale better, as it enables more flexible data replication.
- **Complexity in development**: Applications must handle cases where data might be temporarily inconsistent, leading to added logic and complexity in code.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Vogels, W. (2009). [*Eventually Consistent*](https://doi.org/10.1145/1435417.1435432). Communications of the ACM. Defines eventual consistency and its variants (causal, read-your-writes, session, monotonic) from the perspective of a large scale system builder.

TODO: check the content of this note against the sources above and record what was verified and when.
