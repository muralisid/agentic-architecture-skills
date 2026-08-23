# The target-state architecture

Seven planes across fourteen layers, two binding rules, and the two-estate reality every design must survive.

Source: https://www.agenticarchitectureskills.com/architecture (Markdown: https://www.agenticarchitectureskills.com/architecture.md)

> **In plain terms.**
>
> This page is the one-page map of how a company runs AI agents safely at scale. It shows the parts of your business that agents touch, the new capabilities you build around them, and where the controls and the evidence live. The thing to remember: an instruction written to an AI model is a request, while a rule checked by a separate system is a control.

## The whole thing, on one page

Everything below is in this diagram. It shows the fourteen layers, each with its control point, key mechanisms, and market products. It shows the seven planes that group them. It shows the ten cross-cutting concerns as columns, marking who owns and who enforces each, plus the products that serve them. Underneath sit the four deterministic zones, where a model may advise but never decide. Products are named for orientation as of August 2026; they are representative rather than exhaustive, and they are not endorsements. If you read one artifact from this guide, read this one.

**Figure: The agentic enterprise, on one page.** Fourteen layers with their control point, key mechanisms, and the products that serve them, grouped into the seven planes, with the ten cross-cutting concerns as columns and the four deterministic zones underneath.

Diagram: https\://www\.agenticarchitectureskills.com/diagrams/target-state.svg

## The shape

**In short:** Agents are built across the systems you already own, with seven new groups of capability around them. Two rules hold: an agent never enforces its own rules and never keeps its own evidence.

An agentic enterprise is fourteen layers of estate with a seven-plane agent system built across them. The layers are what you already own: infrastructure, data, integration, records, line-of-business systems, and the rest. The planes are what you build. There are seven. **Execution** is where agent work runs. **Action** is how agents reach your systems. **Knowledge** is what agents know. **Control** is what is allowed. **Improvement** is how behaviour changes. **Evidence** is what you can prove afterward. **Human** is who decides and answers for it.

**Figure: The seven-plane target architecture.** Enforcement and evidence must remain outside the agent’s influence.

The same seven planes apply to every archetype; their contents and operating ownership differ.

**What the diagram shows:** Seven horizontal architecture planes for execution, action, knowledge, control, improvement, evidence, and human accountability, connected by policy and trace flows. The map contains Execution plane: Runtimes and durable sessions; Action plane: Gateways and governed APIs; Knowledge plane: Curated corpora and memory; Control plane: Identity, policy, approvals, budgets; Improvement plane: Evals, promotion, demotion; Evidence plane: Independent traces and records; Human plane: Intent, accountability, exceptions. Its connections are human to control for intent and mandate; control to action for deterministic permission; execution to action for tool request; action to evidence for immutable trace; evidence to improvement for evaluation input.

Diagram: https\://www\.agenticarchitectureskills.com/figures/seven-plane-architecture.svg

Two rules bind the planes, and they are the two most often violated:

1. **Enforcement lives in the control plane, never in the execution plane.** An instruction in a prompt is a preference. The same rule becomes a control when a gateway or a policy decision point checks it. A gateway is the single door every agent request passes through; a policy decision point is the component that says yes or no to each action. Every layer page names where its enforcement actually sits.
2. **The evidence plane is fed by collection the agent cannot influence.** Anything an agent reports about itself is testimony, not evidence. Traces (the step-by-step log of each run), decisions, and provenance (where each piece of information came from) are collected by a separate channel the agent cannot touch.

## The crosswalk

**Figure: Fourteen estate layers, seven agent-system planes.** Layers describe what the enterprise owns; planes describe how governed agent work operates across it.

A layer can contribute to more than one plane; the planes cut across the estate rather than containing its layers.

