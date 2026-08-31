# The fourteen layers

One page for each of the fourteen parts of the enterprise estate that agents touch: what good looks like, how it is built, the choices made, and what the evidence supports.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/layers (Markdown: https://www.agenticarchitectureskills.com/layers.md)
Updated: 2026-08-31
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

> **In plain terms.**
>
> This section walks through the fourteen parts of a company's technology estate that agents will touch, from the servers they run on to the people who supervise them. Each page says what good looks like, how it is built, which popular choices were challenged, and where the evidence runs out. The one thing to remember: the fourteen layers are what you already own, and the seven planes are what you build across them.

**Figure: Layers are what you own; planes are what you build across them.** The fourteen layers are recognisable parts of the enterprise estate. The seven planes coordinate capabilities across several of those layers, so a deployed agent workload never belongs to just one box.

**What the image shows:** A fourteen-floor enterprise building is crossed by seven end-to-end agent-system planes: execution, action, knowledge, control, improvement, evidence and human.

Image: https\://www\.agenticarchitectureskills.com/images/layers/layers-vs-planes-labeled-v1.webp

The estate you already own has fourteen layers. The agent system you build across it has [seven planes](https://www.agenticarchitectureskills.com/architecture). Each page below covers one layer in five parts. First, the target state: the architecture to aim for. Second, the mechanisms that implement it, with their exact protocols and measured numbers. Third, the contested choices, each with a verdict. Fourth, the layer's cross-cutting concern row: the requirements every layer must honour, such as identity, privacy, and cost. Fifth, what the evidence does not support.

**Figure: The fourteen layers grouped by the job they do.** This map is the quickest way to find a page. Start with the job you are trying to understand, then choose the layer within that group. Real workloads touch several groups at once.

**What the image shows:** The fourteen enterprise layers are grouped into execution and platform, action, knowledge, control and evidence, improvement, and human-facing surfaces.

Image: https\://www\.agenticarchitectureskills.com/images/layers/fourteen-layers-map-labeled-v1.webp

**Figure: Fourteen estate layers, seven agent-system planes.** Layers describe what the enterprise owns; planes describe how governed agent work operates across it.

A layer can contribute to more than one plane; the planes cut across the estate rather than containing its layers.

**What the diagram shows:** Crosswalk matrix showing fourteen enduring enterprise layers down the rows and seven agent-system planes across the columns, with several layers contributing to multiple planes. The matrix crosses R01 Infrastructure, R02 Data platform, R03 Integration fabric, R04 Systems of record, R05 LOB and OT, R06 Intelligence and learning, R07 Agent platform, R08 Productivity and collaboration, R09 Experience and channels, R10 Security and identity, R11 Governance, risk and sovereignty, R12 Observability and FinOps, R13 Operating model, R14 Agent data engineering with Execution, Action, Knowledge, Control, Improvement, Evidence, Human. Annotated cells are R01 Infrastructure by Execution: Runtime and model serving; R02 Data platform by Knowledge: Governed source data; R03 Integration fabric by Action: Gateway and tool path; R04 Systems of record by Action: Authoritative action boundary; R05 LOB and OT by Action: Operational actuation boundary; R06 Intelligence and learning by Improvement: Evaluation and promotion; R07 Agent platform by Execution: Agent runtime; R07 Agent platform by Control: Registry and runtime controls; R08 Productivity and collaboration by Human: Human work surface; R09 Experience and channels by Human: Customer and employee edge; R10 Security and identity by Control: Identity and policy; R11 Governance, risk and sovereignty by Control: Risk and sovereignty rules; R11 Governance, risk and sovereignty by Evidence: Decision and consultation records; R12 Observability and FinOps by Evidence: Independent traces and cost; R13 Operating model by Human: Accountability and supervision; R14 Agent data engineering by Knowledge: Curation and memory; R14 Agent data engineering by Improvement: Eval-data flywheel. Important boundary: The cells show primary contributions, not exclusive ownership. Every deployed workload uses all seven planes across the relevant estate layers.

Diagram: https\://www\.agenticarchitectureskills.com/figures/layers-planes-crosswalk.svg

## Execution and platform

| Layer                                                                                                 | Target state in one line                                                                                                                          |
| ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| [R01 Infrastructure and compute](https://www.agenticarchitectureskills.com/layers/r01-infrastructure) | Per-session isolation, microVM sandboxes behind egress proxies for act-capable work, first-class workload identity, classification-routed serving |
| [R07 Agent platform](https://www.agenticarchitectureskills.com/layers/r07-agent-platform)             | Buy the runtime, build the harness: explicit termination, artifacts-as-state, separate verification, registry with eval-gated promotion           |

## Action

| Layer                                                                                             | Target state in one line                                                                                         |
| ------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| [R03 Integration fabric](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric) | A governed tool plane with one gateway as the enforcement point for identity, credentials, inspection, and audit |
| [R04 Systems of record](https://www.agenticarchitectureskills.com/layers/r04-systems-of-record)   | Wrap, do not reinvent: agents act as the requesting user, entitlement stays in the record system                 |
| [R05 Line of business and OT](https://www.agenticarchitectureskills.com/layers/r05-lob-and-ot)    | Agents on the information path, never the control path, behind a validated presentation layer                    |

## Knowledge

| Layer                                                                                                     | Target state in one line                                                                                                            |
| --------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| [R02 Data platform](https://www.agenticarchitectureskills.com/layers/r02-data-platform)                   | Grounding as a governed product: permission-aware indexes, pre-filtered retrieval, semantic contracts where determinism is required |
| [R14 Agent data engineering](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering) | A curation pipeline with named ownership, provenance from parse time, governed memory writes, cascading erasure                     |

## Control and evidence

| Layer                                                                                                                    | Target state in one line                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------- |
| [R10 Security and identity](https://www.agenticarchitectureskills.com/layers/r10-security-and-identity)                  | Registered least-privileged identities and a deterministic policy decision point on every consequential action |
| [R11 Governance, risk and sovereignty](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty) | The registry as compliance inventory, a two-tier evidence posture, classification-routed deployment            |
| [R12 Observability and FinOps](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops)            | End-to-end traces the agent cannot forge, on a translation layer, with deterministic budget enforcement        |

## Improvement

| Layer                                                                                                           | Target state in one line                                                                               |
| --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| [R06 Intelligence and learning](https://www.agenticarchitectureskills.com/layers/r06-intelligence-and-learning) | Expert-owned evals, calibrated judges, promotion gated on counterexample survival with a demotion path |

## Human-facing surfaces

| Layer                                                                                                                     | Target state in one line                                                                          |
| ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| [R08 Productivity and collaboration](https://www.agenticarchitectureskills.com/layers/r08-productivity-and-collaboration) | Access identity as the universal default, presence granted per capability surface and rarely      |
| [R09 Experience and channels](https://www.agenticarchitectureskills.com/layers/r09-experience-and-channels)               | A separate customer-facing edge on a shared control plane, justified by legal exposure            |
| [R13 Supervision and oversight](https://www.agenticarchitectureskills.com/layers/r13-operating-model)                     | Supervision as a queueing system: capacity with wait time included, load budgeted as a burst rate |

## How the pages are built

**Figure: Every layer page follows the same five-step reading path.** Begin with the target picture, learn the mechanisms, inspect the contested choices, check the concerns that every layer must honour, and finish by testing the recommendation against the evidence and its limits.

**What the image shows:** Five numbered stations show target state, mechanisms, design decisions, cross-cutting concerns, and evidence and limits.

Image: https\://www\.agenticarchitectureskills.com/images/layers/layer-page-reading-guide-labeled-v1.webp

Each page condenses one research track. The tracks, with their findings and dated sources, are in [the research library](https://www.agenticarchitectureskills.com/library/layers). Where the evidence does not support a claim, the page says so and names the refusal. The [decision catalog](https://www.agenticarchitectureskills.com/decisions) carries every contested choice, with its verdict and the discriminator: the one test that separates the options.
