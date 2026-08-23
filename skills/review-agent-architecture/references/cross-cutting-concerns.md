# The concern matrix

Ten cross-cutting concerns against fourteen layers: who owns each, who enforces it, and the six gaps with no complete answer anywhere.

Source: https://www.agenticarchitectureskills.com/architecture/concern-matrix (Markdown: https://www.agenticarchitectureskills.com/architecture/concern-matrix.md)

> **In plain terms.**
>
> Requirements such as knowing who did what, protecting personal data, and controlling cost apply to every part of the business that agents touch. No single team owns them end to end. This page shows, for each of those requirements, which part of the estate sets the rule and which part actually stops a violation. It also lists the gaps that nobody, anywhere, has fully solved yet. The thing to remember: most failures happen where a requirement is handed from one part of the system to another and quietly weakened on the way.

## How to read it

Every layer page closes with its own row for the ten cross-cutting concerns, C1 to C10. A layer is one of the fourteen parts of the estate that agents touch, and a concern is a requirement every layer must honour. This page is the view across all fourteen layers. Three words carry the distinction that matters. **Owned** means the layer defines the requirement and holds accountability for it. **Enforced** means the place where a violation is actually stopped, which is frequently a different layer. **Inherited** means the layer must carry the property through without weakening it. Inheritance is where most defects live, because it fails silently. The register applies at every autonomy level and tightens as autonomy rises.

**Figure: Cross-cutting concerns need named homes.** A concern that appears everywhere but is owned nowhere becomes a gap.

The full accessible table remains the source of record beneath this orientation view.

**What the diagram shows:** Heatmap concept showing identity, provenance, cost, evaluation, sovereignty, reversibility, and human oversight crossing all fourteen enterprise layers. The matrix crosses Identity, Provenance, Evaluation, Cost, Sovereignty, Reversibility, Human oversight with Runtime, Data, Action, Records, Channels, Governance. Annotated cells are Identity by Action: Primary enforcement; Provenance by Data: Attach at parse time; Evaluation by Runtime: Pre-release gate; Cost by Runtime: Per-run budget; Sovereignty by Data: Classification route; Reversibility by Records: Compensating action; Human oversight by Governance: Named accountability.

Diagram: https\://www\.agenticarchitectureskills.com/figures/concerns-layer-heatmap.svg

## Owned and enforced

**In short:** For each requirement, this table names who sets the rule, who stops a violation, and what goes wrong when the two are confused.

