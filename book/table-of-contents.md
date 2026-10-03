# DevOps in the Trenches

## Master Table of Contents

*The field guide to building, changing, securing, operating, and leading production systems under pressure.*

This book is written for engineers, technical leaders, platform teams, SREs, security practitioners, architects, and managers who are accountable for real systems. It is not a catalogue of tools and it does not present DevOps as a transformation slogan. It follows the operating life of a production system, from ownership and architecture through delivery, security, reliability, incidents, economics, and executive decisions.

Each chapter is a practical learning unit with an opening production scenario, focused sessions, a field case or war story, lessons from the trenches, an operational checklist, and carefully selected further reading.

## Part I: Seeing Production Clearly

Before an organization can improve delivery, it must see the system it is actually operating. This part replaces transformation theatre with production evidence.

### Chapter 1: Production Does Not Care About Your Transformation Plan

1. The myth of the DevOps transformation
2. Why tools cannot repair a broken operating model
3. The difference between activity and capability
4. What production exposes about the organization
5. The first questions a serious transformation must answer

### Chapter 2: Map the System Before You Change It

1. Finding the real path from idea to production
2. Mapping handoffs, queues, approvals, and rework
3. Identifying shadow systems and unofficial operators
4. Understanding technical, organizational, and regulatory constraints
5. Building an enterprise context map that drives decisions

### Chapter 3: Flow, Queues, and the Cost of Waiting

1. Why most delivery time is waiting time
2. Work in progress and the economics of unfinished change
3. Batch size, feedback speed, and operational risk
4. Local optimization versus end-to-end flow
5. Turning value-stream evidence into action

### Chapter 4: Velocity, Stability, and Risk Are One Problem

1. The false choice between speed and safety
2. How small changes reduce operational exposure
3. Feedback quality as a control mechanism
4. Measuring delivery without gaming the system
5. Using constraints to improve both throughput and reliability

### Chapter 5: Capability Without Maturity Theater

1. Why generic maturity models mislead
2. Assessing capabilities in their operating context
3. Establishing an honest baseline
4. Choosing measures that influence decisions
5. Building a roadmap around constraints, not fashion

## Part II: Ownership, Teams, and Decision Rights

Production systems fail at organizational seams. This part defines who owns services, who makes decisions, and how teams cooperate when the consequences are real.

### Chapter 6: Teams Built to Own Services End to End

1. Service ownership beyond a name in a catalogue
2. Stream-aligned teams and cognitive load
3. Designing team boundaries around the flow of change
4. Ownership during normal operations and incidents
5. Scaling responsibility without creating silos

### Chapter 7: Drawing the Lines Between Platform, SRE, Security, and Operations

1. The responsibilities each function should own
2. Embedded, centralized, and federated operating models
3. Avoiding ticket queues disguised as specialist teams
4. Escalation paths and decision rights
5. Resolving gaps, overlaps, and contested ownership

### Chapter 8: Culture Under Operational Pressure

1. Psychological safety without lowering standards
2. Blamelessness, accountability, and learning
3. Incentives that shape technical behavior
4. Communication across remote and hybrid teams
5. What incidents reveal about the real culture

### Chapter 9: Change Leadership Engineers Will Trust

1. Why technically correct change still fails
2. Building credibility with engineers and executives
3. Decision records, dissent, and reversible choices
4. Preserving institutional memory as teams grow
5. Leading adoption without mandates or theatre

## Part III: Designing for Operability

Reliable operation begins before code reaches a pipeline. This part makes operability, dependency risk, and production readiness explicit design responsibilities.

### Chapter 10: Design for Operability Before the First Deployment

1. Operability as a product requirement
2. Designing observable and controllable services
3. Safe startup, shutdown, degradation, and recovery
4. Administrative interfaces and emergency controls
5. Making operational acceptance part of design review

### Chapter 11: Dependencies and the Physics of Partial Failure

1. Dependency maps that reflect runtime reality
2. Timeouts, retries, backoff, and deadlines
3. Backpressure, load shedding, and isolation
4. Consistency, coordination, and failure domains
5. Designing for degraded service instead of total collapse

### Chapter 12: Production Readiness Must Be Proven

