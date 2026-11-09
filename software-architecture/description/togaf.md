# TOGAF

## Summary

TOGAF (The Open Group Architecture Framework) is a widely adopted enterprise architecture framework that provides a methodology and tools to design, plan, implement, and govern enterprise architectures. It focuses on aligning IT infrastructure with business objectives, improving efficiency, and reducing risks.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

TOGAF (The Open Group Architecture Framework) is a widely adopted enterprise architecture framework that provides a methodology and tools to design, plan, implement, and govern enterprise architectures. It focuses on aligning IT infrastructure with business objectives, improving efficiency, and reducing risks.

Initially developed in 1995 by **The Open Group**, TOGAF has evolved to become one of the most comprehensive frameworks in enterprise architecture.

### Key components

#### 1. Architecture development method (ADM)

The ADM is the central feature of TOGAF, describing an iterative process to develop and manage enterprise architecture:

- **Preliminary Phase**: Prepare the organization for architecture development.
- **Phase A: Architecture Vision**: Define the scope, goals, and vision for the architecture.
- **Phase B: Business Architecture**: Develop business processes and organizational structure.
- **Phase C: Information Systems Architecture**: Address data and application architectures.
- **Phase D: Technology Architecture**: Define technology infrastructure.
- **Phase E: Opportunities and Solutions**: Identify implementation projects.
- **Phase F: Migration Planning**: Develop a roadmap for implementation.
- **Phase G: Implementation Governance**: Ensure compliance during execution.
- **Phase H: Architecture Change Management**: Manage and adapt to changes.
- **Requirements Management**: Continuously capture and manage requirements throughout all phases.

#### 2. Enterprise continuum

A conceptual repository for all architecture artifacts:

- **Foundation Architectures**: Generic architectures (e.g., technical standards).
- **Common Systems Architectures**: Building blocks like security or networking.
- **Industry Architectures**: Specific to industries like healthcare or finance.
- **Organization-Specific Architectures**: Tailored to an organization's unique needs.

#### 3. Architecture content framework

Defines standard **artifacts**:

- **Deliverables**: Outputs for stakeholders, such as reports or blueprints.
- **Artifacts**: Individual elements like diagrams, matrices, or catalogs.
- **Building Blocks**: Reusable components, categorized as:
    - **Architectural Building Blocks (ABBs)**: Logical-level components.
    - **Solution Building Blocks (SBBs)**: Physical implementations.

#### 4. TOGAF reference models

- **TOGAF Technical Reference Model (TRM)**: Provides a foundation for defining technical architecture.
- **Integrated Information Infrastructure Reference Model (IIIRM)**: Supports the requirements of an integrated digital environment.

#### 5. Architecture capability framework

Provides tools and processes to establish an architecture practice:

- Skills management.
- Governance models.
- Architecture maturity assessments.

## Worked example

### Implementation

#### Step 1: establish architecture capability

- Set up an architecture team and define governance structures.
- Secure executive sponsorship and define key stakeholders.

##### Step 2: define scope and vision

- Use the **Preliminary Phase** and **Phase A** of the ADM to establish objectives, scope, and architecture principles.

###### Step 3: conduct iterative ADM cycles

- Work through the ADM phases iteratively to develop architecture for each domain:
    - Business
    - Data
    - Application
    - Technology

###### Step 4: use building blocks

- Identify reusable components (ABBs and SBBs) for efficiency and consistency.

###### Step 5: develop roadmaps

- Use **Phase E** (Opportunities and Solutions) and **Phase F** (Migration Planning) to create actionable roadmaps for implementation.

###### Step 6: implement and govern

- Ensure projects align with architecture goals using **Phase G** (Implementation Governance).

###### Step 7: adapt and evolve

- Manage changes through **Phase H** (Architecture Change Management).

### Practical example

#### Scenario: implementing a digital transformation strategy

1. **Preliminary Phase**: Assemble an enterprise architecture team and define governance.
2. **Phase A**: Identify goals like enhancing customer experience and reducing operational costs.
3. **Phase B**: Map out business processes and identify areas for automation.
4. **Phase C**: Define data flows between legacy systems and new digital platforms.
5. **Phase D**: Design cloud-based infrastructure for scalability and security.
6. **Phase E**: Propose solutions such as CRM integration or cloud migration.
7. **Phase F**: Create a phased implementation plan with milestones.
8. **Phase G**: Monitor project execution to ensure alignment with the architecture.
9. **Phase H**: Regularly review and update the architecture to adapt to new requirements.

##### TOGAF vs. other frameworks

| Aspect | TOGAF | Zachman | IAF |
| --- | --- | --- | --- |
| **Focus** | Methodology for architecture design | Classification of architecture | Integration of architecture |
| **Structure** | Iterative and process-driven | Grid-based | View-driven |
| **Artifacts** | Comprehensive and reusable | Focused on classification | Tailored to domains |
| **Flexibility** | High, adaptable to various industries | Moderate | High |
| **Best For** | Large organizations with complex needs | Academic or theoretical use | Organizations with multiple domains |

## Trade offs and when to use it

### Advantages

1. **Comprehensive Framework:** Covers all aspects of enterprise architecture, including methodology, content, and governance.
2. **Flexibility:** Can be tailored to specific organizational needs and integrated with other frameworks.
3. **Iterative Approach:** Supports continuous improvement and adaptation.
4. **Focus on Reusability:** Encourages the use of building blocks to save time and resources.
5. **Widely Recognized:** Supported by a global community and extensive resources.

#### Challenges of TOGAF

1. **Complexity:** Requires significant training and expertise to implement effectively.
2. **Resource Intensive:** Needs a dedicated team, tools, and executive commitment.
3. **Time-Consuming:** Iterative cycles can be lengthy, especially for large organizations.
4. **Abstract Artifacts:** Some artifacts and processes may seem overly theoretical for smaller teams.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- The Open Group (2022). [*The TOGAF Standard, 10th Edition*](https://www.opengroup.org/togaf). The Open Group. The current version of the TOGAF standard and its Architecture Development Method.

TODO: check the content of this note against the sources above and record what was verified and when.
