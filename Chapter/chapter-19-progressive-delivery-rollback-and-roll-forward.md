# Chapter 19: Progressive Delivery, Rollback, and Roll-Forward

*Part IV: Moving Change Without Losing Control*

[All free chapters](README.md) | [Previous sample](chapter-01-production-does-not-care-about-your-transformation-plan.md) | [Next sample](chapter-54-incident-command-and-decision-making-under-pressure.md)

> This is a free sample chapter from *DevOps in the Trenches* by Ann Felix. It is provided for personal reading through the official book repository. Copyright © 2026 Ann Felix. All rights reserved.

---

## Opening Scenario

The rollout looked disciplined. Five percent of production traffic received the new version, every automated check remained green, and the deployment controller promoted the release worldwide.

The service calculated shipping promises for a global retailer. The canary instances ran in one region and received a random share of interactive customer requests. Their error rate, latency, processor use, and request volume matched the stable version. After twenty minutes, the controller increased exposure to every region.

The failure appeared forty minutes later. Large marketplace sellers submitted bulk updates through an asynchronous endpoint that the canary cohort had barely exercised. Their requests created a different data shape, used a separate queue, and called a regional inventory dependency with stricter rate limits. The new code increased concurrent lookups. That dependency began throttling, queues grew, and promised delivery dates stopped updating.

The canary had not failed. It had answered a narrower question than the organization thought it had asked. Random traffic in one region did not represent bulk sellers, delayed queue processing, or the dependency limit that governed the workload. The promotion rule treated absence of evidence as evidence of safety.

Operators disabled the new calculation path through a feature flag, but the flag affected only synchronous requests. The asynchronous workers had read the setting at startup and continued until they were restarted. Some regions received the flag change quickly, while others used cached configuration. The team had a control mechanism, but no verified model of how fast it could contain exposure.

The incident commander paused queue consumption, reduced concurrency, and routed high-volume accounts to the previous processing path. Engineers compared queued work with inventory-provider acknowledgements before replaying messages. Customer support contacted affected sellers whose promised dates required correction. Recovery took longer than the rollout because the team had to identify which customers, regions, and messages had actually experienced the new behavior.

The review did not conclude that canaries or feature flags were ineffective. It found that the organization had treated them as safety labels. The canary cohort did not represent the high-consequence path. The health model watched infrastructure symptoms but not queue age, dependency throttling, or delayed business completion. The abort path had never been tested across long-lived workers and cached configuration.

The next release used exposure units that matched the workload. Interactive traffic, bulk sellers, asynchronous workers, and regions progressed through separate but coordinated waves. Promotion required customer-journey completion, queue-age stability, dependency health, and data reconciliation. Missing evidence paused the rollout. The team also tested how quickly the flag reached every runtime and which components required restart.

The important correction was not a longer hold period. A longer observation of unrepresentative traffic would have produced the same confidence more slowly. The team changed the unit of exposure, the evidence, and the stop path together. That shift turned the canary from a deployment ritual into a controlled production decision.

Progressive delivery does not make production certain. It limits how much uncertainty the organization accepts at one time. That control begins with a precise answer to three questions: who is exposed, what evidence governs expansion, and how quickly can the exposure be stopped?

## Session 1: Feature Flags, Canaries, and Staged Exposure

Deployment places a change in an environment. Exposure determines which requests, users, tenants, workers, or regions experience it. Progressive delivery separates those events so production evidence can govern how far the change proceeds.

### Choose the control that matches the change

A feature flag controls a behavior inside compatible software. An instance canary routes a bounded share of workload to a new version. A regional wave limits infrastructure and dependency exposure by geography. A tenant or account cohort preserves stable customer assignment. A dark launch sends real work to a new path without using its result. These controls answer different questions and may be combined, but every additional layer increases state and cleanup burden.

### Separate release from experiment

A rollout asks whether a known change is healthy enough to expand. An experiment asks which behavior produces a better outcome. Mixing the two weakens both decisions. Reliability checks should protect customers before an experiment evaluates product effect. An experiment must also define consent, privacy, fairness, and analytical validity where those concerns apply. A green business metric cannot excuse a reliability or security regression.

### Design a representative canary

