# Availability monitoring

## Summary

A healthy system needs all parts to be available, with availability monitoring tracking uptime statistics, distinct from health monitoring's real-time status. Systems often have redundant components like databases for seamless failover during faults, aiming for uninterrupted user experience. Availability monitors must collect extensive failure data to pinpoint causes and prevent recurrences.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

A healthy system needs all parts to be available, with availability monitoring tracking uptime statistics, distinct from health monitoring's real-time status.

Systems often have redundant components like databases for seamless failover during faults, aiming for uninterrupted user experience. Availability monitors must collect extensive failure data to pinpoint causes and prevent recurrences.

Tracking availability involves various application-specific factors. An effective monitor records this data and synthesizes it to reflect overall system health. For instance, in e-commerce, order processing depends on both the order storage and payment processing subsystems' availability.

### Requirements

An operator should also be able to view the historical availability of each system and subsystem, and use this information to spot any trends that might cause one or more subsystems to periodically fail.

A monitoring solution should provide real-time and historical data on subsystem availability, swiftly alert operators of service failures or user connection issues, track user actions, and issue alerts for excessive connectivity failures within a set timeframe.

### Analyzing availability data

The instrumentation data must be aggregated and correlated to support the following types of analysis:

- The immediate availability of the system and subsystems.
- The availability failure rates of the system and subsystems. Ideally, an operator should be able to correlate failures with specific activities: what was happening when the system failed?
- A historical view of failure rates of the system or any subsystems across any specified period, and the load on the system (number of user requests, for example) when a failure occurred.
- The reasons for unavailability of the system or any subsystems. For example, the reasons might be service not running, connectivity lost, connected but timing out, and connected but returning errors.

You can calculate the percentage availability of a service over a period of time by using the following formula:

```text
%Availability =  ((Total Time - Total Downtime) / Total Time ) * 100
```

This is useful for SLA purposes. The definition of *downtime* depends on the service.

For example, Visual Studio Team Services Build Service defines downtime as the period (total accumulated minutes) during which Build Service is unavailable. A minute is considered unavailable if all continuous HTTP requests to Build Service to perform customer-initiated operations throughout the minute either result in an error code or do not return a response.

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