**What the diagram shows:** Crosswalk matrix showing fourteen enduring enterprise layers down the rows and seven agent-system planes across the columns, with several layers contributing to multiple planes. The matrix crosses R01 Infrastructure, R02 Data platform, R03 Integration fabric, R04 Systems of record, R05 LOB and OT, R06 Intelligence and learning, R07 Agent platform, R08 Productivity and collaboration, R09 Experience and channels, R10 Security and identity, R11 Governance, risk and sovereignty, R12 Observability and FinOps, R13 Operating model, R14 Agent data engineering with Execution, Action, Knowledge, Control, Improvement, Evidence, Human. Annotated cells are R01 Infrastructure by Execution: Runtime and model serving; R02 Data platform by Knowledge: Governed source data; R03 Integration fabric by Action: Gateway and tool path; R04 Systems of record by Action: Authoritative action boundary; R05 LOB and OT by Action: Operational actuation boundary; R06 Intelligence and learning by Improvement: Evaluation and promotion; R07 Agent platform by Execution: Agent runtime; R07 Agent platform by Control: Registry and runtime controls; R08 Productivity and collaboration by Human: Human work surface; R09 Experience and channels by Human: Customer and employee edge; R10 Security and identity by Control: Identity and policy; R11 Governance, risk and sovereignty by Control: Risk and sovereignty rules; R11 Governance, risk and sovereignty by Evidence: Decision and consultation records; R12 Observability and FinOps by Evidence: Independent traces and cost; R13 Operating model by Human: Accountability and supervision; R14 Agent data engineering by Knowledge: Curation and memory; R14 Agent data engineering by Improvement: Eval-data flywheel. Important boundary: The cells show primary contributions, not exclusive ownership. Every deployed workload uses all seven planes across the relevant estate layers.

Diagram: https\://www\.agenticarchitectureskills.com/figures/layers-planes-crosswalk.svg

