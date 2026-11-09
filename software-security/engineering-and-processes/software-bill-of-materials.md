# Software bill of materials (SBOM)

## Summary

A software bill of materials (SBOM) is a machine readable inventory of the components, versions and dependencies that make up a piece of software. It lets an organization find out quickly whether it is affected by a newly published vulnerability or license problem, and it is increasingly required by regulation and customers.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

A **Software Bill of Materials (SBOM)** is a formal, machine-readable inventory of all components, libraries, and dependencies that make up a software application.

It is similar to a "ingredient list" for software, detailing:

- **Open-source components**
- **Proprietary code modules**
- **Third-party libraries**
- **Version information**
- **Licenses**
- **Known vulnerabilities**

An SBOM provides **visibility into the software supply chain**, enabling organizations to manage risks, improve security, and comply with regulations.

### Importance

SBOMs have become a **critical element** of modern software development, security, and compliance due to:

- **Increased supply chain attacks** (e.g., SolarWinds, Log4Shell)
- **Regulatory requirements** (e.g., U.S. Executive Order 14028 on cybersecurity)
- **Open-source adoption** and dependency sprawl
- **Need for faster vulnerability response**

### Key elements

A typical SBOM contains:

- **Component Name** (e.g., `log4j-core`)
- **Version** (e.g., `2.14.1`)
- **Unique Identifier** (e.g., Package URL or SWID tag)
- **Supplier Information** (vendor or author)
- **License Information**
- **Hash or Checksum** (integrity verification)
- **Dependency Relationships** (direct/indirect)
- **Vulnerability References** (CVE IDs)

### Standards and formats

SBOMs should follow **standardized formats** for interoperability:

- **SPDX (Software Package Data Exchange)**, ISO/IEC 5962
- **CycloneDX**, OWASP project focused on application security
- **SWID (Software Identification Tags)**, ISO/IEC 19770-2

### Best practices

- **Automate** SBOM creation in build processes.
- Use **signed SBOMs** to ensure authenticity.
- Cover **transitive dependencies** (indirect components).
- Maintain **SBOM version history** for traceability.
- Integrate SBOM checks into **security gates** of CI/CD pipelines.

### Regulatory and industry context

- **US Executive Order 14028** mandates SBOM use for software sold to the U.S. federal government.
- **NIST guidelines** recommend SBOMs for supply chain security.
- **Healthcare & critical infrastructure** sectors increasingly require SBOMs for compliance.

## Worked example

### Implementation

#### Planning

- Identify regulatory or contractual requirements.
- Decide on SBOM format(s) (e.g., SPDX, CycloneDX).
- Define scope (entire system, specific modules).

#### Generation

- Use automated tools to scan source code and dependencies.
    - Examples: **Syft**, **Trivy**, **Grype**, **CycloneDX CLI**, **OWASP Dependency-Check**
- Integrate SBOM generation into the **CI/CD pipeline**.

#### Storage

- Store SBOMs in a **version-controlled repository** or **artifact registry**.
- Ensure secure access and maintain historical SBOM versions.

#### Maintenance

- Update SBOMs with every release.
- Re-scan regularly to capture new vulnerabilities in existing components.

#### Consumption

- Use SBOMs in vulnerability management processes.
- Provide SBOMs to customers and partners for compliance.
- Integrate with **SCA (Software Composition Analysis)** and **SIEM** tools.

## Trade offs and when to use it

### Benefits

#### Security

- Identifies known vulnerabilities (via CVE databases).
- Reduces exposure to supply chain attacks.
- Facilitates rapid patching when a new vulnerability is disclosed.

#### Compliance

- Tracks licenses for all included components.
- Helps avoid legal risks from license violations.
- Supports audits and industry standards (e.g., ISO/IEC 5230, SPDX).

#### Transparency

- Improves understanding of what is inside the software.
- Builds trust with customers, partners, and regulators.
- Supports due diligence in software procurement.

#### Operational efficiency

- Enables faster incident response.
- Reduces time spent identifying and updating dependencies.
- Improves maintainability of legacy systems.

### Challenges

- **Accuracy**, Some tools may miss custom or binary dependencies.
- **Updating**, Dependencies change frequently, requiring continuous updates.
- **Integration**, Aligning SBOMs with vulnerability scanners and asset management.
- **Standard adoption**, Different customers or regulators may require different formats.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- NTIA (2021). [*The Minimum Elements For a Software Bill of Materials (SBOM)*](https://www.ntia.gov/report/2021/minimum-elements-software-bill-materials-sbom). U.S. Department of Commerce. Defines the minimum data fields, automation support and practices of an SBOM.
- OWASP. [*CycloneDX Specification*](https://cyclonedx.org/specification/overview/). One of the two main SBOM formats, maintained by OWASP and standardized as ECMA-424.
- Linux Foundation. [*SPDX Specification*](https://spdx.dev/use/specifications/). The other main SBOM format, published as ISO/IEC 5962.

TODO: check the content of this note against the sources above and record what was verified and when.
