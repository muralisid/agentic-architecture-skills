# Observability and FinOps

How to see what every agent did, test every change before it spreads, and keep every agent's spending inside a limit its business sponsor owns.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops (Markdown: https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops.md)
Updated: 2026-08-23
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

> **In plain terms.**
>
> This page covers how the organisation watches its AI agents: what each one did, step by step, what it cost, and whether a change made it better or worse. It matters because an agent that is not measured cannot be trusted with more work, and an agent without a spending limit can run up a large bill. The one thing to remember: every agent needs a record it cannot alter, a test before any change spreads, and a spending limit owned by a named sponsor.

## Target state

**In short:** Every agent is watched end to end, every change is tested before it spreads, and spending stays inside a sponsor-owned limit.

Agents are managed as traced actors with unit economics, not as services with uptime. Every agent is traced end to end: the session, each model call, each tool call, and the cost. The trace uses a standards-based vocabulary. It sits behind a translation layer, because the vocabulary itself is still moving. Offline and online evals (test suites with known right answers) gate every behaviour change, with calibrated judges and staged rollouts. Every agent runs inside a budget envelope owned by its business sponsor. Hard caps and anomaly alerts back that envelope, and the caps are deterministic: fixed rules, not model judgement. Quality service-level objectives (SLOs) for session success, containment, and escalation are tracked per release. The licensed estate and the metered estate (the two estates) report into one cost and usage view. When a budget runs out, the work falls to a human queue. An observability outage never blinds the kill switch. This layer is the measurement plane of the agentic enterprise and the raw material of its learning flywheel.

**Figure: Traces the agent cannot forge.** Every agent is traced end to end on a translation layer over unstable conventions; budgets are enforced deterministically, and telemetry collection sits outside the agent's control.

Session, model-call, and tool-call spans keyed to agent identity and cost.

**What the diagram shows:** Observability architecture from agent execution through out-of-band collection, a schema translation layer, trace storage with cost attribution, budget enforcement returning errors on exhaustion, and the change-gate pipeline. The map contains Agent execution; Out-of-band collection: Agents cannot forge their own traces; Translation layer: Conventions unstable; avoid deep SDK coupling; Traces + cost: Session, model, tool spans keyed to agent identity; Budget enforcement: Hierarchical caps; 429 on exhaustion; fail to human queues; Change gates: Shadow, 1-5% canary, full; judges calibrated. Its connections are agent to collect; collect to translate; translate to traces; budget to agent for caps per run; traces to gates for gate evidence. Important boundary: An observability outage must not blind the kill switch.

Diagram: https\://www\.agenticarchitectureskills.com/figures/layer-12-hero.svg

| Component                           | Responsibility                                                                                                                                  | Control it hosts                                                                                                          | Where it runs                                                               |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| Instrumentation + translation layer | Emit session, model-call, and tool-call spans in the OpenTelemetry (OTel) generative AI (GenAI) vocabulary; shield backends from schema changes | Schema mapping; redaction at capture; classification tagging                                                              | Agent runtimes and harnesses, software development kit (SDK) plus collector |
| Trace backend                       | Store and correlate traces as operations data, evidence, and eval raw material                                                                  | Access control on traces that contain prompts; retention, integrity, residency                                            | Application performance monitoring (APM) estate or eval-capable platform    |
| Eval service                        | Offline and online evals; judge pool with calibration sets                                                                                      | Change gates; judge-calibration currency; dataset curation from traces                                                    | Continuous integration (CI) plus production sampling                        |
| Rollout controller                  | Shadow, canary, then full rollout of agent changes                                                                                              | Canary gates (session success, satisfaction, escalation); flags that separate activation from deployment                  | Delivery pipeline and runtime flags                                         |
| Budget enforcement                  | Deterministic spend control per invocation and per principal                                                                                    | Hard caps (iterations, timeout, tokens); hierarchical budgets returning HTTP 429 (too many requests); fail to human queue | Large language model (LLM) gateway and agent harness                        |
| FinOps plane                        | Metering, showback maturing to chargeback, anomaly detection                                                                                    | Sponsor envelopes; allocation based on the FinOps Open Cost and Usage Specification (FOCUS); variance alerts              | Cloud cost tooling plus FinOps practice                                     |
| Two-estate bridge                   | One usage and cost view across licensed and metered estates                                                                                     | Visibility-lag tracking; gap register for licensed analytics application programming interfaces (APIs)                    | Vendor admin and analytics APIs feeding the FinOps plane                    |

