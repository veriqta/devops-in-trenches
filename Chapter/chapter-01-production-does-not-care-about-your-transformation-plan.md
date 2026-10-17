# Chapter 1: Production Does Not Care About Your Transformation Plan

*Part I: Seeing Production Clearly*

[All free chapters](README.md) | [Next sample](chapter-19-progressive-delivery-rollback-and-roll-forward.md)

> This is a free sample chapter from *DevOps in the Trenches* by Ann Felix. It is provided for personal reading through the official book repository. Copyright © 2026 Ann Felix. All rights reserved.

---

## Opening Scenario

The quarterly transformation review begins with a familiar slide. Thirty-four delivery pipelines have been standardized. Most application teams have moved their repositories. The cloud migration is ahead of schedule. Hundreds of employees have completed training. A new platform portal is live. Every program milestone is green.

Then a regional pricing service needs a routine configuration change.

The request enters a queue owned by release management. Security must approve a permission change, but the approver listed in the workflow left the company two months earlier. The application team can build the change but cannot reproduce the production configuration. The infrastructure team owns the cluster, the platform team owns the deployment templates, and a vendor owns the database extension. Nobody owns the complete release decision.

Three days pass before the change reaches a staging environment. The test data does not represent the production condition that caused the request. The deployment pipeline is automated, but the rollback requires a manual database step documented in a private team page. Operations asks for a release plan. The application team points to the pipeline. The platform team points to the service owner. The service owner assumes operations will coordinate the recovery if anything fails.

The change is approved for a low-traffic period. It deploys successfully according to the pipeline. Twenty minutes later, customer requests begin timing out in one region. Infrastructure health remains green. Application error rates rise slowly rather than crossing the alert threshold. Customer support sees the problem first.

The incident channel fills with people, but authority remains unclear. One team wants to roll back. Another warns that rollback may corrupt recently written data. The vendor cannot join for forty minutes. An engineer who helped build the original service is contacted during personal time because the documented recovery path has never been tested.

Service returns after two hours. The configuration change was small. The failure was not.

At the review the next morning, every transformation milestone is still green. The pipeline completed its task. The cloud platform remained available. The change ticket contained the required approvals. Training completion did not decline. The program dashboard had no field for the missing service boundary, the untested rollback, the obsolete approver, the weak customer signal, or the dependence on one engineer’s memory.

The organization had changed many visible things. It had not changed the conditions under which production work became safe.

This is where transformation language becomes dangerous. It allows an organization to count adoption while leaving responsibility fragmented. It allows automation to be mistaken for control. It allows teams to report movement while customers continue to experience the same delays, failures, and uncertain recovery.

Production does not evaluate the presentation. It responds to architecture, dependencies, permissions, queues, capacity, feedback, and decisions. When those elements disagree, the declared transformation has no special authority. The system behaves according to what was actually designed and maintained.

The first task is therefore not to defend or reject DevOps. It is to determine what changed in the operating system, what evidence demonstrates that change, and what production still exposes as unresolved.

## Session 1: The Myth of the DevOps Transformation

The transformation label suggests a controlled passage from an old state to a new one. It gives executives a program to fund, leaders a roadmap to report, and teams a destination to reach. The problem is not that organizations want substantial change. The problem is that the label often turns a continuing operating responsibility into a temporary initiative.

A production system never reaches a final state. Applications change, dependencies change, threats change, customer expectations change, and the people carrying operational knowledge change. A delivery practice that worked for ten teams may become a constraint at fifty. A control that reduced risk in a manual release process may create risk when placed unchanged inside an automated one. A platform that initially removes friction can become another legacy dependency if its ownership and lifecycle are neglected.

For that reason, a credible transformation cannot mean that the organization has finished adopting DevOps. It must mean that specific operating capabilities have changed and that the organization can continue improving them. The evidence lives in work and outcomes, not in the name of the program.

### Visible change and operating change

