# Security monitoring

## Summary

Security monitoring collects and analyzes events that may indicate an attack or misuse: failed sign-ins, unusual access patterns, changes to privileges and suspicious requests. It turns raw logs into alerts that let operators respond to incidents and provides evidence for audits.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

All commercial systems that include sensitive data must implement a security structure. The complexity of the security mechanism is usually a function of the sensitivity of the data. In a system that requires users to be authenticated, you should record:

- All sign-in attempts, whether they fail or succeed.
- All operations performed by, and the details of all resources accessed by, an authenticated user.
- When a user ends a session and signs out.

Monitoring can detect system attacks, such as multiple failed sign-in attempts signaling a brute-force attack or a spike in requests indicating a DDoS attack. It's essential to monitor all resource requests, as a sign-in flaw could expose resources without proper authentication.

### Requirements

The most critical aspects of security monitoring should enable an operator to quickly:

- Detect attempted intrusions by an unauthenticated entity.
- Identify attempts by entities to perform operations on data for which they have not been granted access.
- Determine whether the system, or some part of the system, is under attack from outside or inside. (For example, a malicious authenticated user might be attempting to bring the system down.)

To support these requirements, an operator should be notified if:

- One account makes repeated failed sign-in attempts within a specified period.
- One authenticated account repeatedly tries to access a prohibited resource during a specified period.
- A large number of unauthenticated or unauthorized requests occur during a specified period.

The information that's provided to an operator should include the host address of the source for each request. If security violations regularly arise from a particular range of addresses, these hosts might be blocked.

Quick detection of unusual system activity, like spikes in login attempts at odd hours (e.g., sign-ins at 3:00 AM with a normal 9:00 AM start), is crucial for security. Visualizing this data aids in monitoring and can inform time-based autoscaling decisions, allowing operators to scale authentication services up or down based on user login patterns.

### Analyzing security data

Security is crucial in distributed systems, with data originating from various sources. Adopt a SIEM approach to collect security information from events across the system, including application, network, and security devices.

Security monitoring can also include data from external security tools, helping administrators identify and counteract attacks. Data comes in various formats and detail levels, making analysis complex. For intricate cases, manual expert analysis of timestamped, raw data in a secure repository might be necessary.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Microsoft. [*Monitoring and diagnostics guidance*](https://learn.microsoft.com/en-us/azure/architecture/best-practices/monitoring). Microsoft Learn. Guidance on what telemetry to collect for health, availability, performance, security, SLA and usage monitoring, and how to analyze it.

TODO: check the content of this note against the sources above and record what was verified and when.