A canary needs enough relevant traffic to exercise the changed path. Random percentage alone may omit large tenants, rare data shapes, batch work, mobile versions, region-specific dependencies, or peak load. Select the exposure unit from the failure hypothesis. If the change affects a queue consumer, expose workers and observe completed work. If it affects a regional dependency, one global percentage may conceal the affected region.

The stable population must remain comparable. Different hardware, cache warmth, traffic mix, autoscaling state, or dependency route can produce a false difference or hide a real one. Record the assignment method and prevent users or transactions from switching variants when consistency matters.

### Size stages by consequence and evidence

A smaller cohort limits immediate impact and produces fewer observations. A larger cohort generates evidence faster and exposes more customers. Choose stage size and duration from traffic volume, failure latency, customer consequence, and recovery speed. Low-volume services may need longer holds, synthetic journeys, selected tenants, or a different control. Copying a percentage from another service provides no safety argument.

### Preserve compatibility and containment

Chapter 18 established that old and new states must coexist safely. Progressive delivery depends on that compatibility. A flag cannot safely turn behavior off if the new path has already written data the old path cannot interpret. A canary rollback cannot restore an external transaction. Define what exposure control can reverse, what requires containment, and what requires reconciliation.

### Treat flags as production systems

Version flag definitions, restrict write access, audit changes, validate defaults, and define behavior when the flag service is unavailable. Local caches reduce dependency risk but delay control changes. Remote evaluation provides central control but may enter a request path. Decide whether failure should preserve the last known value, choose a safe default, or reject work. Test propagation and failure behavior under realistic network conditions.

### Make each stage a decision

A stage needs entry conditions, exposure identity, observation period, success and failure evidence, an owner, and the next allowed actions. Time elapsed is not proof. Promotion should mean that the evidence relevant to the changed mechanism remained within agreed bounds. If the evidence is absent or ambiguous, the stage is incomplete.

### Apply the mechanism

For an upcoming change, state the failure hypothesis, then choose the smallest cohort that can actually exercise it. Record what that cohort excludes. If the excluded traffic carries material consequence, add a separate stage or another validation path. The mechanism is credible only when the cohort and the question match.

### Keep exposure identity traceable

Operators need to know which version, flag evaluation, route, and cohort affected a request or transaction. Carry that identity through logs, traces, events, and decision records without exposing sensitive customer data. If the team cannot reconstruct exposure after a failure, it cannot compare outcomes, contact affected customers, or prove that containment reached the intended population.

Keep the identity model stable across retries and asynchronous work. A request assigned to the canary should not silently switch behavior when a worker processes it later. Where stable assignment is impossible, record the transition and design the workflow to tolerate mixed behavior.

Once exposure is staged, the next problem is deciding which production evidence is strong enough to permit expansion.

## Session 2: Choosing Health Signals for Automated Decisions

A rollout controller can act only on the health model it receives. If the model watches convenient infrastructure metrics while the change damages customer completion, data integrity, or a dependency, automation will promote the wrong state with confidence.

### Start from the failure hypothesis

Identify how the change could fail and which signal would reveal that failure soon enough to act. A serialization change may require decode errors and dead-letter growth. A cache change may require origin load and stale-read evidence. A payment change may require authorization outcomes, duplicate detection, and reconciliation. Select signals because they represent mechanisms, not because they already appear on a dashboard.

### Use a layered health model

Combine customer journeys, service behavior, dependency health, data correctness, resource saturation, and business-integrity signals where relevant. The layers should explain one another. Rising latency with stable completion may justify observation. Stable latency with missing orders requires an abort. Keep the decision set small enough to interpret under time pressure and link secondary diagnostics for investigation.

### Compare canary and control carefully

A control helps separate release effects from ambient events, but comparison requires similar populations and time. Normalize for traffic, customer mix, region, hardware, cache state, and request type. Check both absolute limits and relative difference. A canary can match a degraded control and still be unacceptable. It can also look worse because it received the harder cohort.

### Allow time for delayed failure

Observation duration should reflect the mechanism. Memory growth may need sustained load. Queue delay may appear after producers outpace consumers. Data corruption may surface during reconciliation. Cache and certificate changes may wait for expiry. Define a minimum evidence volume and a minimum time where both matter. A short quiet interval should not promote a change that has not exercised its risk.

### Handle sparse and noisy signals