Visible change is easy to display. Teams move repositories, adopt infrastructure as code, form a platform group, migrate workloads, purchase observability products, or change job titles. These actions may be necessary. They are still inputs.

Operating change appears in the decisions surrounding production. A team can obtain an environment without waiting through an unmanaged queue. A change can move from commit to production through a path whose controls are known and testable. The people operating a service can see whether customers are receiving the intended outcome. A failed release has a bounded recovery path. Ownership remains clear when a dependency degrades, not only when everything is healthy.

The difference matters because an organization can complete the visible work while preserving the old system underneath it. A cloud migration may reproduce the same ticket queues and fixed capacity assumptions. A continuous integration product may execute builds while integration remains infrequent and painful. A platform may publish templates while application teams still require private intervention for every exception. The surface changes. The constraints survive.

### Transformation as identity

The label becomes more difficult to challenge when it turns into an organizational identity. Leaders have committed funding and credibility. Teams have reorganized. Vendors have been selected. Acknowledging that production capability has not improved can sound like rejecting the entire effort.

This pressure encourages substitution. Adoption becomes a proxy for usefulness. Completion becomes a proxy for capability. A program milestone becomes a proxy for a customer outcome. Once the proxy enters executive reporting, teams learn to protect it. They may count pipeline creation instead of examining release delay, count platform registrations instead of investigating bypasses, or count closed actions instead of verifying that a failure mode has been removed.

The correction is not cynicism. It is precision. Ask what operating condition the initiative was supposed to change. Define the system boundary. Identify the people who experience the result. Establish a baseline that is good enough to guide decisions. Then examine whether the capability improved without transferring risk elsewhere.

### Capability is contextual

DORA’s research treats software delivery performance as an outcome supported by technical, process, and cultural capabilities. Its guidance also warns against treating delivery measures as universal targets or comparing services with materially different contexts. That distinction is important. Transformation cannot be proven by copying another organization’s practices or performance thresholds.

A regulated payment system, an internal analytics tool, a mainframe settlement process, and a consumer mobile service face different consequences and constraints. Each can still improve flow, feedback, stability, and recovery. The standard is not identical implementation. The standard is whether the operating capability is appropriate, observable, owned, and improving within its context.

The myth is not that meaningful transformation is impossible. The myth is that it can be declared complete because a program delivered its outputs. Production capability must be demonstrated repeatedly. The organization has changed only when routine work and failure behavior show that its decisions have changed with it.

## Session 2: Why Tools Cannot Repair a Broken Operating Model

A tool executes the authority and assumptions given to it. It can make a decision repeatable, accelerate a workflow, preserve evidence, and reduce manual variation. It cannot decide who should own a service, resolve incentives that reward conflicting outcomes, or determine how much risk the organization should accept.

This limitation is easy to miss because tool adoption produces immediate evidence of movement. A pipeline runs. A portal creates an environment. A policy engine blocks a deployment. A dashboard shows a new metric. The interface is visible, while the operating model around it remains partly hidden.

### Automation inherits the surrounding system

Consider a deployment pipeline introduced into an organization where development is measured on feature completion, operations is measured on change avoidance, and security is measured on the number of issues blocked. The pipeline may remove manual steps, but it does not reconcile those incentives. Development still wants movement, operations still wants stability through restriction, and security still gains safety through delay. The conflict moves into pipeline rules, exception queues, and approval logic.

The result may be faster execution of a slow decision path. It may also be a brittle path that works only for standard changes. When a change falls outside the template, teams return to private messages and manual intervention. The automation has not removed the old operating model. It has created a fast lane through one portion of it.

The same pattern appears in cloud adoption. Self-service infrastructure can reduce provisioning delay, but only if identity, network, security, cost, and lifecycle decisions have usable defaults and clear owners. Otherwise, a request moves quickly until it meets an unresolved boundary. Teams then accumulate standing privileges, duplicate infrastructure, or build unofficial paths around the platform.

### Tools amplify both strengths and weaknesses

