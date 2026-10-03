# DevOps in the Trenches

## Book Guide

DevOps in the Trenches is a production-focused field guide for engineers and technical leaders responsible for real systems.

The book examines what happens after architecture diagrams, transformation plans, and deployment demonstrations meet production conditions. It connects delivery, ownership, infrastructure, platform engineering, security, reliability, recovery, cost, incident response, and leadership as parts of one operating system.

This is not a tool catalogue or a beginner's command reference. It is about the judgment required to change and operate complex systems under pressure.

## Start Here

Read these files in order:

1. [Introduction](introduction.md)  
   Understand the book's production-first viewpoint, intended audience, boundaries, and central ideas.

2. [How to Use This Book](how-to-use-this-book.md)  
   Choose a complete, problem-based, role-based, or team-study reading path.

3. [Master Table of Contents](table-of-contents.md)  
   Explore the complete 12-part, 63-chapter curriculum and its 315 focused sessions.

4. [Publication Information](publication-information.md)  
   Review the edition status, copyright notice, technical disclaimers, correction process, and citation guidance.

## The Book's Operating Journey

The curriculum follows the life of a production system rather than the menu of a software vendor.

| Part | Focus | Central question |
| --- | --- | --- |
| I | Seeing Production Clearly | What system are we actually operating? |
| II | Ownership, Teams, and Decision Rights | Who owns the outcome and who can act? |
| III | Designing for Operability | Can this service be understood, controlled, degraded, and recovered? |
| IV | Moving Change Without Losing Control | How does change reach users safely? |
| V | Trusted Automation and Software Supply Chains | What establishes trust in automated change? |
| VI | Platforms, Cloud Foundations, and Compute | Which shared capabilities reduce cognitive load without hiding risk? |
| VII | Kubernetes, Networks, and Distributed Integration | Where do infrastructure abstractions break? |
| VIII | Data, Storage, and Recovery | What survives failure, and how can recovery be proved? |
| IX | Security, Identity, and Compliance in Delivery | How can controls work inside real delivery systems? |
| X | Reliability Engineering Before the Incident | What engineering reduces the probability and consequence of failure? |
| XI | Operating Under Pressure | How do teams contain damage and restore service? |
| XII | Leading the Whole System | How do cost, suppliers, executives, AI, and sustainability shape engineering decisions? |

## Who Should Read It

The book is written for:

- DevOps and production engineers.
- Site reliability engineers.
- Platform engineers.
- Cloud and infrastructure engineers.
- Security and compliance engineers.
- Software engineers who own services in production.
- Architects responsible for operability and long-term change.
- Engineering managers and technical program leaders.
- Directors, heads of engineering, CTOs, and other technology decision-makers.

Readers do not need expert-level knowledge in every subject. The book is designed to help them understand boundaries, identify missing evidence, ask useful questions, work across specialties, and make defensible decisions.

## What Each Chapter Contains

Every chapter follows a complete operating structure rather than reading as a long, unbroken essay.

The standard chapter structure includes:

1. Chapter purpose and reader outcome.
2. Opening production scenario.
3. Five focused sessions.
4. Decision points and trade-offs.
5. Failure modes and warning signs.
6. War story or field case.
7. Lessons from the trenches.
8. Operational checklist.
9. Connections to related chapters.
10. Curated further reading.

Some chapters also include worksheets, review templates, decision tables, or supporting resources where the subject requires them.

## What Makes This Book Different

DevOps in the Trenches treats production engineering as a connected discipline.

It does not isolate:

- Delivery from operability.
- Platforms from their internal customers.
- Security from engineering flow.
- Reliability from ownership and investment.
- Backups from restore evidence.
- Incidents from organizational design.
- Cloud cost from architecture.
- Executive reporting from technical truth.
- AI assistance from human accountability.

The book repeatedly returns to six questions:

1. Who owns the outcome?
2. What evidence supports the decision?
3. What can fail partially or unexpectedly?
4. What limits the blast radius?
5. How will the system recover?
6. What must change after learning occurs?

These questions remain useful even as tools and vendors change.

## Public Reader Edition

This directory is the reading center for the book's public companion. It provides the book's scope, complete curriculum, reading paths, application methods, publication information, and links to supporting material.

The repository complements the complete book. It does not reproduce every chapter. Material changes and confirmed corrections are recorded in the repository [CHANGELOG](../CHANGELOG.md) and [errata](../errata/).

## Companion Areas

The repository separates the book from its public supporting material.

### [Samples](../samples/)

Selected chapters and excerpts for public reading.

### [Checklists](../checklists/)

Operational review materials grouped by delivery, platform, security, reliability, recovery, and leadership.

### [Resources](../resources/)

Further reading, frameworks, templates, and glossary material that support the book without interrupting its narrative.

### [Errata](../errata/)

Confirmed corrections and instructions for reporting technical or editorial issues.

### [Media](../media/)

Approved cover files, author material, and press resources.

## How to Use the Public Material

You may use the public material to:

- Understand the book's scope.
- Follow its recommended reading paths.
- Review public samples.
- Apply published checklists to systems you are authorized to assess.
- Report suspected errors or broken references.
- Reference the project in professional discussion with appropriate attribution.

Access to the repository does not automatically grant permission to republish, sell, translate, redistribute, or create substantial derivative versions of the book. Review [COPYRIGHT.md](../COPYRIGHT.md) and [Publication Information](publication-information.md) before reusing material.

## Responsible Application

The book discusses production changes, security controls, incident response, resilience testing, credential management, recovery, and other consequential engineering work.

Do not apply a practice merely because it appears in the book. Confirm that it suits your environment and that you have authority to act. Review dependencies, safeguards, observation, recovery, and stop conditions before changing a live system.

Never submit credentials, customer data, restricted architecture, confidential incident records, private keys, or sensitive vulnerability details through public issues or pull requests.

## Corrections and Feedback

Readers can report:

- Technical inaccuracies.
- Unclear or misleading explanations.
- Broken links.
- Accessibility problems.
- Edition-specific errors.
- Cases where a checklist item lacks enough context to apply safely.

Use the repository's issue templates and include the affected file, section, version, and supporting evidence. Review the [errata guide](../errata/README.md) before submitting a correction.

General disagreement with a design choice is not automatically an error. Useful reports distinguish factual inaccuracies from contextual trade-offs and support claims with authoritative evidence where possible.

## Citation

Reference this public edition as:

> Felix, Ann Ogechi. *DevOps in the Trenches: The Field Guide to Building, Changing, Securing, Operating, and Leading Production Systems Under Pressure.* Public reader edition, 2026.

For repository material, include the repository URL and the relevant release tag or commit identifier.

## Author

Ann Ogechi Felix writes for engineers and leaders responsible for production systems. Her work focuses on DevOps, site reliability engineering, platform engineering, cloud infrastructure, operational security, incident learning, and the decisions that connect these disciplines.

## Continue Reading

Begin with the [Introduction](introduction.md), then use [How to Use This Book](how-to-use-this-book.md) to choose your path through the complete [Table of Contents](table-of-contents.md).