## Mechanisms

### The telemetry contract is not stable

**In short:** The shared language for describing agent activity is still changing, so keep a buffer between recording and storage.

OpenTelemetry GenAI semantic conventions are the right vocabulary, and not yet a stable one. As of August 2026 every GenAI convention remains in **Development status**. The whole set was moved out of the main semantic-conventions repository (**v1.42.0, June 12, 2026**) into a dedicated **open-telemetry/semantic-conventions-genai** repository. That repository had **no tagged release** by mid-July. Agent spans and Model Context Protocol (MCP) conventions exist (v1.39 era) and are what to emit. **OpenInference and OpenLLMetry still compete** as instrumentation schemes. The architectural consequence is standing: emit telemetry as if the schema will change. Keep a **translation layer** as an explicit boundary between instrumentation and backend. Avoid deep coupling to any proprietary SDK you may want to leave. "Just extend APM on standard telemetry" carries schema-churn risk; the translation layer is what makes either path survivable.

### Trace topology and its obligations

**In short:** Each agent run leaves a step-by-step record the agent cannot alter; that record is both audit evidence and personal data.

The trace is a **session span** containing **model-call spans** and **tool-call spans**. Tokens and cost are attributed on every span. The whole tree is **keyed to the agent's identity**; that key is what makes per-agent cost attribution and the audit trail possible. Traces are dual-classified the moment they exist. Spans that carry prompts and outputs are **evidence** for the [governance layer](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty). The same spans are **personal data** under the [erasure mechanics](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering). So retention, redaction, and residency rules ride the pipeline, and telemetry inherits the source classification of what it captured. Collection sits **outside the agent's control**. Agents cannot forge or suppress their own traces, which is what makes telemetry usable as evidence. One resilience rule is non-negotiable: an **observability outage must not blind the kill switch**. The stop path never depends on the measurement path.

### Budget enforcement, deterministic

**In short:** Spending limits are enforced by fixed rules at three levels, and when money runs out the work goes to a person.

Budget enforcement is a deterministic control, not a model behaviour, and it ships in three tiers. The first tier is per-invocation hard caps on the harness (the engineering shell around the model). AgentCore ships **maxIterations (default 75)**, **timeout (default 3600 seconds)**, and **maxTokens**, all carrying cost-allocation tags \[vendor]. The second tier is **hierarchical budgets** at the gateway, set per key, user, team, and organisation. These **return HTTP 429 on exhaustion**; LiteLLM is the dominant open-source pattern. The third tier is control-plane billing policies. Agent 365 ships **Agent Billing Policies** with budget limits and threshold alerts (November 2025). Agentforce **Digital Wallet** drills down to agent, action, and channel at **$0.10 per action** \[vendor pricing]. **Copilot Credits are priced at $0.01** \[vendor pricing]. Above the caps sit the sponsor envelope and anomaly detection. Budget-exhaustion behaviour is defined before autonomy is granted: the agent **fails to a human queue**, it does not silently retry.

### The change gate

**In short:** No behaviour change reaches all users at once; it is tested offline, shadowed, then tried on a small slice of traffic.

No agent behaviour change reaches full traffic ungated. The published pattern comes from arXiv 2606.08867, the 100M-user support-agent deployment. It runs offline evals first, then shadow traffic, then a canary on **1 to 5 percent of traffic**, then full rollout. The canary is **gated on session success, satisfaction (transactional Net Promoter Score, tNPS), and escalation rate**. **Feature flags decouple activation from deployment**, so rollback is a flag flip, not a redeploy. Escalation has a published healthy band of **5 to 15 percent**, tracked per release alongside session success and containment. Guardrail metrics alert in both directions: a **block-rate spike signals attack, and a block-rate drop signals misconfiguration** (Bedrock Guardrails CloudWatch metrics \[vendor]). The pattern's weight got priced: OpenAI bought Statsig, a flags-and-experimentation company, for **$1.1B** (September 2025). One honest gap remains. No published enterprise error-budget analogue for agent quality SLOs exists; this guide carries it as an open pattern.