Automation increases consistency when the underlying decision is sound. It also increases the speed and reach of a mistake. A manual misconfiguration may affect one environment. A shared template can reproduce the same error across hundreds. A centralized policy can prevent unsafe deployments, or it can stop urgent recovery work if exceptions were never designed. A common platform can reduce cognitive load, or it can create a dependency whose failure blocks every delivery team.

The practical question is not whether automation is good. It is what decision has been encoded, who owns that decision, which evidence the tool evaluates, and what happens when the assumptions are false.

### Four conditions deserve examination before automation is treated as improvement.

First, the responsibility must be explicit. Someone must own the policy or workflow beyond its implementation. Ownership includes reviewing its continued validity, responding to failure, and deciding when an exception is justified.

Second, the normal path must be understood. Automating a process that nobody can explain often conceals rather than removes waste. Mapping the actual flow, including waits and rework, reveals whether the tool addresses the constraint or merely one visible step.

Third, degraded behavior must be designed. Identity services fail. Registries become unavailable, agents lose connectivity, and policy data becomes stale. The organization must decide whether work stops, continues with reduced assurance, or moves through a controlled emergency path.

Fourth, feedback must reach the owner. A platform team needs evidence about adoption, abandonment, exceptions, support demand, and downstream incidents. A security team needs evidence about false positives and bypass behavior. Without feedback, automation can remain technically healthy while becoming operationally harmful.

Tool selection still matters. Products differ in reliability, integration, security, maintainability, cost, and usability. The error is expecting selection to substitute for operating design. A suitable tool inside a broken decision system will eventually expose the break, often after the organization has made the tool central to production.

The correct sequence begins with the capability and its owner. Define the decision, evidence, constraints, failure behavior, and review cycle. Then select or build the mechanism that supports them. The tool becomes part of the operating model rather than a replacement for one.

## Session 3: The Difference Between Activity and Capability

Transformation programs produce activity because activity is controllable. Budgets can be allocated, training scheduled, repositories moved, pipelines created, controls configured, and migration waves completed. These outputs show that work occurred. They do not establish that the organization can perform the production task safely and repeatedly.

A capability is a dependable ability under stated conditions. It includes people, knowledge, authority, process, technology, evidence, and recovery. Deployment automation is an asset. The ability to release an important service on demand, observe customer effect, contain failure, and recover within an agreed boundary is a capability.

This distinction prevents a common reporting error. program teams report the completion of enabling work as if it were the outcome the enabling work was meant to produce. The substitution is understandable. Activity data arrives early and is easy to aggregate. Capability evidence appears across different systems and often requires uncomfortable interpretation.

### Five tests of capability

The first test is repeatability. Can the organization perform the task without relying on a particular individual’s memory or private access? A process that succeeds only when the most experienced engineer is present remains fragile, even if that engineer succeeds every time.

The second test is operating range. Under which conditions does the capability work? A deployment path may handle normal application changes but fail for database migrations, urgent security fixes, regional recovery, or a degraded identity provider. Declaring the capability without its boundary hides the situations that matter most.

The third test is evidence. Can the responsible team show that the intended outcome occurred? A successful pipeline run proves execution, not customer success. A completed backup proves that data was written somewhere, not that the service can be restored. Evidence must match the claim.

The fourth test is ownership. Who maintains the capability, decides its standards, responds when it fails, and funds its improvement? Shared responsibility can be appropriate, but shared responsibility without decision rights usually becomes an escalation problem.

The fifth test is adaptation. Can feedback change the process, architecture, or policy? A capability that produces data but cannot act on it may become a reporting ritual. Learning requires authority and capacity, not only a retrospective meeting.

### Measuring without creating theatre

DORA currently describes software-delivery performance through measures of throughput and instability. Its guidance is valuable here because it focuses on outcomes of the delivery process and warns against turning measures into goals, comparing unlike services, or investing in perfect collection before beginning improvement.