Low traffic can make statistical comparison unstable. Rare failures may not appear in the first cohort. Noisy metrics may stop good releases repeatedly. Use minimum sample rules, wider windows, synthetic journeys, selected representative accounts, or manual review. Do not hide uncertainty by lowering the threshold until the pipeline stays green. Record inconclusive as a legitimate result.

### Protect signal integrity

The telemetry path can fail during the same event as the service. Confirm freshness, completeness, label accuracy, cardinality, and canary attribution. Define how missing data affects the decision. For high-consequence change, missing critical telemetry should normally pause exposure rather than count as success. The team that owns the automated decision also owns its monitoring dependency.

### Avoid metric voting

Do not average a severe customer failure into several healthy resource measures. Classify signals as mandatory guardrails, comparative indicators, or diagnostics. A mandatory data-integrity failure can abort independently. Comparative signals may require several intervals. Diagnostics explain an outcome but need not gate promotion. This structure makes the decision traceable.

### Validate the health model

Replay known incidents, inject controlled faults, and examine previous releases. Ask whether the proposed signals would have stopped harmful change and whether they would have blocked healthy change. Review false promotion, false abort, and inconclusive rates over time. The goal is not zero noise. It is a decision system whose errors are visible and governable.

### Make the decision observable

Store the queries, thresholds, evaluation periods, cohort identity, data freshness, result, and action for every stage. Operators should be able to reconstruct why exposure expanded or stopped. A green status without the evidence behind it is not an operational record.

### Set a decision budget

A health model must produce a usable decision before exposure becomes unsafe or the release window loses operational support. Record how long telemetry takes to arrive, how much history the evaluation needs, and how quickly the abort can act. Slow evidence may justify a smaller cohort or a longer stage. It should not be concealed behind a fast green summary.

Review who can interpret each signal during the rollout. A specialist-only metric is a weak guardrail when the specialist is unavailable. Either make the decision rule understandable to the release owner or ensure the required expertise participates for the period in which that signal governs exposure.

Signals inform action. Guardrails and decision rights determine what the delivery system is allowed to do with that information.

## Session 3: Guardrails, Abort Conditions, and Human Authority

Progressive delivery fails when automation can expand exposure faster than the organization can understand or contain it. Guardrails define the actions the system may take, the evidence required, and the conditions that return authority to a person.

### Define four outcomes

Every stage should produce success, failure, inconclusive, or invalid evaluation. Success permits the next defined stage. Failure stops expansion and starts the recovery or containment path. Inconclusive holds the current exposure for bounded investigation. Invalid means the evaluation itself cannot be trusted, perhaps because cohort assignment or telemetry failed. Treating the last two as success converts uncertainty into exposure.

### Write abort conditions before rollout

Abort conditions should name the signal, threshold or event, persistence requirement, scope, and required action. Include hard conditions such as data-integrity violation, security exposure, unsafe dependency behavior, and customer harm that should not wait for an averaged score. Define whether abort means disabling a flag, routing traffic to stable instances, pausing workers, or containing the affected capability.

### Make promotion harder than continuation

The system should hold its current stage unless evidence explicitly permits expansion. Automatic progression based only on elapsed time is useful for mechanics and weak for safety. Promotion requires fresh evidence from the relevant cohort and a healthy control where comparison is used. If a critical query fails, the safe action is a hold unless the documented failure policy says otherwise.

### Assign human authority

Name who may pause, abort, resume, change thresholds, alter cohort assignment, and override a failed gate. Automation owns no risk. A service owner, release owner, or incident commander does. Provide a rapid path for any operator to pause exposure when credible harm appears, while restricting resume and override to roles with sufficient context and accountability.

### Govern overrides

An override needs current evidence, stated reason, scope, expiry, approving authority, and follow-up review. Do not allow a deadline or senior presence to substitute for the decision record. Emergency security fixes may need a faster exposure path, but the organization should predefine which controls remain mandatory and how increased uncertainty will be contained.

### Prevent oscillation and repeated harm

Noisy signals can repeatedly promote and abort a rollout. Use persistence windows, cooldown periods, and stable cohort assignment where appropriate. After an abort, require evidence that the cause is understood or the candidate changed before retrying. A controller that automatically retries the same harmful version can expand incident duration while remaining technically compliant with its workflow.

### Protect the control plane

