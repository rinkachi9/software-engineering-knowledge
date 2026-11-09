# Retry storm antipattern

## Summary

Retry Storm refers to a situation in which a large number of retries are triggered in a short period of time, leading to a significant increase in traffic and resource usage. This can occur when a system is not properly designed to handle failures or when a component is behaving unexpectedly. This can lead to Performance degradation, Increased resource utilization, Increased network traffic, and Poor user experience. To address retry storms, a number of approaches can be taken such as Exponential backoff, Circuit breaking, and Monitoring and alerting.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

### Definition

Retry Storm refers to a situation in which a large number of retries are triggered in a short period of time, leading to a significant increase in traffic and resource usage. This can occur when a system is not properly designed to handle failures or when a component is behaving unexpectedly. This can lead to Performance degradation, Increased resource utilization, Increased network traffic, and Poor user experience. To address retry storms, a number of approaches can be taken such as Exponential backoff, Circuit breaking, and Monitoring and alerting.

#### Reasons

When retries are performed at different layers in a deeply-nested distributed system, and a leaf-node dependency experiences an outage, the **impact can be massively magnified** when each intermediate client in the call chain makes local, context-free decisions to retry failed calls.

![Retry storm antipattern, figure 1](../../../_assets/software-architecture/retry-storm-figure-1.png)

Now imagine that each service has a retry policy installed which performs up to 3 retries on failed calls (a total of 3+1 requests). Think about what happens if D goes down, and this failure is propagated all the way back up the call chain:

- C calls D 4x more
- B calls C 4x more
- A calls B 4x more

![Retry storm antipattern, figure 2](../../../_assets/software-architecture/retry-storm-figure-2.png)

#### Considerations

- Clients should consider the type of error returned. Some error types don't indicate a failure of the service, but instead indicate that the client sent an invalid request. For example, if a client application receives a `400 Bad Request` error response, retrying the same request probably is not going to help since the server is telling you that your request is not valid.
- Clients should consider the length of time that makes sense to reattempt connections. The length of time you should retry for will be driven by your business requirements and whether you can reasonably propagate an error back to a user or caller. In most applications, retrying for a few seconds or minutes is sufficient.

### Detecting the problem

From a client's perspective, symptoms of this problem could include very long response or processing times, along with telemetry that indicates repeated attempts to retry the connection.

From a service's perspective, symptoms of this problem could include a large number of requests from one client within a short period of time, or a large number of requests from a single client while recovering from outages. Symptoms could also include difficulty when recovering the service, or ongoing cascading failures of the service right after a fault has been repaired.

### Solution

We need to limit retries in aggregate. The core problem is that the retry strategies commonly consider each request in isolation. Ideally, what we want is the ability to **enforce an upper bound on the total size of the traffic increase** at each layer in the service call stack. This can be mapped to the tried-and-true **Token Bucket algorithm**, where the token bucket’s refill rate is chosen considering typical traffic levels so the refill rate to be proportional to the underlying call rate (e.g. 1 retry allowed per every 1000 successful calls).

If a client typically makes a particular service call at a rate of 200 TPS, and we install a **rate-limiting retry policy** with a retry ratio of 0.01, then the maximum sustained increase in traffic that the client would generate during a dependency outage would be 2 additional TPS, or K=1.01, effectively eliminating the multiplier for all practical purposes.

1. Always rate-limit retries so that retries are allowed at a rate proportional to the rate of successful calls
2. Don’t retry when the dependency you are calling indicates that it is overloaded
3. For transient failures that warrant retrying, retry at most onceafter an initial call failure
4. Prefer Exponential Backoff and Jitter when scheduling retries
5. Use adaptive retry strategy which lets more traffic through when the downstream service is accepting it, and slows down the traffic it sends through when the downstream service starts failing requests
6. Be as explicit as possible about the Exceptions that should be retried

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Microsoft. [*Retry storm antipattern*](https://learn.microsoft.com/en-us/azure/architecture/antipatterns/retry-storm). Azure Architecture Center. The full description of the antipattern with its symptoms, how to detect it and how to fix it.

TODO: check the content of this note against the sources above and record what was verified and when.