The answers do not need to become a score. Their purpose is to expose the constraint and support a decision. If the team improves deployment frequency by splitting changes while change failures and recovery remain stable or improve, that is evidence of increased capability. If frequency increases because controls moved outside the recorded path, the same number could conceal risk.

Local success can also damage the wider system. A development team may reduce its cycle time by handing incomplete operational work to another group. A central platform may reduce infrastructure variation while increasing the queue for exceptions. A security team may close findings more quickly by rejecting risk rather than helping teams remediate it. Each group appears efficient. The end-to-end system becomes slower or less safe.

Capability must therefore be assessed at the boundary where value and consequence appear. Start with a service or value stream, not an organizational average. Follow work from request through production and recovery. Examine waits, rework, failure, customer effect, and ownership across team boundaries.

Activity deserves recognition when it builds the required capability. It should not be asked to prove more than it can. A migrated repository is a completed task. A reliable, traceable, recoverable change path is the result that matters.

This distinction also changes executive reporting. Leaders do not need every operational detail, but they do need to know whether the promised capability exists, where it fails, and which constraint requires a decision. A concise report can show the intended outcome, current evidence, material exceptions, risk transferred to other teams, and the next intervention. That report is harder to produce than a count of completed migrations because it requires interpretation. It is also more useful because it reveals whether investment changed production behavior.

## Session 4: What Production Exposes About the Organization

Production is an integration test for the organization. It combines architecture, staffing, access, policy, vendor relationships, incentives, documentation, and time pressure. When a service fails or a change stalls, the visible technical symptom often reveals decisions made far from the component that broke.

This does not mean every incident is primarily organizational. Components have defects. Networks partition. Capacity is exhausted. Operators make mistakes. The important point is that the effect of those events depends on the surrounding system. A defect becomes a long outage when detection is weak, ownership is disputed, rollback is unsafe, or authority arrives late.

### Queues reveal decision design

Long waits are often explained as insufficient automation or staffing. Sometimes that is correct. Sometimes the queue exists because the organization has not decided who can accept a risk. A change waits for several approvals because no single approver owns the complete consequence. An environment request waits because network, identity, security, and cost controls were never converted into supported defaults.

Measure the waiting time, but investigate the decision. Adding capacity to an unresolved approval system can process uncertainty faster without removing it.

### Incidents reveal ownership

Service catalogues and responsibility matrices describe ownership under normal conditions. Incidents test it. Who can declare severity, stop a rollout, communicate customer impact, involve a vendor, authorize degraded operation, or accept data-recovery consequences? If those decisions depend on hierarchy, personal relationships, or whoever responds first, the documented owner does not possess operational authority.

Repeated escalation to a small group also reveals where knowledge and trust have concentrated. The immediate response may require those people. The learning response should reduce the dependency through clearer service boundaries, access design, runbooks, rehearsal, and shared diagnosis.

### Degradation reveals what the organization values

Systems rarely move directly from healthy to unavailable. They become slow, inconsistent, partially unreachable, stale, expensive, or difficult to recover. The response to degradation shows whether the organization has defined user-relevant behavior or only infrastructure health.

A dashboard may remain green because hosts are running while customers cannot complete a transaction. A team may meet an availability target while a critical minority of requests fail. The lesson is not that dashboards or objectives are useless. It is that evidence must represent the outcome the organization claims to protect.

### Recovery reveals preparation

Recovery work exposes assumptions that normal operation can conceal. Documentation may describe commands without identifying decision points. Backups may exist without application configuration, keys, dependency order, or validation data. Access may be available in the primary environment but unavailable when the identity path is impaired.

An untested recovery plan is a statement of intent. Demonstrated recovery requires rehearsal, observable success criteria, known dependencies, and an owner who can accept the recovered state. Detailed recovery engineering belongs later in this book, but the transformation lesson belongs here: readiness must be shown under representative conditions.

### Production evidence without blame

Using production as evidence can become punitive if leaders treat every signal as a search for fault. That response teaches teams to protect metrics, narrow incident records, and avoid exposing weak boundaries. The organization then loses the information it needs to improve.