Flag services, rollout controllers, routing systems, metrics stores, and identity controls form a production control plane. Restrict and audit access, test degraded behavior, and avoid one credential with unrestricted global exposure authority. Define what happens if the controller is unavailable mid-stage. The service should remain in a known state rather than drifting through partial manual actions.

### Rehearse the stop path

Test the real pause and abort mechanisms with realistic propagation, caches, long-lived processes, queued work, and regional control paths. Measure how long new exposure continues after the decision. Verify that operators can identify the affected cohort and that recovery evidence distinguishes stopped exposure from corrected state.

### Review decision quality

After releases, examine promotions, holds, aborts, overrides, and missing evidence. Repeated manual approval may indicate weak automation. Repeated false aborts may indicate poor signal design. Repeated overrides may reveal that business pressure has created an unofficial policy. Correct the operating mechanism rather than teaching people to work around it.

### Separate pause from incident declaration

Pausing a rollout is a normal control action and should not require proof that an incident already exists. The pause preserves the current exposure while the team evaluates weak or conflicting evidence. If customer harm, security exposure, or data loss meets the organization’s incident criteria, activate the incident process as well. Keeping these actions distinct prevents teams from continuing a questionable rollout merely to avoid escalation.

Define what work may continue during a hold. Investigation, reconciliation, and preparation of a corrected candidate may proceed, while exposure expansion and unrelated control changes remain blocked. This preserves evidence and prevents several interventions from changing the system at once.

Guardrails control expansion, but their practical value depends on whether the exposure boundaries correspond to real customer and infrastructure failure domains.

## Session 4: Containing Customer and Regional Impact

A rollout percentage does not describe blast radius. Ten percent of requests can include the largest customer, every transaction in one regulated market, or traffic that saturates a shared dependency used by the remaining ninety percent.

### Define the unit of exposure

Choose among request, session, account, tenant, worker, shard, availability zone, region, device version, or business process. The unit should preserve consistency and match the likely failure. Account-level assignment may be necessary when a user completes a multi-step journey. Worker-level exposure may suit queued processing. Regional waves may suit infrastructure or provider dependencies.

### Map shared failure domains

A small cohort can still affect everyone through a shared database, cache, queue, control plane, or external provider. Record which resources remain shared and how the canary could exhaust, corrupt, or lock them. Use quotas, separate pools, workload isolation, rate limits, or shadow writes where justified. If isolation is impossible, acknowledge that the true blast radius exceeds the visible cohort.

### Protect high-consequence customers

Do not assume internal users or the smallest tenants always provide representative safety. They may lack the scale, integrations, data, or contractual consequence that exercises the change. Select consenting or operationally supported cohorts where appropriate. Exclude high-consequence customers at first when that limits harm, then create a deliberate stage that validates their relevant behavior before global exposure.

### Use regional waves deliberately

Regions differ in traffic, regulation, dependency topology, capacity, time zone, support coverage, and customer behavior. A low-volume region may limit impact but fail to exercise scale. A representative region may carry unacceptable business consequence. Choose the first region from the failure model, and ensure the operations team can observe and contain it during the selected window.

### Account for data residency and replication

Tenant and regional cohorts can cross data boundaries through replicated stores, global queues, analytics pipelines, or shared identity systems. Confirm where writes travel and where derived data is produced. A feature disabled in one region may still consume data created by an enabled region. Containment must follow data and messages, not only request routing.

### Control load and dependency exposure

Traffic weight is not resource weight. A small cohort may issue expensive queries, create larger payloads, or increase calls to a rate-limited provider. Track concurrency, fan-out, queue growth, connection pools, and dependency quotas by cohort where possible. Cap canary demand so one bad version cannot starve the stable population.

### Plan customer communication

When staged exposure produces customer-visible difference, support and account teams need the cohort identity, expected behavior, known limits, and escalation path. Avoid describing customers as test subjects. Explain the controlled release in language appropriate to the relationship and any contractual or regulatory obligation. Record who may remove a customer from the cohort.

### Know when staged exposure is unsuitable

Some changes are atomic, fleet-wide, or externally mandated. Schema contractions, cryptographic revocation, shared network policy, and certain financial cutovers may not support partial exposure. Use rehearsal, compatibility, isolation, parallel operation, or bounded maintenance instead. Progressive delivery is one control, not a requirement to fragment every change.

