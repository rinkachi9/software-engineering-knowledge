# ACID and BASE

## Summary

ACID stands for Atomicity, Consistency, Isolation, and Durability. It is a set of principles that ensure reliable processing of database transactions, particularly in relational databases.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

ACID stands for **Atomicity**, **Consistency**, **Isolation**, and **Durability**. It is a set of principles that ensure reliable processing of database transactions, particularly in relational databases.

**Purpose**: ACID principles help maintain the integrity of a database by guaranteeing that transactions are processed reliably, even in the event of system failures, errors, or concurrency issues.

### Components

#### Atomicity

Ensures that each transaction is treated as a single "atomic" unit, meaning either all operations within the transaction are executed successfully, or none are applied.

**Example**: In a bank transfer between accounts, if debiting the sender's account succeeds but crediting the recipient's account fails, the entire transaction is rolled back to avoid an inconsistent state.

**Implementation**: Managed through mechanisms like transaction logs and rollback protocols. The database records changes temporarily until the transaction is complete and can revert changes if any step fails.

##### Consistency

Ensures that any transaction brings the database from one valid state to another, maintaining the defined rules, constraints, and data integrity.

**Example**: If a transaction tries to write data that violates constraints (e.g., entering negative inventory values when negative quantities are disallowed), it will fail to keep the database consistent.

**Implementation**: Enforced by data validation rules, integrity constraints (e.g., foreign keys, check constraints), and triggers that maintain data accuracy according to the schema's defined rules.

###### Isolation

Guarantees that transactions are executed independently of each other, preventing one transaction’s intermediate changes from affecting others until it is complete.

**Example**: When two users simultaneously update the same record, isolation levels ensure that the transactions don’t interfere with each other, preventing dirty reads or non-repeatable reads.

**Isolation Levels**:

- **Read Uncommitted**: Allows transactions to see uncommitted changes from others, which may lead to dirty reads.
- **Read Committed**: Ensures transactions can only read committed changes from others, preventing dirty reads but not non-repeatable reads.
- **Repeatable Read**: Prevents dirty and non-repeatable reads but may still allow phantom reads.
- **Serializable**: The strictest level, where transactions are fully isolated from each other, effectively serializing their execution. This eliminates all anomalies but may reduce performance.

**Implementation**: Isolation is achieved through locking mechanisms, such as row-level and table-level locks, or through multi-version concurrency control (MVCC), which maintains multiple versions of data for concurrent transactions.

###### Durability

Ensures that once a transaction has been committed, the data changes are permanent, even in the event of a system crash or power failure.

**Example**: After committing a sale transaction in an e-commerce system, the purchase should be permanently recorded, even if the database crashes right after the commit.

**Implementation**: Achieved through techniques like write-ahead logging, which writes changes to a log before committing them, and by using checkpoints and backups to ensure data can be recovered after failures.

### Ensuring compliance

- **Transaction management**: Use a robust transaction management system that can track the state of transactions, including partially completed transactions, and roll back changes if needed.
- **Concurrency control**: Implement appropriate concurrency control strategies, such as locking or MVCC, tailored to the workload and the required isolation level.
- **Logging and recovery mechanisms**: Use logging (e.g., write-ahead logs) to record transaction states and implement recovery protocols to restore database consistency after failures.
- **Use of database-specific features**: Most relational databases (like MySQL, PostgreSQL, Oracle, and SQL Server) provide built-in mechanisms and configurations for achieving ACID compliance.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Impact

- **Data integrity**: ACID principles are crucial for maintaining high data integrity in environments where data accuracy is essential, like finance, healthcare, and e-commerce.
- **Transaction reliability**: ACID ensures that even in high-concurrency environments, transactions complete without corrupting data or compromising accuracy.
- **Performance vs. consistency trade-offs**: Achieving full ACID compliance can impact performance, particularly in high-transaction environments. Systems must balance between strict ACID compliance and scalability, depending on their consistency and speed needs.

### Challenges in implementing

- **Performance overhead**: Isolation levels, especially serializable isolation, can slow down systems by requiring more locks or data versioning, which can increase latency and reduce throughput.
- **Complexity in distributed systems**: Ensuring ACID compliance in distributed environments (e.g., across multiple servers or data centers) is challenging and often requires consensus protocols (like two-phase commit or Paxos) to synchronize transactions.
- **Scalability**: High levels of isolation can hinder the scalability of large databases, leading some distributed databases to opt for eventual consistency instead of strict ACID compliance.

### ACID vs. BASE

- **BASE (Basically Available, Soft state, Eventually consistent)**: Unlike ACID, BASE prioritizes availability and partition tolerance, allowing for temporary inconsistencies to achieve higher scalability. It is commonly used in systems requiring high availability over strict consistency.
- **When to Choose ACID or BASE**: Systems requiring high data integrity (e.g., banking) usually need ACID compliance, while those prioritizing speed and availability (e.g., social media feeds) often adopt BASE.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Haerder, T., Reuter, A. (1983). [*Principles of Transaction-Oriented Database Recovery*](https://doi.org/10.1145/289.291). ACM Computing Surveys. The paper that introduced the ACID acronym and the recovery concepts behind it.
- Kleppmann, M. (2017). *Designing Data-Intensive Applications*. O'Reilly Media. A rigorous treatment of replication, partitioning, transactions, consistency models and stream processing.

TODO: check the content of this note against the sources above and record what was verified and when.