1. What a production-readiness review must establish
2. Ownership, support, observability, security, and capacity evidence
3. Launch criteria, exceptions, and risk acceptance
4. Readiness for rollback, recovery, and incident response
5. Reassessing readiness as systems and traffic change

### Chapter 13: Architecture Decisions That Survive Turnover

1. Recording decisions without creating document graveyards
2. Connecting trade-offs to operational consequences
3. Designing boundaries that teams can maintain
4. Recognizing architectural drift and accidental coupling
5. Evolving systems without erasing their history

## Part IV: Moving Change Without Losing Control

Delivery is a production system in its own right. This part follows change from source control through build, verification, release, and controlled exposure.

### Chapter 14: Source Control Is Production Infrastructure

1. Repository strategy and ownership at scale
2. Branching, integration, and the cost of divergence
3. Protecting critical paths without blocking flow
4. Managing monorepos, multirepos, and shared components
5. Recovering from source-control compromise or failure

### Chapter 15: Builds You Can Reproduce and Trust

1. Hermetic and repeatable build principles
2. Dependency resolution and version discipline
3. Build isolation, caching, and determinism
4. Provenance from source to artifact
5. Treating the build service as critical infrastructure

### Chapter 16: CI/CD Is a Production Service

1. Pipeline architecture, ownership, and service levels
2. Runner isolation and workload boundaries
3. Failure handling, concurrency, and queue pressure
4. Observability for delivery systems
5. Recovering when the deployment system is unavailable

### Chapter 17: Test the Risks Staging Cannot Reproduce

1. Choosing tests by failure consequence
2. Contract, integration, performance, and resilience testing
3. Test data, environment fidelity, and false confidence
4. Verifying infrastructure and policy changes
5. Testing safely in production

### Chapter 18: Release Engineering Without Heroics

1. Coordinating application, database, configuration, and infrastructure change
2. Forward and backward compatibility
3. Release orchestration across teams and services
4. Rollback, roll-forward, and irreversible change
5. Release evidence and operational handover

### Chapter 19: Progressive Delivery and Blast-Radius Control

1. Feature flags, canaries, and staged exposure
2. Choosing health signals for automated decisions
3. Guardrails, abort conditions, and human authority
4. Containing customer and regional impact
5. Cleaning up flags, variants, and temporary controls

## Part V: Trusted Automation and Software Supply Chains

Automation increases both speed and consequence. This part establishes how infrastructure, configuration, credentials, artifacts, and policy remain trustworthy at scale.

### Chapter 20: Artifact Supply Chains as Trust Systems

1. Registries as control points, not file stores
2. Provenance and build integrity
3. Software bills of materials and dependency visibility
4. Signing, verification, and admission decisions
5. Retention, revocation, and forensic evidence

### Chapter 21: Infrastructure as Code Without State Panic

1. Designing modules and ownership boundaries
2. State, locking, concurrency, and recovery
3. Plans, approvals, and policy checks
4. Drift detection and reconciliation
5. Importing, refactoring, and replacing live infrastructure safely

### Chapter 22: Configuration Without Drift

1. Separating code, configuration, and secrets
2. Configuration schemas, validation, and compatibility
3. Environment variance and promotion
4. Dynamic configuration and safe rollout
5. Detecting and reversing configuration-induced incidents

### Chapter 23: Secrets and Workload Identity

1. The enterprise secret problem
2. Central secret management and cloud-native stores
3. Workload identity and short-lived credentials
4. Rotation without synchronized failure
5. Privileged access and break-glass controls

### Chapter 24: Securing Runners, Pipelines, and Automation

1. Why pipeline credentials require separate treatment
2. Token scope, audience, lifetime, and delegation
3. Isolating hosted and self-managed runners
4. Preventing exposure through templates, caches, artifacts, and logs
5. Detecting, revoking, and recovering from automation compromise

### Chapter 25: Policy as Code Without Policy Outages

1. Translating intent into enforceable controls
2. Choosing preventive, detective, and advisory policies
3. Testing policies and their failure modes
4. Exceptions, ownership, expiry, and evidence
5. Operating the policy engine as production infrastructure

## Part VI: Platforms, Cloud Foundations, and Compute

Platforms should reduce cognitive load without hiding operational truth. This part moves from product thinking to the foundations on which workloads actually run.