### Reconstruct actual impact

Maintain assignment and version evidence so responders can identify who experienced which behavior. Include configuration version, region, instance or worker identity, and transaction correlation where appropriate. Without this evidence, the organization cannot communicate accurately, reconcile data, or learn whether containment worked.

### Design containment around business continuity

Containment may preserve the core journey while disabling enrichment, personalization, reporting, or other optional work. Define the minimum service the organization must continue and the capacity required to support it. A regional or tenant boundary is useful only when the stable path can absorb redirected demand without creating a second failure.

Rehearse removal from the cohort as well as entry. Verify session stickiness, queued work, cached decisions, and downstream state. Moving a customer back to the stable path can create inconsistency when a transaction began under the new behavior and finishes under the old one.

Bounded exposure creates temporary routes, flags, variants, dashboards, permissions, and operating rules. Safety declines if those controls remain after their purpose ends.

## Session 5: Cleaning Up Flags, Variants, and Temporary Controls

Temporary exposure controls become part of the production system the moment they can change behavior. If they are not removed or deliberately converted into supported controls, they accumulate hidden states, untested combinations, stale access, and uncertain recovery paths.

### Classify the control at creation

Record whether a flag is a short-lived release control, experiment, operational switch, permission control, or permanent product configuration. The type determines ownership, access, default behavior, expected lifetime, test strategy, and retirement evidence. A release flag should not quietly become a permanent entitlement system.

### Give temporary controls an owner and expiry

Store the creating team, accountable owner, purpose, creation date, expected removal date, affected services, dependencies, safe default, and removal plan. Expiry should trigger review or action, not automatically delete a control whose state may still affect customers. Escalate overdue controls through normal service governance.

### Remove code and configuration together

Setting every cohort to the winning path does not remove the flag. Delete the decision branch, obsolete configuration, routing rules, tests for unsupported variants, stale dashboards, emergency permissions, and documentation that describes the transition. Preserve tests for the final behavior. Verify that no job, client, or service still depends on the old value.

### Control combinatorial state

Multiple flags create combinations the team may never have tested. Identify interactions among controls that affect the same path and limit who can change them together. Prefer dependency rules, mutual exclusion, or a higher-level operating mode over independent switches that can produce an invalid state. Monitor actual combinations in production rather than assuming configuration intent.

### Keep operational switches deliberate

Some controls remain useful for load shedding, disabling optional work, or isolating a dependency. Treat these as supported operational interfaces. Define authorization, audit, degraded behavior, customer consequence, propagation, testing cadence, and restoration criteria. Exercise them during game days or controlled maintenance so they do not fail when first used during an incident.

### Retire variants with evidence

Confirm that traffic no longer reaches the old path, retained messages cannot invoke it, mobile or offline clients have moved beyond it, data is compatible, and rollback no longer depends on it. Remove exposure telemetry only after the retirement evidence is retained. Cleanup that removes observability first makes the final state harder to prove.

### Include the control plane in resilience work

Test flag-store outage, stale cache, partial regional propagation, malformed rules, permission loss, and accidental global change. Backup and restore configuration where it is authoritative. Limit the number of people and systems that can change global exposure. A mature flag platform can create a large blast radius if its own changes are weakly governed.

### Measure debt without rewarding concealment

Track temporary controls by age, owner, type, affected services, expiry, and overdue status. Use the inventory to schedule removal and identify recurring design problems. Do not turn raw flag count into a team ranking. A service may need several deliberate operational switches, while one forgotten release flag may carry greater risk than all of them.

### Close the progressive-delivery record

A rollout closes when full exposure is verified, delayed health conditions have passed, affected customers and regions are known, temporary controls are removed or transferred into supported ownership, and decision evidence is retained. Pipeline completion or one hundred percent routing does not satisfy these conditions by itself.

### Fund cleanup as release work

Cleanup competes with new feature work and will be deferred when it has no capacity, owner, or completion criterion. Include removal tasks in the original change, estimate them, and keep the release open until they are completed or transferred through an explicit decision. Managers should treat repeated overdue cleanup as a delivery-system defect, not an individual failure of discipline.