| #   | Concern                        | Owned at                                                                                                                                                      | Enforced at                                                                                                                                                                                                                                                                                                                                      | The failure when this is wrong                                                                |
| --- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| C1  | Identity and access            | [R10](https://www.agenticarchitectureskills.com/layers/r10-security-and-identity)                                                                             | [R03](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric) gateway, [R04](https://www.agenticarchitectureskills.com/layers/r04-systems-of-record) entitlement, [R01](https://www.agenticarchitectureskills.com/layers/r01-infrastructure) workload identity                                                                  | Identity asserted but never checked at the point of action                                    |
| C2  | Observability                  | [R12](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops)                                                                          | Emitted by every layer, aggregated at R12                                                                                                                                                                                                                                                                                                        | The licensed estate emits into its own console and coverage only looks complete               |
| C3  | Traceability and audit         | [R11](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty)                                                                       | [R12](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops) collection, [R14](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering) parse-time provenance                                                                                                                                        | Evidence reconstructed after the incident instead of produced as a byproduct                  |
| C4  | Grounding                      | [R02](https://www.agenticarchitectureskills.com/layers/r02-data-platform), [R14](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering) | [R09](https://www.agenticarchitectureskills.com/layers/r09-experience-and-channels) hardest external bar, [R05](https://www.agenticarchitectureskills.com/layers/r05-lob-and-ot) twin validation                                                                                                                                                 | Answering over weak evidence instead of refusing                                              |
| C5  | Impersonation and authenticity | [R10](https://www.agenticarchitectureskills.com/layers/r10-security-and-identity)                                                                             | [R03](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric) server identity, [R08](https://www.agenticarchitectureskills.com/layers/r08-productivity-and-collaboration)/[R09](https://www.agenticarchitectureskills.com/layers/r09-experience-and-channels) disclosure                                                        | Agent-to-human trust exploitation, named in the current threat taxonomies                     |
| C6  | Sovereignty and residency      | [R11](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty)                                                                       | [R01](https://www.agenticarchitectureskills.com/layers/r01-infrastructure) serving, [R02](https://www.agenticarchitectureskills.com/layers/r02-data-platform)/[R14](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering) indexes, [R03](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric) routing | Residency held at the source and broken by an embedding, a trace, or a session artifact       |
| C7  | Privacy                        | [R11](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty)                                                                       | [R14](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering) erasure cascade, [R02](https://www.agenticarchitectureskills.com/layers/r02-data-platform) index scope, [R12](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops) trace redaction                                                  | Deletion succeeds in the record and fails in the vectors, memories, and telemetry             |
| C8  | Safety and oversight           | [R13](https://www.agenticarchitectureskills.com/layers/r13-operating-model)                                                                                   | [R03](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric) gateway kill, [R07](https://www.agenticarchitectureskills.com/layers/r07-agent-platform) harness caps, [R05](https://www.agenticarchitectureskills.com/layers/r05-lob-and-ot) operator authority                                                                  | Oversight on the org chart but not in the workload                                            |
| C9  | Cost                           | [R12](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops)                                                                          | [R07](https://www.agenticarchitectureskills.com/layers/r07-agent-platform) per-run budgets, [R03](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric) rate limits                                                                                                                                                           | Spend attributed to a platform rather than a sponsor; supervision labour absent from the case |
| C10 | Resilience                     | [R01](https://www.agenticarchitectureskills.com/layers/r01-infrastructure)                                                                                    | Every layer's degraded mode; [R12](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops) budget-exhaustion behaviour                                                                                                                                                                                                    | Fallbacks designed per layer and never tested end to end                                      |

## Seven invariants

**In short:** Seven rules came up on their own in three or more layers, so the guide treats them as fixed requirements rather than recommendations.

Each surfaced independently in three or more layers, which is why they are invariants, rules that must always hold, rather than recommendations:

1. **Derived artifacts inherit the strictest classification of their sources.** That includes chunks, embeddings, session artifacts, traces, and fine-tuned weights.
2. **Erasure cascades or it did not happen.** When a record is deleted, so are its vectors, memories, traces, telemetry, eval datasets, and derived artifacts.
3. **Every layer degrades to a human queue**, and containment (conversations that never reach a person) is never manufactured by making the queue unavailable.
4. **Telemetry is collected outside the agent's control.** Self-report is testimony, not evidence.
5. **The kill switch is multi-point** (runtime, gateway, harness, identity plane), and an observability outage must not blind it.
6. **Enforcement is deterministic and outside the model.** It is held in the harness and enforced at the gateway or policy decision point (PDP).
7. **Provenance travels inside the artifact**, attached at parse time, when the document is first processed; provenance stored alongside is out of sync when it matters.

## The open gaps

**In short:** Six problems have no complete solution anywhere yet, and the guide says so rather than pretending otherwise.

The gaps below are published as unsolved. A matrix without holes would be the least credible artifact in this guide.

| Gap                                                                       | Layer | Status, August 2026                                                                                       |
| ------------------------------------------------------------------------- | ----- | --------------------------------------------------------------------------------------------------------- |
| Permissions on many-to-one derived artifacts                              | R14   | No complete published solution; intersection-stamping is the emerging practice                            |
| Behavioural baselining for agents in the SOC (security operations centre) | R10   | Unsolved; agent behaviour is legitimately variable, so both human and workload baselining methods misfire |
| Multi-agent incident reporting                                            | R11   | No frame exists for who reports what when several agents contribute to one incident                       |
| Error budgets for agent quality                                           | R12   | No published enterprise analog; an open pattern, not a practice                                           |
| Human-to-agent supervision ratio                                          | R13   | No credible published figure from any source                                                              |
| Embedded versus external agent outcomes                                   | R04   | No published head-to-head measurement on identical tasks                                                  |

**The research behind this page**

* [The concerns-by-layers matrix](https://www.agenticarchitectureskills.com/library/architecture/concerns-by-layers-matrix)
* [All fourteen research tracks](https://www.agenticarchitectureskills.com/library/layers)