### Judge governance

**In short:** When an AI model grades other AI output, the grader itself must be checked against human judgement on a schedule.

Online evals mostly mean LLM judges, and the judges need governance of their own. The 2025 to 2026 reliability findings are consistent. Judge models **agree with themselves more than they measure the right thing** (arXiv 2606.19544). They run overconfident (arXiv 2508.06225). They **drift silently on hosted endpoints** when the underlying model is updated without notice. The discipline is a loop. Production traces feed eval datasets; judges score them; **human-labelled calibration sets** check the judges; calibration is re-validated on a schedule (GoDaddy published this workflow, November 2025). The adoption gap is the risk. Among agent teams, **89 percent** have some observability, **52 percent** run evals at all, and **37.3 percent** run them online (LangChain, December 2025 \[vendor]).

### Failure signatures and the cost numbers

**In short:** The typical cost disaster is an agent stuck in a loop, and the number to manage is cost per solved case.

The signature failures are runaway loops and retry storms. The incident record holds a self-reported **$1.3 million incident that burned 603 billion tokens** in a multi-agent loop (May 2026, medium confidence). It also holds a **$47K** agent-to-agent ping-pong loop (vendor blog, low confidence, unverified). The systemic figure behind them: **60 percent of LLM call errors are rate-limit driven** (Datadog telemetry \[vendor]). Retry storms are therefore an ecosystem-wide operations problem, not an anecdote. Consumption is structurally volatile. **Tokens per request doubled year over year at the median and quadrupled for heavy users** \[vendor telemetry]. That is why spend can rise while unit prices fall, and why cost per outcome, not raw spend, is the number to manage. Outcome anchors exist: **$0.99 to $2.00 per automated resolution** \[vendor pricing], against a **$6 to $12** human-handled comparator. Where outcomes are not priced, action and credit metering supplies the unit. The ownership numbers say who is exposed. In the Harness 2026 survey \[vendor survey], **52 percent report no clear AI cost owner** and **an estimated 26 percent of AI spend is wasted**. In the same survey, **72 percent saw an unexpected spike** in the past year. Separately, **98 percent of FinOps practitioners now manage AI spend, up from 63 percent** a year earlier (State of FinOps 2026).

### Bridging the two estates

**In short:** Agent costs arrive from per-seat licences and from pay-per-use meters, and the aim is one combined view of both.

Cost and usage live in two estates: the licensed estate (per-seat copilots) and the metered estate (token- and action-priced agents). The target is one view. The licensed side exposes analytics APIs with documented gaps. Microsoft Graph Copilot usage APIs reached general availability (GA) in October 2025. They **omit unlicensed Copilot Chat activity and refresh on a roughly 48-hour lag**. Salesforce Digital Wallet reports in near real time. Anthropic ships an **Admin Usage and Cost API plus an Enterprise Analytics API**. Agents-console products bridge third-party agents into the same pane \[vendor]. On allocation, **splitting the cost of a shared model is the acknowledged hard problem**. **FOCUS 1.3 split-cost allocation** is the specification-side answer, with the Tokenomics Foundation collaborating on token-cost normalisation. The estates are also merging organisationally: **90 percent of FinOps teams now manage software-as-a-service (SaaS) spend** as well.

## Design decisions

