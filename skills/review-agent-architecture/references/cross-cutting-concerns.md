# The concern matrix

Ten requirements every layer must honour, such as identity, privacy and cost. For each one: which layer owns it, which layer stops a violation, and the six gaps with no complete answer yet.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/architecture/concern-matrix (Markdown: https://www.agenticarchitectureskills.com/architecture/concern-matrix.md)
Updated: 2026-10-15
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

Some requirements belong to no single team: knowing who did what, protecting personal data, controlling cost. The concern matrix lists ten of them. They are the cross-cutting concerns that every layer must honour. For each one, the matrix names where the rule is owned and where a violation is actually stopped. Most failures happen in the hand-off between the two. A requirement passes from one part of the system to the next and is quietly weakened.

## How to read it

A layer is one of [the fourteen layers](https://www.agenticarchitectureskills.com/layers) of systems a company runs and agents touch. Each layer page ends with its own row for the ten concerns, C1 to C10. This page shows them side by side. Three words carry the meaning.

* **Owned** means the layer defines the requirement and answers for it.
* **Enforced** means the place where a violation is actually stopped. That is often a different layer.
* **Inherited** means the layer must pass the requirement on without weakening it. Most defects live here, because a weakened requirement fails silently.

The matrix applies at every autonomy level on [the autonomy contract](https://www.agenticarchitectureskills.com/architecture/autonomy-contract). It tightens as autonomy rises.

**Figure: Cross-cutting concerns need named homes.** A concern that appears everywhere but is owned nowhere becomes a gap.

The full accessible table remains the source of record beneath this orientation view.

**What the diagram shows:** Heatmap concept showing identity, provenance, cost, evaluation, sovereignty, reversibility, and human oversight crossing all fourteen enterprise layers. The matrix crosses Identity, Provenance, Evaluation, Cost, Sovereignty, Reversibility, Human oversight with Runtime, Data, Action, Records, Channels, Governance. Annotated cells are Identity by Action: Primary enforcement; Provenance by Data: Attach at parse time; Evaluation by Runtime: Pre-release gate; Cost by Runtime: Per-run budget; Sovereignty by Data: Classification route; Reversibility by Records: Compensating action; Human oversight by Governance: Named accountability.

Diagram: https\://www\.agenticarchitectureskills.com/figures/concerns-layer-heatmap.svg

## Owned and enforced

| #   | Concern                        | Owned at                                                                                                                   | Enforced at                                                                                                                                                                                                                                                                                                                                                             | What goes wrong when this is missed                                                                   |
| --- | ------------------------------ | -------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| C1  | Identity and access            | [Security and identity (R10)](https://www.agenticarchitectureskills.com/layers/r10-security-and-identity)                  | The gateway in the [integration fabric (R03)](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric). Entitlements in [systems of record (R04)](https://www.agenticarchitectureskills.com/layers/r04-systems-of-record). Workload identity in [infrastructure and compute (R01)](https://www.agenticarchitectureskills.com/layers/r01-infrastructure) | Identity is claimed but never checked where the action happens                                        |
| C2  | Observability                  | [Observability and FinOps (R12)](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops)            | Every layer emits it. Observability and FinOps (R12) gathers it                                                                                                                                                                                                                                                                                                         | Vendor-embedded agents report to their own consoles, so coverage only looks complete                  |
| C3  | Traceability and audit         | [Governance, risk and sovereignty (R11)](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty) | Collection in observability and FinOps (R12). Provenance at parse time in [agent data engineering (R14)](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering)                                                                                                                                                                                   | Evidence is rebuilt after the incident instead of recorded as the work happens                        |
| C4  | Grounding                      | [Data platform (R02)](https://www.agenticarchitectureskills.com/layers/r02-data-platform). Agent data engineering (R14)    | [Experience and channels (R09)](https://www.agenticarchitectureskills.com/layers/r09-experience-and-channels), the strictest bar for customers. [Line of business and OT (R05)](https://www.agenticarchitectureskills.com/layers/r05-lob-and-ot), checked against a digital twin                                                                                        | The agent answers from weak evidence instead of refusing                                              |
| C5  | Impersonation and authenticity | Security and identity (R10)                                                                                                | Tool server identity in the integration fabric (R03). Disclosure in [productivity and collaboration (R08)](https://www.agenticarchitectureskills.com/layers/r08-productivity-and-collaboration) and experience and channels (R09)                                                                                                                                       | People trust an agent they take for a person or a known system                                        |
| C6  | Sovereignty and residency      | Governance, risk and sovereignty (R11)                                                                                     | Model serving in infrastructure and compute (R01). Indexes in the data platform (R02) and agent data engineering (R14). Routing in the integration fabric (R03)                                                                                                                                                                                                         | Data stays in the right country at the source, then leaves in an embedding, a trace or a session file |
| C7  | Privacy                        | Governance, risk and sovereignty (R11)                                                                                     | Deletion of every copy in agent data engineering (R14). Index scope in the data platform (R02). Trace redaction in observability and FinOps (R12)                                                                                                                                                                                                                       | Deletion works in the record and fails in the vectors, memories and logs                              |
| C8  | Safety and oversight           | [Operating model and supervision (R13)](https://www.agenticarchitectureskills.com/layers/r13-operating-model)              | The gateway kill switch in the integration fabric (R03). Harness caps in the [agent platform (R07)](https://www.agenticarchitectureskills.com/layers/r07-agent-platform). Operator authority in line of business and OT (R05)                                                                                                                                           | Oversight sits on the org chart but not in the running system                                         |
| C9  | Cost                           | Observability and FinOps (R12)                                                                                             | Per-run budgets in the agent platform (R07). Rate limits in the integration fabric (R03)                                                                                                                                                                                                                                                                                | Spend is charged to a platform, not a sponsor, and supervision work is left out of the case           |
| C10 | Resilience                     | Infrastructure and compute (R01)                                                                                           | Every layer's fallback mode. What happens when a budget runs out, in observability and FinOps (R12)                                                                                                                                                                                                                                                                     | Fallbacks are designed layer by layer and never tested end to end                                     |

## Seven rules that always hold

Seven rules came up on their own in three or more layers. So they are treated as rules that must always hold, not as recommendations.

1. **A derived copy takes the strictest label of its sources.** That includes chunks, embeddings, session files, traces and fine-tuned model weights.
2. **A deletion reaches every copy, or it did not happen.** When a record is deleted, so are its vectors, memories, traces, logs, eval datasets and other copies. [The data-to-memory pipeline](https://www.agenticarchitectureskills.com/architecture/data-to-memory) shows how.
3. **Every layer falls back to a human queue.** Containment means conversations that never reach a person. It is never raised by making the human queue unavailable.
4. **Logs are collected outside the agent's control.** A log the agent can change is not proof.
5. **The kill switch works from several points.** It sits in the runtime, the gateway, the harness and the identity system. An outage in monitoring must not disable it.
6. **Enforcement is fixed rules, outside the model.** Rules may be written in the harness. They are enforced at the gateway or the policy decision point, as set out in [enforcement outside the model](https://www.agenticarchitectureskills.com/architecture/enforcement).
7. **Provenance travels inside the item.** It is attached at parse time, when the document is first read. Provenance stored separately falls out of step when it matters.

## Six open gaps

These problems have no complete published answer yet. The status is as of August 2026.

| Gap                                                                      | Layer                                  | Status                                                                                                              |
| ------------------------------------------------------------------------ | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Permissions on a copy built from many sources                            | Agent data engineering (R14)           | No complete published solution. Giving the copy only the permissions all its sources share is the emerging practice |
| A normal-behaviour baseline for agents in the security operations centre | Security and identity (R10)            | Unsolved. Agent behaviour varies for good reasons, so baselines built for people or for software both misfire       |
| Incident reporting when several agents contribute                        | Governance, risk and sovereignty (R11) | No agreed way exists to decide who reports what                                                                     |
| Error budgets for agent quality                                          | Observability and FinOps (R12)         | No published enterprise example. An open pattern, not a practice                                                    |
| Span of control: how many agents one person can supervise                | Operating model and supervision (R13)  | No credible published figure from any source                                                                        |
| Embedded versus external agent results                                   | Systems of record (R04)                | No published side-by-side measurement on the same tasks                                                             |

## A worked example: erasing a customer at a utility

A former customer asks a utility to erase their personal data, where the law allows. The privacy rule is owned by governance, risk and sovereignty (R11). The deletion starts in the customer record system. Agent data engineering (R14) must carry it to the search index, the agents' memories and their traces. Observability and FinOps (R12) must remove the person from stored traces. If one hand-off is missed, the record is gone, but an agent can still answer questions about the customer.

## Evidence and limits

The matrix comes from the fourteen layer research tracks. Each of the seven rules surfaced on its own in three or more layers. That is agreement between tracks, not a measured outcome. The gaps are dated August 2026, and some may have published answers since.

## Next step

Run the agent day to day, starting with [observability and FinOps](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops).

**Explore this topic**

* [The concerns-by-layers matrix](https://www.agenticarchitectureskills.com/library/architecture/concerns-by-layers-matrix)
* [All fourteen research tracks](https://www.agenticarchitectureskills.com/library/layers)
