# Software Engineering Knowledge

A personal, language agnostic knowledge base of software engineering: concepts, principles, patterns and practices, organized by the knowledge areas of the SWEBOK Guide V4.0.

## Table of Contents

- [About](#about)
- [Purpose](#purpose)
- [Scope](#scope)
- [Knowledge areas](#knowledge-areas)
- [Full table of contents](#full-table-of-contents)
- [How to use this repository](#how-to-use-this-repository)
- [Reading the library](#reading-the-library)
- [Repository layout](#repository-layout)
- [Sources and migration](#sources-and-migration)
- [Contributing and working with AI agents](#contributing-and-working-with-ai-agents)
- [Status](#status)

## About

This repository collects what I learn about building software: requirements, architecture, design, construction, testing, operations and the foundations underneath them. Each note explains one idea in plain English, with an example and links to primary sources. The notes are written so that they are still useful when I come back after a year, and so that someone new to the topic can follow them from top to bottom.

This is a personal knowledge base, not a tutorial site or a product. The goal is depth and correctness.

## Purpose

The repository exists to:

- build a durable reference that I can search, extend and trust,
- force real understanding by requiring every concept to be explained precisely, with examples and analogies,
- keep one consistent standard for how knowledge is written down, so the collection stays coherent as it grows,
- provide a source of truth that both people and AI assistants can work with under the same rules.

## Scope

**In scope**

- Language agnostic software engineering: principles, patterns, architectural styles, methods, quality attributes, processes and the computing foundations they rely on.
- Worked examples, comparisons, checklists and decision guides. Code appears as an illustration in one declared language.
- Case studies of real systems, in my own words and with a link to the original source.

**Out of scope**

- Tutorials and reference material for one specific programming language or framework.
- Credentials, tokens, private keys, personal data or proprietary code from employers or clients.
- Text copied wholesale from books, courses or articles.

## Knowledge areas

The top level follows the 18 knowledge areas of the [Guide to the Software Engineering Body of Knowledge (SWEBOK Guide), Version 4.0](https://www.computer.org/education/bodies-of-knowledge/software-engineering), published by the IEEE Computer Society in 2024. Inside each knowledge area, the topic sections follow the topics of the corresponding SWEBOK chapter in the same order. A few catalog sections (for example design patterns and cloud design patterns) group large bodies of material that SWEBOK only names. Case studies have their own entry point.

| Knowledge area | What it covers |
| --- | --- |
| [Software requirements](software-requirements/README.md) | Eliciting, analyzing, specifying, validating and managing requirements. |
| [Software architecture](software-architecture/README.md) | Architecture fundamentals and description, architectural styles, distributed systems, system design and cloud design patterns. |
| [Software design](software-design/README.md) | Design principles, coupling and cohesion, domain-driven design, design patterns and API design. |
| [Software construction](software-construction/README.md) | Clean code, code reuse, the twelve-factor app and construction technologies. |
| [Software testing](software-testing/README.md) | Test levels, techniques, measures and testing practices such as TDD. |
| [Software engineering operations](software-engineering-operations/README.md) | Delivery, monitoring, service levels and operational metrics. |
| [Software maintenance](software-maintenance/README.md) | Evolving existing software, legacy code and technical debt. |
| [Software configuration management](software-configuration-management/README.md) | Version control, change control, versioning and releases. |
| [Software engineering management](software-engineering-management/README.md) | Planning, estimation, execution and measurement of software projects. |
| [Software engineering process](software-engineering-process/README.md) | Life cycles, process definition, assessment and improvement. |
| [Software engineering models and methods](software-engineering-models-and-methods/README.md) | Modeling with UML and methods such as agile, Scrum, Kanban and XP. |
| [Software quality](software-quality/README.md) | Quality models, quality attributes and quality assurance. |
| [Software security](software-security/README.md) | Secure development, software supply chain and API security. |
| [Software engineering professional practice](software-engineering-professional-practice/README.md) | Professionalism, teamwork and communication. |
| [Software engineering economics](software-engineering-economics/README.md) | Value, cost, estimation and decision making. |
| [Computing foundations](computing-foundations/README.md) | Data structures, programming paradigms, databases and network protocols. |
| [Mathematical foundations](mathematical-foundations/README.md) | Logic, sets, graphs, automata, counting and probability. |
| [Engineering foundations](engineering-foundations/README.md) | Engineering design, measurement, statistics and root cause analysis. |
| [Case studies](case-studies/README.md) | Real systems and the engineering decisions behind them. |

Where a topic fits two knowledge areas, it has one home note and the other area links to it. [GUIDELINE.md](GUIDELINE.md#311-placement-of-a-note) lists the primary home of each kind of topic.

## Full table of contents

[ToC.md](ToC.md) lists every file in the repository as an indented tree, with planned topics shown without links. Use it to see the whole structure at once. Use the knowledge area and section READMEs for the recommended reading order.

## How to use this repository

- To learn a topic, open the knowledge area, then the section, and read the notes in the order the section `README.md` gives.
- To look something up, start from [ToC.md](ToC.md) or search with `grep -rn "term" --include="*.md" .`.
- To find open gaps, run `grep -rn "^TODO:" --include="*.md" .`.

## Reading the library

This repository is set up for Librarian OS, a reader for Markdown knowledge repositories. [librarian-os.json](librarian-os.json) names the project and lists the entry points (the 18 knowledge area directories and `case-studies`). Librarian OS renders the notes in the browser with themes, search, a graph of the relations between notes and practice questions.

```bash
# in the librarian-os directory
npm install
npm run dev -- --repo /absolute/path/to/this/repository
```

The relations come from the sidecar files described in [GUIDELINE.md](GUIDELINE.md#35-sidecar-metadata): every `note.md` has a `note.md.json` next to it. The tools that keep them valid run from Librarian OS: `npm run check`, `npm run scaffold` and `npm run toc`, each with this repository's path as the argument. [INSTRUCTIONS.md](INSTRUCTIONS.md) describes the Librarian OS format.

## Repository layout

```text
ToC.md                      # full tree of every file
GUIDELINE.md                # rules for structure, note format and style
INSTRUCTIONS.md             # the Librarian OS repository format
librarian-os.json           # configuration for Librarian OS (project name, entry points, rules)
_assets/<knowledge-area>/   # images, diagram sources and other files used by notes
<knowledge-area>/
    README.md               # topic sections of the knowledge area
    <topic-section>/
        README.md           # notes in reading order and planned topics
        <topic>.md          # a single note
        <topic>.md.json     # its sidecar: node header, relations and sources
case-studies/               # real systems, linked to the concept notes
```

The full rules for structure and naming are in [GUIDELINE.md](GUIDELINE.md#3-repository-structure-and-naming).

## Sources and migration

The local directory `_sources/` holds the original exports (HTML) that the first notes came from. It is excluded from version control. Their content was translated into English where needed and moved into the knowledge area tree. Migrated notes keep their original content, start with the status `draft`, and contain `TODO:` lines for the parts of the note skeleton they do not have yet. Their content has not been verified against the sources listed in each note. Figures in migrated notes are third-party graphics whose authors were not recorded. They are kept for personal study and are to be redrawn as Mermaid diagrams or SVG files when a note is reviewed.

## Contributing and working with AI agents

All notes follow [GUIDELINE.md](GUIDELINE.md). It applies to people and to AI agents alike. Agent-specific entry points are [AGENTS.md](AGENTS.md) and [CLAUDE.md](CLAUDE.md). Both point to the GUIDELINE and do not repeat its rules.

## Status

The full SWEBOK V4.0 structure is in place. Sections marked `(planned)` in [ToC.md](ToC.md) have a `README.md` with planned topics and no notes yet. Every note is a `draft`: open gaps are marked with `TODO:` lines and the content still has to be checked against its sources.
