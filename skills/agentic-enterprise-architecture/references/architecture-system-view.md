# What an agent platform provides

The seven capabilities that must exist before agents can run safely at scale, the layers that build them, and the lifecycle stages that call on them.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/architecture/system-view (Markdown: https://www.agenticarchitectureskills.com/architecture/system-view.md)
Updated: 2026-10-15
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

An agent does not live inside one AI model. To finish a task, it reaches into identity, data, applications, tools, records and people. So what must exist before agents can run safely at scale? Seven capabilities. Three let agents work: a runtime, a tool gateway, and [knowledge and memory](https://www.agenticarchitectureskills.com/memory). Four keep them in bounds: identity and policy, evaluation and release, observability and an audit trail, and human oversight. You build them across [the fourteen layers](https://www.agenticarchitectureskills.com/layers) you already own. Each stage of [the agent lifecycle](https://www.agenticarchitectureskills.com/architecture/agent-lifecycle) calls on some of them. Two rules hold them together. [Policy is enforced outside the model](https://www.agenticarchitectureskills.com/architecture/enforcement). The audit trail is written where the agent cannot touch it.

**Figure: Layers you own, a lifecycle you run, capabilities you add.** The layers are what you own. The capabilities are what you add across them. Each lifecycle stage calls on the capabilities it needs.

**What the image shows:** On the left, a building of fourteen floors shows the layers you own. They run from infrastructure and compute (R01) at the bottom to agent data engineering (R14) at the top. In the centre, seven bands show the capabilities you add. Each band names the industry products and the layers that build it. The runtime is built from R01 and R07. The tool gateway is built from R03, R04 and R05. Knowledge and memory is built from R02 and R14. Identity and policy is built from R10, R11 and R07. Evaluation and release is built from R06 and R12. Observability and audit trail is built from R12 and R11. Human oversight is built from R13, R08 and R09. On the right, the nine lifecycle stages run in order, and each change loops back to evaluate. Lines link each stage to the capabilities it calls on. Register, entitle and retire call on identity and policy. Sponsor and owner calls on human oversight. Evaluate and change call on evaluation and release. Approve calls on human oversight and on identity and policy. Operate calls on the runtime, the tool gateway, knowledge and memory, and observability. Periodic review calls on observability and on human oversight. A strip at the bottom gives the two rules. Policy is enforced outside the model. The audit trail is written where the agent cannot touch it.

Image: https\://www\.agenticarchitectureskills.com/figures/architecture/layers-lifecycle-capabilities.svg

## The seven capabilities

The industry already has names for six of the seven. AWS, Microsoft and Google sell them as separate products. The grouping into seven is this guide's own. It lets you point each capability at a product you may already buy. Human oversight is the one no vendor sells. It comes from regulation and from how you organise people.

**Figure: The seven capabilities of an agent platform.** Policy is enforced outside the model, and the audit trail is written where the agent cannot touch it.

The same seven capabilities apply to every kind of enterprise; what fills them and who runs them differ.

**What the diagram shows:** Seven horizontal bands for the runtime, the tool gateway, knowledge and memory, identity and policy, evaluation and release, observability and audit trail, and human oversight, connected by policy and trace flows. The map contains Runtime: Sandboxes, sessions, model serving; Tool gateway: One gateway, governed tools; Knowledge and memory: Curated sources and memory; Identity and policy: Identity, policy decisions, registry, budgets; Evaluation and release: Evaluations, promotion, rollback; Observability and audit trail: Traces the agent cannot write; Human oversight: Intent, accountability, exceptions. Its connections are human to control for intent and mandate; control to action for deterministic permission; execution to action for tool request; action to evidence for immutable trace; evidence to improvement for evaluation input.

Diagram: https\://www\.agenticarchitectureskills.com/figures/seven-plane-architecture.svg

### Runtime

The runtime is where agents run. It holds the sandboxes, the sessions that survive a pause, and model serving. A sandbox is an isolated space where an agent's code and tools run. The [infrastructure and compute layer (R01)](https://www.agenticarchitectureskills.com/layers/r01-infrastructure) and the [agent platform layer (R07)](https://www.agenticarchitectureskills.com/layers/r07-agent-platform) build it. The operate stage calls on it for every run. AWS sells it as AgentCore Runtime. Google calls it Agent Runtime. Microsoft Foundry runs hosted agents on its own Agent Runtime.

### Tool gateway

The tool gateway is how agents reach your systems. Every tool call passes through one gateway, under the agent's own identity. Each tool wraps an existing system behind a governed interface. The gateway also holds the boundary with operational technology (OT), the systems that run physical plant. Agents stay on the information side of that boundary. Three layers build it: [integration fabric (R03)](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric), [systems of record (R04)](https://www.agenticarchitectureskills.com/layers/r04-systems-of-record), and [line of business and OT (R05)](https://www.agenticarchitectureskills.com/layers/r05-lob-and-ot). The operate stage calls on it. AWS sells AgentCore Gateway. It turns existing APIs into Model Context Protocol (MCP) tools. Google sells Agent Gateway. Microsoft Foundry puts tools in Toolboxes behind one managed endpoint. Analysts call the wider category an AI gateway.

### Knowledge and memory

Knowledge and memory is what agents know. It covers governed indexes, sources curated for a purpose, and memory that lasts beyond one task. Each source keeps its permissions. An agent finds only what its user may see. The [data platform layer (R02)](https://www.agenticarchitectureskills.com/layers/r02-data-platform) and the [agent data engineering layer (R14)](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering) build it. The operate stage calls on it whenever an agent needs context. AWS sells AgentCore Memory. Google offers Sessions and Memory Bank. Microsoft's adoption guidance names retrieval and memory as building blocks. [The data-to-memory pipeline](https://www.agenticarchitectureskills.com/architecture/data-to-memory) traces data from its source to a cited answer.

### Identity and policy

Identity and policy decide who the agent is and what it may do. Each agent gets its own identity. A registry lists every agent with its owner, purpose, permissions and live version. A policy decision point says yes or no to each action. Budgets cap what each agent may spend. Three layers build it: [security and identity (R10)](https://www.agenticarchitectureskills.com/layers/r10-security-and-identity), [governance, risk and sovereignty (R11)](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty), and the agent platform (R07). The register, entitle and retire stages call on it. So does approve. It sets the permissions the agent goes live with. [The delegation chain](https://www.agenticarchitectureskills.com/architecture/delegation-chain) traces each action back to the person who asked. AWS sells AgentCore Identity, AgentCore Policy and AWS Agent Registry. Microsoft Entra Agent ID gives each agent its own identity. Microsoft Agent 365 adds a registry and access control across agents.

### Evaluation and release

Evaluation and release is how behaviour changes safely. Evaluations (evals) test each change against a fixed set of cases. Judges score the answers. A judge is a model or a person that grades output against a rubric. A promotion gate decides whether the change ships. Release is staged: a small share of work first, then more. This is a canary release. The [intelligence and learning layer (R06)](https://www.agenticarchitectureskills.com/layers/r06-intelligence-and-learning) and the [observability and FinOps layer (R12)](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops) build it. The evaluate and change stages call on it. AWS sells AgentCore Evaluations and AgentCore Optimization. Google files this work under its Optimize pillar. Microsoft Foundry lists evaluate and optimize steps. [The learning flywheel](https://www.agenticarchitectureskills.com/architecture/learning-flywheel) sets out the gates a change must pass.

### Observability and audit trail

Observability and audit trail is what you can prove afterwards. Traces record each model call, tool call and cost. Provenance records where each piece of information came from. Retention keeps records as long as the law and the business need them. The observability and FinOps layer (R12) and the governance, risk and sovereignty layer (R11) build it. The operate stage writes to it. The periodic review stage reads from it. AWS, Google and Microsoft all ship agent observability. AWS builds its version on OpenTelemetry, the open standard for traces. Every agent keeps an audit trail baseline. High-risk uses also keep the records Article 12 of the EU AI Act asks for.

### Human oversight

Human oversight is who decides and who answers. It covers supervision, the named people accountable for each agent, and the channels people use. Three layers build it: [operating model and supervision (R13)](https://www.agenticarchitectureskills.com/layers/r13-operating-model), [productivity and collaboration (R08)](https://www.agenticarchitectureskills.com/layers/r08-productivity-and-collaboration), and [experience and channels (R09)](https://www.agenticarchitectureskills.com/layers/r09-experience-and-channels). The sponsor and owner, approve and periodic review stages call on it. No vendor sells human oversight as a product. The term comes from Article 14 of the EU AI Act. Microsoft Entra Agent ID requires a sponsor when an agent is created. The sponsor answers for the agent's purpose. [Operate](https://www.agenticarchitectureskills.com/operate) shows how to check that people can keep up.

## The layers behind each capability

Each capability draws on more than one layer. A layer can serve more than one capability. The grid shows every layer against every capability. The [concern matrix](https://www.agenticarchitectureskills.com/architecture/concern-matrix) does the same for the ten cross-cutting concerns. A cross-cutting concern is a need every layer must meet, such as privacy or cost.

**Figure: Fourteen layers you own, seven capabilities you add.** The layers are what the enterprise owns; the seven capabilities are what it adds so governed agent work can run across them.

A layer can contribute to more than one capability; the capabilities cut across the estate rather than containing its layers.

**What the diagram shows:** Crosswalk matrix showing the fourteen enterprise layers down the rows and the seven agent platform capabilities across the columns, with several layers contributing to more than one capability. The matrix crosses R01 Infrastructure, R02 Data platform, R03 Integration fabric, R04 Systems of record, R05 LOB and OT, R06 Intelligence and learning, R07 Agent platform, R08 Productivity and collaboration, R09 Experience and channels, R10 Security and identity, R11 Governance, risk and sovereignty, R12 Observability and FinOps, R13 Operating model, R14 Agent data engineering with Runtime, Tool gateway, Knowledge and memory, Identity and policy, Evaluation and release, Observability and audit trail, Human oversight. Annotated cells are R01 Infrastructure by Runtime: Runtime and model serving; R02 Data platform by Knowledge and memory: Governed source data; R03 Integration fabric by Tool gateway: Gateway and tool path; R04 Systems of record by Tool gateway: Authoritative action boundary; R05 LOB and OT by Tool gateway: Operational actuation boundary; R06 Intelligence and learning by Evaluation and release: Evaluation and promotion; R07 Agent platform by Runtime: Agent runtime; R07 Agent platform by Identity and policy: Registry and runtime controls; R08 Productivity and collaboration by Human oversight: Human work surface; R09 Experience and channels by Human oversight: Customer and employee edge; R10 Security and identity by Identity and policy: Identity and policy; R11 Governance, risk and sovereignty by Identity and policy: Risk and sovereignty rules; R11 Governance, risk and sovereignty by Observability and audit trail: Decision and consultation records; R12 Observability and FinOps by Observability and audit trail: Independent traces and cost; R13 Operating model by Human oversight: Accountability and supervision; R14 Agent data engineering by Knowledge and memory: Curation and memory; R14 Agent data engineering by Evaluation and release: Eval-data flywheel. Important boundary: The cells show primary contributions, not exclusive ownership. Every deployed workload uses all seven capabilities across the relevant layers.

Diagram: https\://www\.agenticarchitectureskills.com/figures/layers-planes-crosswalk.svg

## The two rules

Two rules hold the seven capabilities together. They are also the two most often broken.

**Policy is enforced outside the model.** An instruction in a prompt is a request. A rule becomes a control when a separate system checks it. That system is the gateway and the policy decision point. Both sit outside the agent's runtime. The agent cannot go around them. Models may take permission away, never grant it. In the four [deterministic zones](https://www.agenticarchitectureskills.com/architecture/deterministic-zones), a model may not approve at all. The four are access, money, safety actuation and formal regulatory records. [Enforcement outside the model](https://www.agenticarchitectureskills.com/architecture/enforcement) sets out where each check sits.

**The audit trail is written where the agent cannot touch it.** A log the agent can edit is not proof of what it did. Traces, decisions and provenance go to a store the agent cannot write to. A separate channel collects them as the work happens. Every layer page names where its own checks and records sit.

## One inspection task, seven capabilities

Take an agent that checks vegetation near power lines for an electricity distributor. A person sets the goal: find the spans that need trimming before summer.

1. The runtime starts the agent in a sandbox. It keeps the session if the agent pauses for a photograph.
2. Knowledge and memory supplies the imagery, the asset location and the inspection policy.
3. The tool gateway lets the agent read the asset record and draft a work order.
4. Identity and policy checks each call. The agent may draft a work order. It may not dispatch a crew.
5. Observability and audit trail records each call, each source and each approval.
6. Human oversight puts the draft in front of a planner, who approves or rejects it.
7. Evaluation and release tests any change to the agent before the next season.

This is a design example, not a measured deployment. [The task walkthrough](https://www.agenticarchitectureskills.com/architecture/task-walkthrough) follows a similar task step by step.

## Your own agents and vendor-embedded agents

Not every agent passes through your gateway. Agents you build run through your own runtime and gateway. You can see, budget and trace everything they do. Agents embedded in vendor products run on the vendor's platform. Suite copilots and agents inside record systems are examples. Your gateway never sees them. You govern them through the vendor's tenant settings and the activity data the vendor exports. Those exports have documented gaps.

So every design must work for both kinds of agent. A design that assumes one gateway sees everything is the most common structural error at scale. Cost models need the same care. One vendor prices governance per user, and another includes it \[vendor pricing]. [Agents and packaged applications](https://www.agenticarchitectureskills.com/use-cases/packaged-applications) covers when to wait for the vendor's agent, buy it, or build your own.

**Figure: Your own agents and vendor-embedded agents.** One gateway cannot govern agents that run inside a vendor's platform.

Use tenant policy and telemetry extraction for vendor-embedded agents; direct gateway enforcement for your own agents.

**What the diagram shows:** Two-part architecture comparing vendor-embedded suite agents governed through tenant policy with your own agents governed through an enterprise gateway and a shared audit trail. The comparison contains 2 groups: Vendor-embedded agents, containing Vendor runtime, Tenant policy, Telemetry extraction, Limited gateway visibility; Your own agents, containing Enterprise runtime, Gateway enforcement, Per-run budgets, Full action trace.

Diagram: https\://www\.agenticarchitectureskills.com/figures/support-licensed-metered-estates.svg

## Three kinds of enterprise

The same seven capabilities apply to every enterprise. Who builds them, and in what order, differs.

* **A globally regulated enterprise** runs its own agents and vendor-embedded agents side by side. It keeps one knowledge and memory capability, one registry and one audit trail. Only the enforcement points double: its own gateway, and each vendor's settings.
* **A mid-market company** rents identity and policy from its productivity vendor. It builds knowledge and memory itself. No vendor curates its data for it.
* **A digital-native company** has the runtime and the tool gateway early. It must add identity and policy and an audit trail before autonomy rises. [The autonomy contract](https://www.agenticarchitectureskills.com/architecture/autonomy-contract) holds it to that.

**Figure: One frame, three target architectures.** Use the same seven capabilities, but adapt ownership and controls to the enterprise's real operating capacity.

A global regulated enterprise, a mid-market organisation and a digital native should not build identity and policy the same way.

**What the diagram shows:** Three side-by-side target architectures comparing global regulated, mid-market, and digital-native enterprises across defining constraint, control ownership, and primary gap. The comparison contains 3 groups: Global regulated, containing Own and vendor-embedded agents at the edge, Independent policy and audit trail, Sovereignty routing from day one; Mid-market, containing Identity and policy are rented, Purpose-scoped curation is the build priority, Operate one independent capability at most; Digital native, containing The runtime arrives first, Add policy and the audit trail now, Discipline is the limiting factor.

Diagram: https\://www\.agenticarchitectureskills.com/figures/three-target-architectures.svg

## The estate on one chart

The wall chart shows all fourteen layers on one page. Each layer shows its control point, its key mechanisms and representative products. The ten cross-cutting concerns run as columns. Products are named as of August 2026, for orientation only. They are not endorsements.

**Figure: The agentic enterprise, on one page.** Fourteen layers with their control point, key mechanisms, and the products that serve them, grouped into the seven planes, with the ten cross-cutting concerns as columns and the four deterministic zones underneath.

Diagram: https\://www\.agenticarchitectureskills.com/diagrams/target-state.svg

## Evidence and limits

The capability names come from vendor documentation read on 15 October 2026. Six of the seven match products that two or three large cloud vendors share. The match is strong for the runtime, the gateway, memory, evaluation and observability. Human oversight has no vendor product. Its anchors are the EU AI Act and Microsoft's sponsor and owner model.

The vendors draw some lines differently. Google files its gateway under governance. AWS files its gateway as a tool service. Microsoft sells Agent 365 as one product for registry, access, observability and security. It spans several of the seven.

The grouping into seven is this guide's own. No standards body groups agent platforms this way. Most vendors use three or four groups, such as build, run, govern and optimise. Seven smaller groups let you check each one on its own.

The two rules match industry practice. Google describes its gateway as a policy enforcement point. AWS checks policy on every tool call at its gateway. Article 12 of the EU AI Act asks high-risk systems to record events automatically. Product status changes fast. Check the dated sources below before you rely on a product name.

**Next step:** see the stages in order on [the agent lifecycle](https://www.agenticarchitectureskills.com/architecture/agent-lifecycle), or follow one task on [the task walkthrough](https://www.agenticarchitectureskills.com/architecture/task-walkthrough).

**Explore this topic**

**Guide research**

* [Master target-state architecture](https://www.agenticarchitectureskills.com/library/architecture/master-target-state)
* [Vision and target state](https://www.agenticarchitectureskills.com/library/architecture/vision-and-target-state)
* [The concerns-by-layers matrix](https://www.agenticarchitectureskills.com/library/architecture/concerns-by-layers-matrix)

**What each vendor calls each capability, checked 15 October 2026** \[vendor]

| Capability                    | AWS (Bedrock AgentCore)                                                                                | Microsoft                                                                              | Google (Gemini Enterprise Agent Platform)                                     |
| ----------------------------- | ------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Runtime                       | Runtime. Platform generally available October 2025                                                     | Foundry Agent Runtime, hosted agents                                                   | Agent Runtime, Sessions, Code Execution                                       |
| Tool gateway                  | Gateway, turns APIs into MCP tools                                                                     | Foundry Toolboxes behind one managed MCP endpoint                                      | Agent Gateway, described as a central policy enforcement point for tool calls |
| Knowledge and memory          | Memory, short-term and long-term                                                                       | Retrieval and memory in the Cloud Adoption Framework                                   | Memory Bank, RAG Engine, Vector Search                                        |
| Identity and policy           | Identity; Policy (generally available March 2026); Agent Registry (generally available 31 August 2026) | Entra Agent ID; Agent 365 registry and access control (generally available 1 May 2026) | Agent Identity, Agent Registry, Governance Policies                           |
| Evaluation and release        | Evaluations (generally available March 2026); Optimization (July 2026)                                 | Foundry evaluate and optimize steps                                                    | Agent evaluation, under the Optimize pillar                                   |
| Observability and audit trail | Observability, based on OpenTelemetry                                                                  | Agent 365 audit and logging                                                            | Observability, under the Optimize pillar                                      |
| Human oversight               | No product. The Well-Architected agentic lens asks for human-in-the-loop on critical decisions         | Entra sponsors and owners for each agent                                               | No product                                                                    |

Notes. The AWS per-service dates are the platform date unless a later release note names the service. Google's older Agent Engine overview page now redirects to "Scale your agents". The words "Agent Engine" no longer appear on Google's current pages. Microsoft's five launch functions (registry, access control, visualisation, interoperability, security) come from November 2025 press coverage. Its current pages use three pillars: observe, govern and secure.

**Sources**

* AWS. Amazon Bedrock AgentCore developer guide, [What is Amazon Bedrock AgentCore?](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/what-is-bedrock-agentcore.html), undated, read 15 October 2026. [Release notes](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/release-notes.html), entries July 2025 to October 2026. [Policy and Evaluations preview](https://aws.amazon.com/about-aws/whats-new/2025/12/amazon-bedrock-agentcore-policy-evaluations-preview), 2 December 2025. [AWS Agent Registry generally available](https://aws.amazon.com/about-aws/whats-new/2026/08/aws-agent-registry-generally-available), 31 August 2026. [Well-Architected agentic AI lens, best practice reference](https://docs.aws.amazon.com/wellarchitected/latest/agentic-ai-lens/appendix-a.html), undated.
* Microsoft. [Agent 365 overview](https://learn.microsoft.com/en-us/microsoft-agent-365/overview), updated 19 August 2026. [Agent 365 generally available](https://www.microsoft.com/security/blog/2026/05/01/microsoft-agent-365-now-generally-available-expands-capabilities-and-integrations/), 1 May 2026. [Entra Agent ID: what are agent identities](https://learn.microsoft.com/en-us/entra/agent-id/what-are-agent-identities), updated 15 June 2026. [Entra Agent ID: owners, sponsors and managers](https://learn.microsoft.com/en-us/entra/agent-id/agent-owners-sponsors-managers), updated 3 September 2026. [Foundry Agent Service overview](https://learn.microsoft.com/en-us/azure/foundry/agents/overview), 11 October 2026. [Cloud Adoption Framework: govern and secure AI agents](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ai-agents/governance-security-across-organization), updated 1 October 2026. It asks for policies applied across first-party, custom and third-party agents.
* Google. [Gemini Enterprise Agent Platform overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/overview), updated 13 October 2026. [Scale your agents](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview), updated 13 October 2026.
* Analysts. Gartner Market Guide for AI Gateways, 2025, exact date not verified, via the [Peer Insights category](https://www.gartner.com/reviews/market/ai-gateways).
* Standards and regulation. EU AI Act, Regulation (EU) 2024/1689: [Article 12, record keeping](https://artificialintelligenceact.eu/article/12/) and [Article 14, human oversight](https://artificialintelligenceact.eu/article/14/). OASIS [XACML 3.0](https://docs.oasis-open.org/xacml/3.0/xacml-3.0-core-spec-os-en.html), 22 January 2013, for the policy decision point and the policy enforcement point.