Removal can itself be risky. Delete one layer at a time, observe the final path, and retain a recovery option until the code and configuration state are proven. The objective is not the fastest reduction in flag count. It is a production system whose remaining states are intentional, supported, and understandable.

Progressive delivery can limit the reach of an incorrect change. It cannot establish whether the artifact, dependency, or build process entering that system is trustworthy. That is the next control boundary.

## War Story: The Five Percent Rollout That Reached Every Customer

This is a composite scenario built from recurring patterns in enterprise release incidents. Names, timings, technologies, and organizational details are fictionalized. It is not presented as a verified account of one company.

A financial-services company introduced a new fraud-scoring model behind a feature flag. The team planned to enable it for five percent of transactions, compare authorization outcomes with the existing model, and expand through four stages. The release had executive attention because the new path promised faster decisions during a seasonal traffic period.

### The first stage

The flag assigned transactions by account identifier. Five percent received the new score, while the remainder used the existing model. Application error rate and latency remained healthy. The new cohort showed no increase in declined transactions. After the planned hold, the controller promoted exposure to twenty-five percent.

The team did not see that both variants wrote to the same feature cache. The new model stored an additional attribute under a cache key shared with the old path. Old-model requests ignored the attribute, but a downstream batch process treated its presence as proof that the new model had evaluated the account. The five percent cohort changed data consumed by work serving the entire customer population.

### The misleading health model

The rollout watched synchronous request health and authorization outcome. It did not watch batch completion, cache-key contamination, review-queue growth, or the reconciliation difference between model decisions and downstream processing. The control population was no longer independent because both groups shared state. Comparison made the rollout look stable while the experiment itself altered the control.

When the batch process ran, manual-review queues grew across every account class. Customers outside the intended cohort experienced delayed transfers. Operators disabled the feature flag, but the additional cache attribute remained until expiry. The flag stopped new scoring behavior and did not remove the state already influencing downstream work.

### The abort that did not contain

The incident team first assumed the flag had failed to propagate. They spent time comparing regional flag values while the actual problem lived in shared data. Once the cache interaction was identified, responders blocked the batch rule, shortened cache lifetime, and rebuilt affected queue entries from the authoritative transaction log. Operations maintained a list of delayed transfers for customer communication and reconciliation.

### What the review found

The rollout percentage had measured request assignment, not business impact. The team had not mapped shared state between canary and control. Health signals covered the immediate application and omitted the process that completed the customer outcome. The abort procedure had been tested for routing but not for data already created by the new path.

Schedule pressure also mattered. The health review displayed a single green status, and the release owner could not see which signals were mandatory or merely informational. An analyst had noticed a small increase in review-queue age but did not know whether it could pause the rollout. Automation progressed exactly as configured while human authority remained unclear.

### The correction

The company changed the exposure design. The new model wrote to an isolated cache namespace. Canary and control data remained distinguishable through downstream processing. Promotion required end-to-end completion, review-queue age, reconciliation difference, dependency health, and synchronous service signals. Missing batch evidence produced an inconclusive result and held the stage.

Any operator could pause expansion. Resume required the release owner and service owner to acknowledge current evidence. Hard data-integrity and customer-harm signals could abort independently of the composite score. The team rehearsed flag propagation, cache cleanup, queue containment, and reconstruction before the next attempt.

The company also changed cleanup. Release flags received owners and expiry dates when created. The final stage included deletion of the decision branch, removal of temporary telemetry, and proof that retained work could no longer invoke the old variant. Long-lived operational switches moved into a separate governed inventory.

### The lesson

The next rollout progressed more slowly through its first stages because batch evidence arrived later than request metrics. It completed with less operational uncertainty. The organization accepted that waiting for the governing signal was part of the release, while waiting for irrelevant green metrics had never provided safety.

The incident was not caused by choosing five percent instead of one percent. The visible cohort was smaller than the real failure domain. Progressive delivery limited risk only after the organization aligned assignment, shared state, end-to-end evidence, abort authority, and cleanup with the way the service actually worked.

## Lessons From the Trenches

### Exposure is different from deployment

A deployed change may remain unexposed, and one exposed behavior may span several versions. Record both states and the authority that changes them.

### A percentage is not a blast radius

The real impact follows tenants, regions, data, queues, shared dependencies, and business processes. Map those boundaries before choosing a cohort.

### The cohort must exercise the risk