A better review asks how the system made the action reasonable. What information was available? Which incentives applied? What constraint shaped the choice? Which control failed to prevent, detect, or contain the event? Which recovery dependency was missing? The purpose is not to erase individual accountability. It is to distinguish a careless act from a predictable outcome produced by the operating environment.

Transformation claims should become more specific after contact with production. The organization may discover that automation improved the normal path but not emergency change, that cloud adoption improved provisioning but not service ownership, or that observability improved detection but not decision authority. These findings do not automatically invalidate the investment. They identify the next constraint.

Production exposes the organization because production contains the organization. The responsible response is to follow the evidence across technical and managerial boundaries until the operating decision becomes visible.

## Session 5: The First Questions a Serious Transformation Must Answer

A serious transformation begins with a production problem that matters, not a catalog of practices to adopt. It defines what must improve, for whom, under which constraints, and how the organization will know. These questions create a basis for action without pretending that one model fits every service.

### What outcome must change?

Name the customer, user, operator, regulator, or business process affected. “Improve DevOps” is not an outcome. Reducing the time required to deliver a pricing change while preserving transaction correctness is an outcome. Restoring a critical service without relying on one person is an outcome. Producing traceable deployment evidence without a manual audit chase is an outcome.

The outcome should connect technical behavior to a real consequence. It should also identify what must not be sacrificed. Faster change that increases unrecoverable data risk is not an uncomplicated improvement.

### Where is the system boundary?

Choose a service or value stream that can be examined end to end. Include the queues, control points, dependencies, and teams required to reach production and recover from failure. If the boundary ends at the application team, transferred work will disappear from the analysis.

The boundary may need to include a vendor, legacy platform, change authority, security control, or finance decision. Chapter 2 develops this mapping in depth. At this stage, the purpose is to prevent a local initiative from claiming a system outcome.

### Who owns the result and the decisions inside it?

Assign ownership at the level of consequence. Someone must be accountable for the service outcome. Different groups may own platform reliability, security policy, data integrity, or release control, but their decision rights and escalation paths must meet at the service boundary.

Ask who can stop a change, accept an exception, approve degraded operation, initiate recovery, and fund correction of a known risk. If the answer changes depending on who is available, the operating model is not ready for automation at scale.

### What evidence will guide action?

Select a small set of signals that reflect flow, stability, customer effect, and recovery. Use them to locate constraints and evaluate changes over time. Record definitions, scope, time windows, and limitations. Do not aggregate unlike services to create a reassuring enterprise number.

Combine quantitative and qualitative evidence. Queue time may show where work waits. Interviews and value-stream observation may explain why. Incident records may reveal recovery delay. Support contacts may show a customer problem that infrastructure metrics miss.

### What failure behavior is acceptable?

Every new path introduces failure modes. Decide what should happen when the pipeline, platform, identity provider, policy service, registry, or approval system is unavailable. Identify which operations may continue, which must stop, and who can authorize an exception. Test that decision before an urgent release requires it.

The goal is not uninterrupted operation at any cost. Some work should stop when assurance is unavailable. The important point is to make the condition deliberate rather than discover it during an incident.

### What constraint should be addressed first?

Transformation programs often launch several workstreams because every weakness appears important. That spreads attention and makes attribution difficult. Begin with the most consequential constraint that the organization can influence. Form a hypothesis, change the system, observe the effect, and retain or revise the intervention.

A constrained approach may look less impressive than a large adoption dashboard. It produces better information. It also limits the risk of automating a process before the organization understands it.

### How will learning change funding and priority?

Continuous improvement fails when evidence has no route into planning. Teams may identify unsafe dependencies and recurring toil while investment remains tied to feature commitments. Leaders must reserve capacity and create a decision cadence that can act on operational evidence.

The review should ask whether the capability improved, what risk moved, what new constraint appeared, and whether the original outcome still matters. It should be willing to stop an initiative that produces adoption without value.