| Plane       | Built primarily from                                                                                           | Deep pages                                                                                                                                                                                                                                                   |
| ----------- | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Execution   | Sandboxes, runtimes, durable sessions, model serving                                                           | [R01](https://www.agenticarchitectureskills.com/layers/r01-infrastructure), [R07](https://www.agenticarchitectureskills.com/layers/r07-agent-platform)                                                                                                       |
| Action      | Tool gateway, wrapped governed APIs (application programming interfaces), OT (operational technology) boundary | [R03](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric), [R04](https://www.agenticarchitectureskills.com/layers/r04-systems-of-record), [R05](https://www.agenticarchitectureskills.com/layers/r05-lob-and-ot)                        |
| Knowledge   | Governed indexes, curation pipelines, memory tiers                                                             | [R02](https://www.agenticarchitectureskills.com/layers/r02-data-platform), [R14](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering)                                                                                                |
| Control     | Identity, policy decision points, registry, budgets                                                            | [R10](https://www.agenticarchitectureskills.com/layers/r10-security-and-identity), [R11](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty), [R07](https://www.agenticarchitectureskills.com/layers/r07-agent-platform)       |
| Improvement | Evals, judges, promotion gates, staged rollout                                                                 | [R06](https://www.agenticarchitectureskills.com/layers/r06-intelligence-and-learning), [R12](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops)                                                                                  |
| Evidence    | Traces, provenance chains, retention                                                                           | [R12](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops), [R11](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty)                                                                                |
| Human       | Supervision instrumentation, accountability, channels                                                          | [R13](https://www.agenticarchitectureskills.com/layers/r13-operating-model), [R08](https://www.agenticarchitectureskills.com/layers/r08-productivity-and-collaboration), [R09](https://www.agenticarchitectureskills.com/layers/r09-experience-and-channels) |

## The two-estate reality

**In short:** Some agents run through systems you control, where you can see and govern everything. Others run inside vendor products, where you govern only what the vendor's settings allow, so every design has to work for both.

Agent work runs in two estates, and every design must survive that fact. The **metered estate** flows through your own gateways. It is fully governable, budget-enforced, and traced on your terms. The **licensed estate** (suite copilots, agents embedded in record systems) runs on vendor control planes your gateway never sees. You can govern it only through tenant policy settings and by extracting telemetry, the activity measurements the vendor's system emits. The vendor interfaces (APIs) for doing so have documented gaps. Architectures that assume one gateway governs everything are the most common structural error at enterprise scale. A cost model that prices agent actions but not the governance plane is wrong by a variable amount. Governance is a separately priced per-user item (a SKU, or stock-keeping unit) in one vendor stack and free in another \[vendor pricing].

**Figure: Licensed and metered agent estates.** One gateway cannot govern agents that run inside a vendor’s licensed control plane.

Use tenant policy and telemetry extraction for the licensed estate; direct gateway enforcement for the metered estate.

**What the diagram shows:** Two-estate architecture comparing licensed suite agents governed through tenant policy with metered agents governed through an enterprise gateway and shared evidence plane. The comparison contains 2 groups: Licensed estate, containing Vendor execution plane, Tenant policy, Telemetry extraction, Limited gateway visibility; Metered estate, containing Enterprise runtime, Gateway enforcement, Per-run budgets, Full action trace.

Diagram: https\://www\.agenticarchitectureskills.com/figures/support-licensed-metered-estates.svg

## Three builds of the same planes

**In short:** Large regulated enterprises, mid-sized companies, and digital-native companies build the same seven planes in different ways. The diagram shows what each one builds, rents, or still has to add.

**Figure: One frame, three target architectures.** Use the same plane model but adapt ownership and controls to the enterprise’s real operating capacity.

A global regulated enterprise, mid-market organisation, and digital native should not build the same control-plane implementation.

**What the diagram shows:** Three side-by-side target architectures comparing global regulated, mid-market, and digital-native enterprises across defining constraint, control ownership, and primary gap. The comparison contains 3 groups: Global regulated, containing Two estates at the edge, Independent control and evidence, Sovereignty routing from day one; Mid-market, containing Control plane is rented, Purpose-scoped curation is the build priority, Operate one independent capability at most; Digital native, containing Execution arrives first, Retrofit control and evidence now, Discipline is the limiting factor.

Diagram: https\://www\.agenticarchitectureskills.com/figures/three-target-architectures.svg

A globally regulated enterprise runs both estates and doubles nothing else: same knowledge plane, same registry, same evidence machinery, two enforcement surfaces. A mid-market estate rents the control plane from its productivity vendor and builds only the knowledge plane, which vendors do not curate for you. A digital-native estate has the execution and action planes early. It must add control and evidence before autonomy rises, which is what the [autonomy contract](https://www.agenticarchitectureskills.com/architecture/autonomy-contract) enforces.

## Where to go deep

The cross-layer mechanics live in six spine pages. They are [the four deterministic zones](https://www.agenticarchitectureskills.com/architecture/deterministic-zones), [the identity and delegation chain](https://www.agenticarchitectureskills.com/architecture/identity-chain), [enforcement outside the model](https://www.agenticarchitectureskills.com/architecture/enforcement), [the data-to-memory pipeline](https://www.agenticarchitectureskills.com/architecture/data-to-memory), [the learning flywheel](https://www.agenticarchitectureskills.com/architecture/learning-flywheel), and [the autonomy contract](https://www.agenticarchitectureskills.com/architecture/autonomy-contract). The full [concern matrix](https://www.agenticarchitectureskills.com/architecture/concern-matrix) shows all ten cross-cutting concerns against all fourteen layers. Every contested technology choice has a verdict in [the decision catalog](https://www.agenticarchitectureskills.com/decisions).

**The research behind this page**

* [Master target-state architecture](https://www.agenticarchitectureskills.com/library/architecture/master-target-state)
* [Vision and target state](https://www.agenticarchitectureskills.com/library/architecture/vision-and-target-state)
* [The concerns-by-layers matrix](https://www.agenticarchitectureskills.com/library/architecture/concerns-by-layers-matrix)
