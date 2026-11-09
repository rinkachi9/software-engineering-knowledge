# Security patterns

Patterns that protect cloud applications by controlling identity, access and exposure of services and data.

This is a catalog section: it groups a large body of related notes inside the knowledge area. It is not a separate SWEBOK topic.

## Overview

Security provides confidentiality, integrity, and availability assurances against malicious attacks on information systems (and safety assurances for attacks on operational technology systems). Losing these assurances can negatively impact your business operations and revenue, as well as your organization’s reputation in the marketplace. Maintaining security requires following well-established practices (security hygiene) and being vigilant to detect and rapidly remediate vulnerabilities and active attacks.

## Reading order

1. [Federated identity pattern](federated-identity.md): Delegate authentication to an external identity provider.
2. [Gatekeeper pattern](gatekeeper.md): Protect applications and services by using a dedicated host instance to broker requests between clients and the application or service.
3. [Valet key pattern](valet-key.md): Use a token that provides clients with restricted direct access to a specific resource, in order to offload data transfer from the application.