### Chapter 26: The Internal Developer Platform as a Product

1. Platform customers, problems, and product boundaries
2. Self-service without loss of control
3. Platform APIs, portals, and paved capabilities
4. Roadmaps driven by developer evidence
5. Measuring adoption, outcomes, and trust

### Chapter 27: Golden Paths With Escape Hatches

1. Designing a path teams voluntarily choose
2. Secure and reliable defaults
3. Extension points and supported variation
4. Versioning templates and managing upgrades
5. Preventing golden paths from becoming golden cages

### Chapter 28: Platform Governance at Scale

1. Platform ownership and funding
2. Service levels, support models, and deprecation
3. Federated platforms and shared capabilities
4. Preventing platform sprawl and duplicated control planes
5. Governance that protects both autonomy and coherence

### Chapter 29: Cloud Foundations and Landing Zones

1. Account, subscription, and project structure
2. Identity, network, logging, and policy foundations
3. Environment isolation and organizational guardrails
4. Bootstrap, change, and recovery of foundational services
5. Measuring whether the foundation enables delivery

### Chapter 30: Compute and Host Reality Beyond Containers

1. Virtual machines in a container-first organization
2. Linux hosts, kernels, processes, and filesystems
3. Serverless governance and failure modes
4. Batch, scheduled, and high-throughput workloads
5. Mainframe and legacy compute integration

### Chapter 31: Hybrid, Multi-Cloud, and Edge Where Abstraction Leaks

1. Workload placement based on constraints
2. Connectivity, identity, and policy across boundaries
3. Data movement and consistency
4. Offline operation and intermittent connectivity
5. Operating heterogeneous estates without pretending they are identical

## Part VII: Kubernetes, Networks, and Distributed Integration

Modern infrastructure is a web of shared control planes and network dependencies. This part focuses on the places where abstractions most often break.

### Chapter 32: Running Kubernetes at Enterprise Scale

1. Cluster topology and fleet strategy
2. GitOps and desired-state operations
3. Cluster lifecycle and upgrade discipline
4. Resource management, scheduling, and cost
5. Troubleshooting the control plane and workload plane

### Chapter 33: Governing Shared Kubernetes Environments

1. Namespace ownership and tenancy boundaries
2. RBAC at organizational scale
3. Quotas, fairness, and noisy-neighbor control
4. Admission policy and exception handling
5. Platform-team and application-team responsibilities

### Chapter 34: Enterprise Networking Without Guesswork

1. Network boundaries, routing, and segmentation
2. Ingress, egress, load balancing, and failover
3. Multi-region and multi-cloud connectivity
4. Network observability and packet-level evidence
5. Troubleshooting connectivity systematically

### Chapter 35: DNS, Traffic, and Certificates: The Hidden Control Plane

1. DNS resolution paths and failure modes
2. TTLs, caching, propagation, and migration
3. Traffic management and global routing
4. Certificate issuance, renewal, and trust chains
5. Designing safe cutovers and emergency rerouting

### Chapter 36: Service Mesh and mTLS Without Hype

1. The problems a mesh can and cannot solve
2. Sidecars, ambient models, and operational cost
3. Identity, mTLS, authorization, and policy
4. Telemetry, retries, and conflicting control loops
5. Adoption, debugging, and exit strategy

### Chapter 37: API Contracts That Survive Change

1. Ownership, discovery, and lifecycle governance
2. Contract-first design and compatibility
3. Versioning, deprecation, and consumer migration
4. Security, rate limits, and abuse controls
5. Testing and observing API behavior in production

### Chapter 38: Queues, Events, and Asynchronous Failure

1. Delivery semantics and idempotency
2. Ordering, duplication, replay, and poison messages
3. Backpressure and consumer lag
4. Schema evolution and event contracts
5. Operating brokers, streams, and dead-letter paths

## Part VIII: Data, Storage, and Recovery

Data changes the meaning of failure. This part covers systems where rollback is limited, recovery is stateful, and evidence matters more than optimistic dashboards.

### Chapter 39: Databases in the Delivery Lifecycle

1. Database architecture and ownership
2. Safe schema and data migrations
3. Compatibility across mixed application versions
4. Performance, connection pressure, and contention
5. Security, auditing, and operational access

