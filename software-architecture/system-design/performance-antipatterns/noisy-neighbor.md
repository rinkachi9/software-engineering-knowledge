# Noisy neighbor antipattern

## Summary

Noisy neighbor refers to a situation in which one or more components of a system are utilizing a disproportionate amount of shared resources, leading to resource contention and reduced performance for other components. This can occur when a system is not properly designed or configured to handle the workload, or when a component is behaving unexpectedly.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

Noisy neighbor refers to a situation in which one or more components of a system are utilizing a disproportionate amount of shared resources, leading to resource contention and reduced performance for other components. This can occur when a system is not properly designed or configured to handle the workload, or when a component is behaving unexpectedly.

Examples of noisy neighbor scenarios include:

- One user on a shared server utilizing a large amount of CPU or memory, leading to reduced performance for other users on the same server.
- One process on a shared server utilizing a large amount of I/O, causing other processes to experience slow I/O and increased latency.
- One application consuming a large amount of network bandwidth, causing other applications to experience reduced throughput.

#### Considerations

In most cases, individual tenants don't intend to cause noisy neighbor issues. Individual tenants might not even be aware that their workloads cause noisy neighbor issues for others. However, it's also possible that some tenants might exploit vulnerabilities in shared components to attack a service, either individually or by executing a distributed denial-of-service (DDoS) attack.

Regardless of the cause, it's important to treat these problems as resource governance issues, and to apply usage quotas, throttling, and governance controls to mitigate the problem.

### Detecting the problem

From a client's perspective, the noisy neighbor problem typically manifests as failed requests to the service, or as requests that take a long time to complete. In particular, if the same request succeeds at other times and appears to fail randomly, there might be a noisy neighbor issue. Client applications should record telemetry to track the success rate and performance of the requests to services, and the applications should also record baseline performance metrics for comparison purposes.

From a service's perspective, the noisy neighbor issue might appear in several ways:

- **Spikes in resource usage.** It's important to have a clear understanding of your normal baseline resource usage, and to configure monitoring and alerts to detect spikes in resource usage. Ensure you consider all of the resources that could affect your service's performance or availability. These resources include metrics like server CPU and memory usage, disk IO, database usage, network traffic, and metrics that are exposed by managed services, such as the number of requests and the synthetic and abstract performance metrics, such as the Azure Cosmos DB request units.
- **Failures when performing an operation for a tenant.** In particular, look for failures that occur when a tenant isn't using a large portion of the system's resources. Such a pattern might indicate that the tenant is a victim of the noisy neighbor problem. Consider tracking the resource consumption by tenant. For example, when using Azure Cosmos DB, consider logging the request units used for each request, and add the tenant's identifier as a dimension to the telemetry, so that you can aggregate the request unit consumption for each tenant.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Microsoft. [*Noisy neighbor antipattern*](https://learn.microsoft.com/en-us/azure/architecture/antipatterns/noisy-neighbor/noisy-neighbor). Azure Architecture Center. The full description of the antipattern with its symptoms, how to detect it and how to fix it.

TODO: check the content of this note against the sources above and record what was verified and when.
