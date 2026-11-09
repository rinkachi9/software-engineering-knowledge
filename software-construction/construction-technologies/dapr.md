# Dapr (Distributed Application Runtime)

## Summary

Dapr is a portable, event-driven runtime that exposes standardized, language-agnostic APIs (“building blocks”) for common distributed-systems concerns, service-to-service calls, pub/sub, state, workflow, actors, secrets, config, bindings, resiliency, and observability, implemented via a sidecar process you call over HTTP/gRPC.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

**Dapr is a portable, event-driven runtime that exposes standardized, language-agnostic APIs (“building blocks”) for common distributed-systems concerns, service-to-service calls, pub/sub, state, workflow, actors, secrets, config, bindings, resiliency, and observability, implemented via a sidecar process you call over HTTP/gRPC.**

### Why use

- **Productivity & portability.** Call `POST /v1.0/state/...` or `.../invoke/...` and switch implementations (Redis↔Cosmos DB, Kafka↔RabbitMQ, etc.) without changing app code; you only swap Dapr **components** (YAML).
- **Polyglot by design.** Any language that can speak HTTP/gRPC works (SDKs for .NET, Go, Java, Python, JS, etc.).
- **Built-in resilience, security, and telemetry.** mTLS with a built-in CA (Sentry), SPIFFE identities, configurable retries/timeouts/circuit breakers, and native OpenTelemetry tracing.
- **Cloud and edge, self-hosted or Kubernetes, and first-class integration in Azure Container Apps.**

### Architecture

- **Sidecar pattern**: each app instance runs **`daprd`** alongside your process; your code calls the sidecar, and the sidecar talks to state stores, brokers, etc. On Kubernetes, the **sidecar injector** adds `daprd` to annotated pods.
- **Building blocks** (APIs): Service Invocation, Pub/Sub, State, Actors, Bindings, Secrets, Configuration, Workflow, **Jobs** (scheduling), plus cross-cutting **Resiliency** and **Observability**. You can adopt them independently.
- **Components**: pluggable adapters (YAML) that connect a building block to a concrete backend (Redis, Cosmos DB, DynamoDB; Kafka, RabbitMQ; Key Vault, Vault, etc.). Each component has a maturity level (alpha/beta/stable).

#### Building blocks

##### Service invocation

Direct, secure service-to-service calls with service discovery, retries, and timeouts handled by Dapr.

**Invoke URL pattern** (HTTP):

`POST ``http://localhost:3500/v1.0/invoke/{app-id}/method/{path}`

##### Publish/Subscribe

Topic-based messaging with CloudEvents envelopes; swap brokers without code changes (Kafka, RabbitMQ, Redis Streams, Pulsar, AWS SNS/SQS, Azure Event Hubs/Service Bus, GCP Pub/Sub, etc.).

##### State management

Key/value state with ETags & transactions across a variety of stores (Redis, Cosmos DB, DynamoDB, Cassandra, MongoDB, etc.).

##### Actors (virtual actors)

Per-ID single-threaded “grains” with timers/reminders and durable state, implemented over the state building block.

##### Bindings

Input/output bindings to external systems (including **Cron** as an input binding to trigger code on a schedule).

##### Secrets

Uniform API to retrieve secrets from providers like Kubernetes, Vault, Azure Key Vault; you can reference secrets in component YAMLs.

##### Configuration

Read-only key/value config with change subscriptions; separate from sidecar/control-plane configuration.

##### Workflow

In-sidecar workflow runtime; author workflows in code, manage via HTTP/gRPC; built atop Actors for durability.

##### Jobs (scheduling)

Schedule “do X at time T or every N minutes”; powered by the **Scheduler** control-plane service; currently maturing.

##### Resiliency & observability

Declarative **timeouts, retries, circuit breakers**; distributed tracing via **OpenTelemetry/OTLP** (plus Zipkin).

### Security model

**mTLS by default** between sidecars (Sentry = CA); each app gets a **SPIFFE ID** (`spiffe://<trustdomain>/ns/<namespace>/<appid>`). You can add **invoke ACLs**.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Comparison with other solutions

- **Versus a service mesh:** Both use sidecars, both can do mTLS and tracing, but **Dapr is an app runtime** (APIs for state/pubsub/etc.), **not** a networking mesh. They’re complementary and often run together.
- **Versus hand-rolled libs/SDKs:** You avoid provider lock-in and duplicated boilerplate; you trade that for learning Dapr and operating sidecars.

### Use cases

- **Polyglot microservices** where teams don’t want to bake cloud-specific SDKs into code.
- **Event-driven systems** (pub/sub) with multiple brokers across environments.
- **Stateful services** needing **idempotency, concurrency control (ETags)**, and **virtual actors**.
- **Edge + cloud** deployments and **Azure Container Apps** scenarios with managed Dapr.

### Pros & cons

#### Pros

- **Standardized APIs** for cross-cutting concerns; language & platform neutral.
- **Swappable providers** via components ⇒ less lock-in, faster experiments.
- **Built-in resilience/telemetry/security** (mTLS, retries, timeouts, circuit breakers, OTLP tracing).
- **Actors & Workflow** for durable, long-running processes.

#### Cons

- **Sidecar overhead** (extra container/process per app), memory/CPU and ops complexity; if you *also* run a service mesh, consider combined overhead and operational surface.
- **Component maturity varies** (alpha/beta/stable), verify status for your chosen store/broker.
- **Learning curve & debugging** through an abstraction; must understand both Dapr and your underlying backends.
- **Feature fit**: some advanced, provider-specific features may still require direct SDKs.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Dapr Authors. [*Dapr concepts*](https://docs.dapr.io/concepts/). Official description of the Dapr sidecar, building blocks and hosting modes.

TODO: check the content of this note against the sources above and record what was verified and when.