### Chapter 40: Data Pipelines Under Pressure

1. Batch and stream processing architecture
2. Orchestration, retries, and idempotency
3. Data quality, freshness, and lineage
4. Backfills, reprocessing, and late-arriving data
5. Governance without destroying delivery flow

### Chapter 41: Storage Architecture and Data Lifecycle

1. Block, file, object, and distributed storage choices
2. Performance, durability, and consistency trade-offs
3. Classification, retention, archival, and deletion
4. Encryption, access, and tenant boundaries
5. Capacity, cost, and operational failure modes

### Chapter 42: Backup Truth Versus Backup Illusion

1. Defining the data and configuration that must survive
2. Backup architecture, isolation, and immutability
3. Ransomware, credential compromise, and blast radius
4. Monitoring backup evidence without trusting job success
5. Retention, compliance, and recoverability

### Chapter 43: Restore Engineering

1. Recovery objectives grounded in business reality
2. Restore order and dependency sequencing
3. Automated, partial, and point-in-time recovery
4. Proving integrity and service usability after restoration
5. Running restore drills that produce operational evidence

### Chapter 44: Disaster Recovery and Business Continuity

1. Failure scenarios beyond infrastructure loss
2. Regional and provider-level recovery architecture
3. Failover, failback, and data reconciliation
4. Business processes, people, suppliers, and communications
5. Exercising the plan and governing unresolved risk

## Part IX: Security, Identity, and Compliance in Delivery

Security must influence the design and delivery system without becoming an unaccountable queue. This part treats identity, vulnerability, trust, and evidence as operational concerns.

### Chapter 45: IAM at Enterprise Scale

1. Human and machine identity layers
2. Federation, lifecycle, and authoritative sources
3. Least privilege without operational paralysis
4. Role explosion, entitlement drift, and access reviews
5. Emergency access, monitoring, and revocation

### Chapter 46: Security as a Delivery Constraint

1. Security gates based on risk, not ritual
2. Vulnerability prioritization engineers respect
3. Threat modeling that changes design
4. Secure defaults and usable remediation paths
5. Measuring exposure, time at risk, and control effectiveness

### Chapter 47: Zero Trust in Enterprise Reality

1. Identity before network location
2. Internal services are not automatically safe
3. Trust decisions across service boundaries
4. Legacy systems, migration, and compensating controls
5. Developer experience and zero-trust governance

### Chapter 48: Compliance Without Killing Delivery

1. Turning obligations into operational controls
2. Audit evidence that generates itself
3. SOC 2, ISO 27001, PCI, and shared engineering patterns
4. Separation of duties without bureaucratic delay
5. Continuous control monitoring and defensible exceptions

## Part X: Reliability Engineering Before the Incident

Reliability is the work performed before alarms fire. This part connects telemetry, objectives, capacity, failure mechanics, and controlled experimentation.

### Chapter 49: Observability Engineers Can Act On

1. Logs, metrics, traces, profiles, and events
2. Instrumenting around user journeys and system boundaries
3. Correlation, context propagation, and cardinality
4. Alerting on symptoms without exhausting responders
5. Managing telemetry quality, retention, and cost

### Chapter 50: Reliability With SLIs, SLOs, and Error Budgets

1. Selecting service-level indicators that represent users
2. Setting targets without availability theatre
3. Burn rates and actionable alerting
4. Error budgets as operational decision tools
5. Reliability reviews and explicit risk acceptance

### Chapter 51: The SRE Operating Model, Toil, and Sustainable Ownership

1. Reliability as an engineering function
2. Central, embedded, and consulting SRE models
3. Engagement criteria and responsibility boundaries
4. Identifying, measuring, and reducing toil
5. Preventing SRE from becoming the new operations queue

### Chapter 52: Capacity and Performance Before Saturation

1. Demand modeling and capacity envelopes
2. Load, stress, endurance, and scalability testing
3. Application, database, network, and infrastructure bottlenecks
4. Autoscaling behavior, lag, and instability
5. Forecasting, headroom, and cost-aware performance decisions

### Chapter 53: Failure Patterns, Chaos, and Resilience Testing