Random traffic can omit the data shape, scale, geography, client, or delayed process that the change affects. Select exposure from the failure hypothesis.

### Control and canary must be comparable

Traffic mix, hardware, cache state, dependency route, and shared data can distort comparison. Record differences and prevent the new path from contaminating the control.

### Missing evidence is not success

A stage should distinguish success, failure, inconclusive, and invalid evaluation. Critical telemetry loss should hold exposure unless a documented policy states otherwise.

### Health must follow the customer outcome

Infrastructure signals explain service behavior but may miss incomplete orders, duplicate work, corrupted data, or delayed settlement. Include the completion path that matters.

### Automation executes owned policy

People remain accountable for signals, thresholds, stage design, overrides, and failure behavior. Name who may pause, abort, resume, and accept uncertainty.

### Abort must be tested

Measure propagation through caches, workers, queues, and regions. Stopping new exposure does not automatically correct state already created.

### Progressive delivery has limits

Atomic or fleet-wide changes may require compatibility, rehearsal, parallel operation, isolation, or maintenance rather than artificial partial exposure.

### Temporary controls require retirement

Flags, variants, routing rules, permissions, and telemetry need owners, expiry, removal evidence, and a supported operating model if they remain.

### The practical review

### Small exposure can have shared effects

Canary traffic can mutate shared data, consume common capacity, or trigger external work used by the stable population. Isolation and reconciliation determine whether the visible cohort is the real boundary.

### Pausing is normal control

Teams should pause when evidence is weak, conflicting, or unavailable. They should not need to prove an incident before preventing wider exposure.

### Cleanup closes the decision

Full traffic does not complete the work. Remove temporary states, retain evidence, verify the final path, and transfer any permanent operational control into supported ownership.

Take one planned rollout. Identify its exposure unit, failure hypothesis, control population, shared failure domains, health signals, minimum evidence, four evaluation outcomes, decision owners, abort propagation, customer communication, and cleanup condition. Any missing element is an ungoverned expansion of risk.

## Operational Checklist: Progressive Delivery and Blast Radius Review

### Exposure design

- [ ] Identify the specific production uncertainty that staged exposure is intended to test.

- [ ] Record the deployment state separately from the exposure state.

- [ ] Select an exposure mechanism that can control the changed behavior and its degraded path.

- [ ] Define the assignment unit, such as request, account, tenant, worker, shard, zone, or region.

- [ ] Verify that assignment remains stable for transactions or journeys that require consistency.

- [ ] Record which traffic, data shapes, clients, regions, and dependencies the first cohort excludes.

- [ ] Demonstrate that the canary receives enough relevant workload to exercise the failure hypothesis.

- [ ] Verify that canary and control use comparable capacity, routing, cache state, and dependency paths.

- [ ] Identify shared databases, queues, caches, control planes, and providers that extend the true blast radius.

- [ ] Apply quotas, isolation, rate limits, or containment where a small cohort can exhaust shared resources.

### Health evidence

- [ ] Define customer-journey and business-completion signals for the changed path.

- [ ] Define service, dependency, data-integrity, capacity, and security signals where relevant.

- [ ] Classify each signal as a mandatory guardrail, comparative indicator, or diagnostic.

- [ ] Set absolute safety limits in addition to canary-versus-control comparisons.

- [ ] Define minimum evidence volume and observation time from the expected failure latency.

- [ ] Verify telemetry freshness, completeness, cohort attribution, and control independence.

- [ ] Record how sparse, noisy, delayed, missing, and conflicting evidence affects the decision.

- [ ] Test the health model against known incidents and healthy historical releases.

### Guardrails and authority

- [ ] Define success, failure, inconclusive, and invalid outcomes for every stage.

- [ ] Record the actions allowed after each evaluation outcome.

- [ ] Assign authority to pause, abort, resume, change thresholds, and override a decision.

- [ ] Allow a rapid pause when an operator presents credible evidence of harm.

- [ ] Require overrides to record evidence, reason, scope, authority, expiry, and review.

- [ ] Prevent automatic retry of an unchanged candidate after a harmful abort.

- [ ] Test degraded behavior when the flag, routing, controller, or metrics system is unavailable.

- [ ] Measure how long exposure continues after a pause or abort decision.