These questions do not produce a finished transformation plan. They produce something more useful: a testable operating change with an owner, a boundary, evidence, and known failure conditions. That is enough to begin honestly.

## War Story

The Platform That Passed Every Milestone

The following story is a composite based on recurring enterprise patterns. Names, numbers, and identifying details are intentionally omitted.

A large organization approved an internal platform program after several years of slow releases, inconsistent environments, and difficult audit preparation. The business case was persuasive. Standard templates would reduce variation. Self-service would shorten provisioning. Central policy would improve security. Shared pipelines would create evidence automatically.

The platform team delivered on schedule. It built a service catalog, environment templates, continuous integration workflows, deployment automation, policy checks, and centralized logging. The first dashboard showed strong progress. Applications were registered. Repositories were connected. Engineers attended training. The program reported adoption by counting each completed migration.

Production behavior changed less than the dashboard suggested.

Most teams could create a development environment quickly, but production network rules still required a ticket reviewed by a small infrastructure group. Database changes remained outside the standard pipeline because ownership was split across application, database, and release teams. Security policy blocked several legacy deployment patterns, but the exception process had no response target and no permanent owner.

Application teams learned where the platform ended. Some kept the standard pipeline for visible stages and performed sensitive steps manually. Others copied templates into their own repositories so they could modify them without waiting. A few services registered in the catalog but continued releasing through the previous system.

Those choices were not visible as platform failures. The portal remained available. Pipeline jobs succeeded. Policy checks recorded decisions. Support demand was classified as onboarding assistance rather than evidence about product fit.

### The failure chain

The immediate incident began with a routine certificate update for a revenue-critical service. The platform template supported automated rotation, but the service depended on an older component that loaded certificates only at startup. The application team had documented the exception in its own repository. The platform team did not track which services had modified the standard.

The pipeline replaced the certificate and reported success. One group of instances continued serving existing connections. Newly started instances failed to establish a downstream connection. Traffic shifted gradually, producing intermittent customer errors rather than a clean outage.

The observability platform showed healthy infrastructure and successful deployment status. Customer support reported transaction failures. The application team began diagnosis, then discovered that its usual rollback would restore the expired certificate. The security team rejected that option. The platform team could revert the template but could not decide whether the service should operate temporarily with the previous credential. The incident commander had technical coordination authority but no clear risk owner for the exception.

Recovery took longer than the certificate repair. Teams had to reconstruct the service’s modified deployment path, obtain an emergency security decision, restart instances in the correct order, and confirm that transactions had not been duplicated. The platform was not unavailable. It had done exactly what its shared workflow specified. The surrounding ownership model had failed to carry a known service exception into production control and recovery.

The first review focused on compliance with the platform. Leaders proposed mandatory adoption and tighter restrictions on template modification. That response would have increased visible conformity while preserving the missing decisions.

A second review followed the work across team boundaries. It found that the platform program had been measured on migration completion, not on reduction of release delay or recovery risk. The platform team owned components but not the service outcomes created through them. Application teams could modify templates without registering divergence. Security owned policy but not exception response. Service owners had responsibility without authority over several recovery decisions.

### The correction

The organization stopped treating registration as adoption. It selected a small set of important services and mapped each delivery and recovery path. Platform teams recorded supported patterns and known divergence. Application teams retained responsibility for service behavior while platform owners accepted reliability obligations for shared paths. Security defined time-bounded exception authority and evidence requirements. Recovery exercises tested the interactions among those decisions.

Some platform features were simplified. Others gained stronger controls. A few services remained outside the standard path because forcing them into it would have increased risk. Their exceptions became visible, owned, and reviewed rather than hidden.

The program dashboard changed last. It began reporting support demand, standard-path completion, unresolved divergence, change outcomes, and recovery exercises for selected services. The numbers were less impressive than the original adoption count. They were more useful.