1. Cascading failure, retry storms, and thundering herds
2. Resource exhaustion and dependency collapse
3. Silent degradation and gray failure
4. Designing safe experiments and game days
5. Stop conditions, evidence, and remediation ownership

## Part XI: Operating Under Pressure

When prevention is no longer enough, operating discipline determines the size and duration of the damage. This part is the book's practical incident field guide.

### Chapter 54: Incident Management for Adults

1. Declaring incidents and assigning severity
2. Command roles, authority, and span of control
3. War rooms that support decisions instead of noise
4. Technical, customer, executive, and regulatory communication
5. Stabilization, recovery, and incident closure

### Chapter 55: On-Call Systems People Can Sustain

1. Designing rotations around service reality
2. Readiness, training, shadowing, and certification
3. Escalation paths and follow-the-sun operations
4. Measuring load, interruptions, and responder health
5. Fixing the system instead of normalizing exhaustion

### Chapter 56: The Production Debugging Playbook

1. Stabilize first, investigate with hypotheses
2. Timelines, change correlation, and scope isolation
3. Logs, traces, metrics, profiles, and system evidence
4. Network, resource, and dependency investigation
5. Preserving evidence while restoring service

### Chapter 57: Post-Incident Learning That Changes the System

1. Reconstructing conditions, decisions, and contributing factors
2. Moving beyond root-cause storytelling
3. Writing actions that change risk
4. Ownership, prioritization, and closure of corrective work
5. Sharing lessons without blame or institutional amnesia

## Part XII: Leading the Whole System

The final part connects engineering choices to money, suppliers, executive decisions, emerging automation, and long-term stewardship.

### Chapter 58: FinOps From Engineer to Enterprise

1. Unit economics and the real drivers of cloud cost
2. Allocation, showback, chargeback, and shared services
3. Engineering-controlled waste and cost-aware design
4. Commitments, procurement, and demand uncertainty
5. Cost governance that protects reliability and delivery

### Chapter 59: Vendor Lock-In and the Discipline of Exit

1. Distinguishing dependency from unacceptable concentration risk
2. Portability myths and managed-service trade-offs
3. Data, identity, policy, and operational lock-in
4. Architecture choices that preserve negotiating power
5. Exit plans, drills, and evidence

### Chapter 60: Executive Reporting Without False Confidence

1. Translating technical evidence into business consequence
2. Reporting reliability, security, delivery, cost, and recovery honestly
3. Leading indicators, lagging indicators, and uncertainty
4. Dashboards that support decisions rather than theatre
5. Communicating risk in executive timeframes

### Chapter 61: AI-Assisted Delivery and Operations With Human Accountability

1. Where AI can improve engineering flow
2. Anomaly detection, prediction, and incident assistance
3. AI-generated code, configuration, and operational advice
4. Evaluation, provenance, privacy, and model risk
5. Keeping consequential decisions under accountable human control

### Chapter 62: Sustainable Infrastructure Is Production Engineering

1. Waste reduction as operational discipline
2. Carbon-aware workload placement and scheduling
3. Storage, data-transfer, and retention impact
4. Sustainable delivery and hardware lifecycle choices
5. Metrics that connect efficiency, cost, and environmental impact

### Chapter 63: The Engineer Who Can Operate the Whole System

1. Seeing technical and organizational systems together
2. Making decisions with incomplete information
3. Building judgment through drills, incidents, and reflection
4. Teaching the next operator and preserving hard-won knowledge
5. Leaving systems safer, clearer, and easier to change

## Appendices

### Appendix A: Production Readiness Review Template

### Appendix B: Service Ownership and Dependency Record

### Appendix C: Incident Command and Communication Templates

### Appendix D: Post-Incident Review Template

### Appendix E: SLI, SLO, and Error-Budget Worksheet

### Appendix F: Architecture Decision Record Template

### Appendix G: Change and Release Risk Assessment

### Appendix H: Disaster-Recovery Exercise Pack

### Appendix I: Platform and Developer-Experience Scorecard

### Appendix J: Security, Supply-Chain, and Compliance Evidence Map

### Appendix K: FinOps and Vendor-Dependency Review

### Appendix L: Glossary of Production Engineering Terms

### Appendix M: Further Reading and Standards Map