- [ ] Verify that containment covers cached configuration, long-lived workers, queues, and regional propagation.

### Customer and regional containment

- [ ] Identify customers, transactions, versions, regions, and configuration states affected by each stage.

- [ ] Prepare support and account teams for customer-visible differences and escalation.

- [ ] Confirm data-residency, replication, and regulatory boundaries before cross-region exposure.

- [ ] Document when progressive exposure is unsuitable and which alternative control will be used.

### Cleanup and retained evidence

- [ ] Classify every flag or temporary control by purpose, owner, safe default, and expected lifetime.

- [ ] Assign an expiry and removal condition when a temporary control is created.

- [ ] Verify that retained clients, messages, jobs, and data no longer depend on the retiring variant.

- [ ] Remove obsolete code, configuration, routing rules, access, telemetry, tests, and documentation together.

- [ ] Treat retained operational switches as supported interfaces with access, audit, testing, and restoration rules.

- [ ] Retain stage evidence, decisions, cohort identity, abort actions, and cleanup proof with the release record.

## Further Reading

**Google, The Site Reliability Workbook: Canarying Releases**

Provides a rigorous treatment of canary populations, controls, evaluation, confidence, and the operational cost of false promotion and false rejection. Use it to design the evidence model, not merely the traffic percentages.

**Microsoft Azure Well-Architected Framework, Safe Deployment Practices**

Connects progressive exposure with health models, failure detection, deployment guardrails, emergency paths, and decommissioning. It is useful for reviewing the complete operating system around staged change.

**Pete Hodgson, Feature Toggles**

Explains release, experiment, operational, and permissioning toggles, along with routing, configuration, testing, and lifecycle concerns. Use it to distinguish temporary release controls from supported product or operational behavior.

**Martin Fowler, Canary Release**

Introduces canary release as limited production exposure before wider rollout. Read it with the chapter’s cautions about representativeness, shared failure domains, and end-to-end evidence.

**Argo Rollouts Documentation, Canary and Analysis**

Documents one implementation of weighted traffic, rollout steps, metric analysis, pause, abort, and rollback behavior. Use it for mechanism-level understanding, not as proof that any default configuration is safe.

**Jez Humble and David Farley, Continuous Delivery**

Provides the broader delivery foundations for small changes, feedback, automation, deployment pipelines, and recoverability that make progressive exposure practical.

**Google, Site Reliability Engineering: Release Engineering**

Describes repeatable release mechanisms and the collaboration between release engineering and SRE. It provides context for canary strategy, rollback, and controlled production change.

**Microsoft Azure Architecture Center, Deployment Stamps Pattern**

Shows how independently deployable units can support regional or tenant isolation. Use it to reason about structural blast-radius boundaries rather than traffic percentages alone.

**Martin Fowler, Dark Launching**

Explains how production workload can exercise a new path without using its result. It is useful when the primary uncertainty concerns capacity or dependency behavior, while also requiring careful control of side effects.

## The Next Trench

### Artifact Supply Chains as Trust Systems

Progressive delivery controls how far a change reaches and how quickly evidence can stop it. That control assumes the release candidate is the artifact the organization intended to build, approve, store, and deploy.

A carefully staged rollout can still distribute an unsigned image, a replaced package, an unverified dependency, or an artifact built through a compromised path. Limiting exposure may reduce immediate harm, but it does not establish provenance or prevent an untrusted input from entering the delivery system.

Chapter 20, Artifact Supply Chains and Build Integrity, examines registries, provenance, software bills of materials, signing, verification, retention, and policy enforcement as one trust system. It asks which evidence must travel with an artifact, where trust decisions occur, and how the organization prevents a convenient exception from becoming the path into production.

The next boundary is not how much traffic receives the change. It is whether the organization can prove what the change is and why it should be trusted.

---

## About This Sample

This chapter is part of *DevOps in the Trenches*, a 63-chapter field guide to building, changing, securing, operating, and leading production systems under pressure.

This public sample may be read and linked from this repository. It may not be republished, sold, translated, scraped into another publication, or redistributed as a separate work without written permission from the copyright holder.

[Return to all free chapters](README.md) | [Read the previous sample](chapter-01-production-does-not-care-about-your-transformation-plan.md) | [Read the next sample](chapter-54-incident-command-and-decision-making-under-pressure.md)