* **Extend APM with OTel GenAI vs dedicated LLM observability** ([CD-15](https://www.agenticarchitectureskills.com/decisions#cd-15), the choice between extending existing monitoring tools and buying a specialist AI monitoring product): the question dissolved. In twelve months the specialists were largely absorbed. Dynatrace agreed to acquire Arize for $915M (announced August 13, 2026, not closed at research time). ClickHouse acquired Langfuse (January 2026, MIT license retained). Cisco folded Galileo into Splunk (May 2026). CoreWeave took Weights & Biases (2025). LangSmith and Braintrust remain independent. Choose on the surviving fault lines: **OTel-native pipeline vs proprietary SDK**, **eval-loop depth vs infrastructure correlation**, and **self-hosting requirements**. Either telemetry path needs the translation layer. The open-source option now belongs to a database vendor but keeps its license. Most enterprises land on the APM incumbent for correlation plus one eval-capable tool for the loop. The merged-category trend suggests even that seam closes.
* **Per-agent cost ownership**: a **sponsor-owned budget envelope** per agent, with unit-economics targets and variance alerting. Showback first (reporting each agent's cost to its owner), maturing to chargeback (billing the owner) where allocation is clean. Central funding is retained for the shared platform layer. "Salary-like" is deliberately rejected: consumption is too volatile for a fixed-line analogy. The sponsor construct is productised. Identity platforms carry a literal sponsor role with automatic transfer on departure. Workforce systems took per-agent budgeting to GA in February 2026, with thin shipped mechanics and no named customer. Control planes ship billing policies. Even so, no enterprise has published running per-agent budgets in production as of August 2026. This is a recommended design, not established practice.

## Cross-cutting concerns

| #   | Concern                | Treatment at this layer                                                                                             |
| --- | ---------------------- | ------------------------------------------------------------------------------------------------------------------- |
| C1  | Identity and access    | Trace access is controlled (traces contain prompts and data); per-agent cost attribution is keyed to agent identity |
| C2  | Observability          | The layer itself; coverage metrics; two-estate bridging                                                             |
| C3  | Traceability and audit | Traces as evidence artifacts; retention and integrity; span-level linkage from answer to source                     |
| C4  | Grounding              | Eval datasets curated from production traces; judge calibration against human labels                                |
| C5  | Impersonation          | Telemetry authenticity: collection outside the agent's control; agents cannot forge their own traces                |
| C6  | Sovereignty            | Telemetry residency inherits the source classification; backend location in scope                                   |
| C7  | Privacy                | Prompt and output redaction in traces; erasure cascades include telemetry                                           |
| C8  | Safety and oversight   | Canary gates with human review; guardrail alerts in both directions; kill-switch integration                        |
| C9  | Cost                   | The layer's core: envelopes, caps, showback to chargeback, anomaly detection, cost per outcome                      |
| C10 | Resilience             | Budget-exhaustion behaviour defined (fail to human queues); an observability outage does not blind the kill switch  |

## Evidence and limits

The incident record here is cost incidents, not Common Vulnerabilities and Exposures (CVE) entries, and it is graded. The $1.3 million, 603 billion token loop is self-reported (May 2026, medium confidence). The $47K agent-to-agent (A2A) loop traces only to a vendor blog (low confidence, unverified) and stays flagged until a primary source exists. Survey and telemetry figures are vendor-published and marked so throughout (LangChain, Harness, Datadog). The Harness cost figures are paired with FinOps Foundation State of FinOps data for neutrality. Every pricing anchor ($0.10 per action, $0.01 credits, $0.99 to $2.00 per resolution) is a vendor list price. The sponsor-owned envelope is the authors' recommended design, not established practice. The error-budget analogue for agent quality has no published enterprise example. One refusal: a spring 2026 funding round attributed to the open-source tracing project circulates on content-farm sites. It contradicts the verified January 2026 acquisition, so this guide excludes it and treats that class of aggregator source as unreliable generally. Four items to re-verify quarterly. The first, and the single most important item on this layer, is the semantic-conventions-genai repository's first tagged release and stability status. The others are the Dynatrace-Arize close and the fate of the Phoenix open-source project, the shipped depth of workforce-system agent budgeting, and agents-console GA states.

**The research behind this page**

* [Observability and FinOps findings](https://www.agenticarchitectureskills.com/library/layers/r12-observability-and-finops/findings)
* [Sources](https://www.agenticarchitectureskills.com/library/layers/r12-observability-and-finops/sources)
* [Products named for orientation](https://www.agenticarchitectureskills.com/architecture), on the one-page wall chart
