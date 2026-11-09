# Change data capture

## Summary

Change data capture (CDC) detects every insert, update and delete in a database and publishes it as a stream of change events. Other systems, such as caches, search indexes and data warehouses, consume the stream to stay in sync without querying the source database repeatedly.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

**Change Data Capture -** Constant data changes make databases, data lakes, and data warehouses out of sync.

CDC or Change Data Capture can help you overcome this challenge.

CDC identifies and captures changes made to the data in a database, allowing you to replicate and sync data across multiple systems.

### Components

So, how does Change Data Capture work? Here's a step-by-step breakdown:

1 - Data Modification: A change is made to the data in the source database. It could be an insert, update, or delete operation on a table.

2 - Change Capture: A CDC tool monitors the database transaction logs to capture the modifications. It uses the source connector to connect to the database and read the logs.

3 - Change Processing: The captured changes are processed and transformed into a format suitable for the downstream systems.

4 - Change Propagation: The processed changes are published to a message queue and propagated to the target systems, such as data warehouses, analytics platforms, distributed caches like Redis, and so on.

5 - Real-Time Integration: The CDC tool uses its sink connector to consume the log and update the target systems. The changes are received in real time, allowing for conflict-free data analysis and decision-making.

Users only need to take care of step 1 while all other steps are transparent.

A popular CDC solution uses Debezium with Kafka Connect to stream data changes from the source to target systems using Kafka as the broker. Debezium has connectors for most databases such as MySQL, PostgreSQL, Oracle, etc.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Debezium Authors. [*Debezium Architecture*](https://debezium.io/documentation/reference/stable/architecture.html). Describes log-based change data capture with Kafka Connect connectors.
- Kleppmann, M. (2017). *Designing Data-Intensive Applications*. O'Reilly Media. A rigorous treatment of replication, partitioning, transactions, consistency models and stream processing.

TODO: check the content of this note against the sources above and record what was verified and when.