The platform investment was not wasted. Its technical foundation supported the correction. The failure was the assumption that delivering the foundation had already changed the operating system. Production supplied the missing evidence.

## Lessons from the Trenches

Transformation is a claim that requires production evidence. A program can deliver every planned artifact while the original constraint survives in approvals, ownership, recovery, or exception handling.

Tools encode decisions. Before automating a path, identify who owns the decision, which evidence it uses, how exceptions work, and what happens when a dependency is degraded.

Adoption is not the same as use, and use is not the same as outcome. Registration, training, migration, and pipeline execution are useful activity measures. They do not prove that customer impact, flow, stability, or recovery improved.

The normal path is only part of the capability. A production practice must define its operating range, including database change, urgent correction, dependency failure, degraded identity, and recovery.

Local efficiency can transfer risk. A team may shorten its work by creating a queue, exception, or operational burden elsewhere. Follow the work across the service boundary before declaring improvement.

Production signals should lead to investigation rather than punishment. If teams fear that evidence will be used against them, metrics become defensive and weak boundaries remain hidden.

Ownership requires authority. Naming a service owner is insufficient when another group controls rollback, access, exception approval, vendor escalation, or investment in known risk.

Begin with one consequential constraint. Define the outcome, boundary, evidence, owner, and failure behavior. Improve it, observe the result, and then address the next constraint.

The strongest transformation dashboard may contain fewer numbers. Each number should connect to a decision, a defined system boundary, and an outcome the organization is prepared to act upon.

Exceptions are operating data. Repeated requests for manual access, template changes, urgent approvals, or support intervention show where the supported path does not match production reality. Hiding exceptions protects the program narrative and weakens the system.

Recovery is where ownership becomes concrete. The person named as owner must be able to coordinate the technical, customer, security, data, and vendor decisions required to return the service safely.

Improvement needs capacity. A retrospective can identify the right corrective work, but learning remains incomplete when planning and funding cannot make room for it.

Context limits imitation. Practices from high-performing organizations can inform a decision, but their value depends on architecture, risk, regulation, staffing, and service purpose. Copy the reasoning before copying the shape.

Transformation should reduce dependence on exceptional effort. If success still relies on late escalation, private knowledge, or repeated rescue by the same people, the operating capability remains immature regardless of the technology in place.

## Operational Checklist

Enterprise DevOps Transformation Reality Check

Use this checklist as an investigation, not as a maturity score. Apply it to one service or value stream. Record evidence, owners, and unresolved decisions.

### Outcome and boundary

1. Identify the customer, user, operator, or business process expected to benefit.

2. State the production outcome the transformation is intended to change.

3. Record the conditions that must not be sacrificed while pursuing that outcome.

4. Map the path from requested change through production validation and recovery.

5. Include external vendors, shared platforms, control functions, and legacy dependencies inside the boundary where they affect the outcome.

### Ownership and authority

6. Assign an accountable owner for the service outcome.

7. Identify who can stop a release, approve an exception, authorize degraded operation, and initiate recovery.

8. Verify that documented owners possess the access, funding path, and decision authority their responsibility requires.

9. Record dependencies that rely on one individual’s knowledge, relationship, or privilege.

10. Define escalation paths for decisions that cross application, platform, security, operations, data, and vendor boundaries.

### Capability and evidence

11. Separate program activities from the operating capabilities they are meant to create.

12. Define evidence for flow, stability, customer effect, and recovery at the service level.

13. Record each measure’s definition, scope, time window, and known limitation.

14. Verify that a successful automated task demonstrates the claimed outcome rather than only tool execution.

15. Examine waiting time, rework, manual intervention, bypasses, and exception queues.

16. Compare current evidence with a useful baseline before declaring improvement.

### Failure and recovery

17. Identify how the delivery path behaves when identity, policy, registry, platform, network, or vendor services are degraded.

18. Define which operations stop, continue, or require explicit exception authority.

19. Test a representative rollback or recovery path, including data and dependency consequences.

