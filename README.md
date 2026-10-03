# DevOps in the Trenches

## Operating Real Systems Under Pressure

DevOps in the Trenches is a production-focused book for engineers and technical leaders responsible for building, changing, securing, operating, recovering, and governing real systems.

The book begins where simplified DevOps explanations usually end. It examines what happens when architecture diagrams meet traffic, automation meets state, security controls meet delivery pressure, and ownership meets production consequence.

This repository is the public companion to the book. It gives readers a clear route into the book, selected reading material, operational checklists, supporting resources, and verified corrections.

## The Book

**Title:** DevOps in the Trenches  
**Subtitle:** The Field Guide to Building, Changing, Securing, Operating, and Leading Production Systems Under Pressure  
**Author:** Ann Ogechi Felix  
**Edition:** Public reader edition, 2026

DevOps in the Trenches is not a command reference, certification guide, or catalogue of products. It develops the judgment required to operate systems whose technical, organizational, security, financial, and human conditions cannot be separated.

## Start Reading

1. [Book Introduction](book/introduction.md)
2. [How to Use This Book](book/how-to-use-this-book.md)
3. [Master Table of Contents](book/table-of-contents.md)
4. [Publication Information](book/publication-information.md)
5. [Book Guide](book/README.md)

## Curriculum at a Glance

The book contains 63 chapters across 12 parts.

| Part | Subject |
| --- | --- |
| I | Seeing Production Clearly |
| II | Ownership, Teams, and Decision Rights |
| III | Designing for Operability |
| IV | Moving Change Without Losing Control |
| V | Trusted Automation and Software Supply Chains |
| VI | Platforms, Cloud Foundations, and Compute |
| VII | Kubernetes, Networks, and Distributed Integration |
| VIII | Data, Storage, and Recovery |
| IX | Security, Identity, and Compliance in Delivery |
| X | Reliability Engineering Before the Incident |
| XI | Operating Under Pressure |
| XII | Leading the Whole System |

Read the complete [table of contents](book/table-of-contents.md) for all chapters and sessions.

## Who This Is For

The book is intended for:

- DevOps and production engineers.
- Site reliability engineers.
- Platform engineers.
- Cloud, systems, and infrastructure engineers.
- Security and compliance engineers.
- Software engineers who own production services.
- Architects responsible for operability and change.
- Engineering managers and technical program leaders.
- Directors, heads of engineering, CTOs, and technology decision-makers.

It assumes that the reader wants more than tool familiarity. The material focuses on ownership, evidence, decision-making, trade-offs, failure behavior, blast-radius control, recovery, and learning.

## Repository Map

```text
devops-in-trenches/
├── README.md
├── COPYRIGHT.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── CHANGELOG.md
├── book/
├── samples/
├── checklists/
├── resources/
├── errata/
├── media/
└── .github/
```

### [book/](book/)

The book introduction, reading guide, curriculum, publication information, and reader navigation.

### [samples/](samples/)

Approved sample chapters and excerpts released for public reading.

### [checklists/](checklists/)

Operational review material covering delivery, platforms, security, reliability, recovery, and leadership.

### [resources/](resources/)

Further reading, frameworks, templates, and glossary material that support the book.

### [errata/](errata/)

Confirmed corrections and instructions for reporting errors.

### [media/](media/)

Approved cover, author, and press material.

### [.github/](.github/)

Issue and pull-request templates for technical corrections, broken links, and reader feedback.

## What You Will Find Here

The public repository organizes reader material into:

- The master table of contents.
- The introduction and reading guide.
- Selected sample chapters.
- Approved excerpts.
- Operational checklists.
- Reader worksheets and templates.
- A glossary and further-reading guides.
- Errata and version history.
- Cover and press material.

This repository is a reader companion, not a replacement for the complete book. Public access to selected material does not transfer ownership or create an open-source license for the book.

## Chapter Standard

Each chapter follows a complete operating structure containing:

1. A clear purpose and reader outcome.
2. An opening production scenario.
3. Five focused sessions.
4. Decisions, trade-offs, and failure modes.
5. A war story or field case.
6. Lessons from the trenches.
7. An operational checklist.
8. Connections to related chapters.
9. Curated further reading.

The chapter structure keeps the book practical without turning it into a product tutorial.

## Corrections and Reader Feedback

Accurate technical feedback is welcome.

Use the available issue templates to report:

- A technical correction.
- A broken link or unavailable source.
- Unclear wording.
- An accessibility problem.
- A contradiction between public files.
- A version-specific error.

Reports should identify the affected file and section, describe the problem precisely, and provide authoritative evidence where appropriate.

Do not submit credentials, customer information, confidential incidents, private architecture, restricted documents, exploit details that require coordinated disclosure, or other sensitive information.

Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening an issue or pull request.

## Copyright and Use

Copyright © 2026 Ann Ogechi Felix. All rights reserved.

This is a publicly accessible proprietary book repository. The book is not open source and is not released under an open-content license.

You may read, link to, and reference the public material. Other uses, including substantial copying, redistribution, translation, adaptation, commercial training use, resale, or republication, may require written permission.

Read [COPYRIGHT.md](COPYRIGHT.md) and [Publication Information](book/publication-information.md) before reusing material.

## Responsible Use

The repository discusses production systems, security, credentials, incident response, resilience testing, failover, recovery, and other consequential work.

Apply material only in systems you own or are authorized to use. Test changes appropriately. Protect data and credentials. Review failure modes, blast radius, recovery, observation, and stop conditions before changing a live environment.

The repository provides educational material, not legal, regulatory, audit, financial, or other licensed professional advice.

## Citation

Use the following citation for this public edition:

> Felix, Ann Ogechi. *DevOps in the Trenches: The Field Guide to Building, Changing, Securing, Operating, and Leading Production Systems Under Pressure.* Public reader edition, 2026.

When citing repository material, include the relevant release tag or commit identifier.

## Author

Ann Ogechi Felix writes about DevOps, site reliability engineering, platform engineering, cloud infrastructure, operational security, incident learning, and the decisions required to run production systems responsibly.

## Continue

Begin with [The Work Begins Where the Diagram Ends](book/introduction.md).