20. Verify that recovery does not depend on undocumented knowledge or unavailable credentials.

21. Record how lessons from incidents, failed changes, and support demand alter the operating path.

### Governance and learning

22. Review whether team incentives reward conflicting outcomes or transfer work across boundaries.

23. Assign a decision cadence for reviewing evidence and choosing the next constraint.

24. Reserve capacity and funding for corrective work revealed by production evidence.

25. Stop, narrow, or redesign initiatives that create adoption without improving the intended capability.

## Further Reading

Nicole Forsgren, Jez Humble, and Gene Kim, Accelerate: The Science of Lean Software and DevOps: Building and Scaling High Performing Technology Organizations, IT Revolution Press, 2018. Read this for the research model connecting software-delivery capabilities, delivery performance, organizational outcomes, and culture. It also helps readers distinguish evidence from DevOps folklore.

DORA, Accelerate State of DevOps Report 2024, Google Cloud, 2024. Use the report to examine current findings on user focus, stable priorities, platform engineering, leadership, and the trade-offs associated with emerging technology. Read the methodology and limitations before converting findings into policy.

DORA, DORA’s Software Delivery Performance Metrics, updated 5 January 2026. This guide explains the current five-metric model, the division between throughput and instability, service-level context, and common measurement failures. Its warnings about targets, comparisons, competition, and collection effort are as important as the metric definitions.

Google Cloud Architecture Center, DevOps Capabilities. This catalog separates technical, process, and cultural capabilities. It is useful when a transformation plan has collapsed into a list of products or isolated practices.

Gene Kim, Jez Humble, Patrick Debois, John Willis, and Nicole Forsgren, The DevOps Handbook, Second Edition, IT Revolution Press, 2021. Read this for value-stream thinking, feedback, continual learning, and the operating practices that support DevOps beyond tool adoption.

Donella H. Meadows, Thinking in Systems: A Primer, edited by Diana Wright, Chelsea Green Publishing, 2008. Use this to understand feedback, delays, system boundaries, resilience, and why local interventions can produce unexpected behavior elsewhere.

Matthew Skelton and Manuel Pais, Team Topologies: Organizing Business and Technology Teams for Fast Flow, Second Edition, IT Revolution, 2025. Read this for the relationship among team boundaries, cognitive load, interaction modes, platforms, and flow. Chapter 1 uses only the general lesson that organizational design changes system behavior. Later chapters apply the model more directly.

Betsy Beyer, Chris Jones, Jennifer Petoff, and Niall Richard Murphy, editors, Site Reliability Engineering: How Google Runs Production Systems, O’Reilly Media, 2016. Read the principles and management sections for a production-centered treatment of risk, toil, automation, incidents, communication, and organizational engagement. Apply the ideas with attention to differences between Google’s environment and your own.

## The Next Trench

Once transformation claims are tested against production, the next problem is boundary. A service depends on more than its repository and runtime. It depends on identity, networks, data, shared platforms, vendors, approval paths, support processes, budgets, and people who hold operational knowledge.

If those relationships remain invisible, the organization will continue improving components while risk accumulates between them. Ownership will end where the org chart ends, even though failure crosses that boundary without permission.

Chapter 2 builds the enterprise production context map. It shows how to identify the real system that carries a change, serves a customer, and must recover under pressure. Without that map, the organization cannot tell whether an improvement changed the system or merely moved its constraint.

The next step is to make that system visible before another local improvement conceals it.

That map becomes the foundation for every later decision about ownership, delivery, security, reliability, recovery, and cost.

---

## About This Sample

This chapter is part of *DevOps in the Trenches*, a 63-chapter field guide to building, changing, securing, operating, and leading production systems under pressure.

This public sample may be read and linked from this repository. It may not be republished, sold, translated, scraped into another publication, or redistributed as a separate work without written permission from the copyright holder.

[Return to all free chapters](README.md) | [Read the next sample](chapter-19-progressive-delivery-rollback-and-roll-forward.md)
