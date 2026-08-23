# The decision catalog

Twenty-five technology choices usually made by habit, each with a verdict, the condition that decides your case, and what would change it.

Source: https://www.agenticarchitectureskills.com/decisions (Markdown: https://www.agenticarchitectureskills.com/decisions.md)

> **In plain terms.**
>
> This page lists twenty-five technology choices that are usually made by habit or by following the crowd, and records what the evidence says about each. It matters because these are the choices that decide cost, risk, and how much of the estate has to be rebuilt later. The one thing to remember: each decision comes with the single condition that would change it, so check that condition against your own situation before following the verdict.

Each entry is a challenged default: a hyped or habitual technology choice the research contested, resolved by evidence and economics rather than adoption momentum. Each record holds the question, the verdict, the discriminator that decides your case, and the register status in the research vocabulary. The statuses are converged, supported with reframe, split, conditionally approved, and position. This catalog records technology decisions; the programme's own decision log is at [/library/decisions](https://www.agenticarchitectureskills.com/library/decisions).

| ID              | Question                                                                                                    | Verdict in one line                                                                                 |
| --------------- | ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| [CD-1](#cd-1)   | Graph database vs embedding retrieval                                                                       | Routed hybrid, vector-first; a graph only for deterministic traversal                               |
| [CD-2](#cd-2)   | Dedicated Model Context Protocol (MCP) gateway vs extend application programming interface (API) management | Extend the incumbent by default; dedicated is conditional                                           |
| [CD-3](#cd-3)   | Replace robotic process automation (RPA) vs coexist                                                         | Coexist, supervised; replacement earned per workload                                                |
| [CD-4](#cd-4)   | Agent-to-agent protocols now                                                                                | Not yet for most; selective for cross-organisation federation                                       |
| [CD-5](#cd-5)   | Modernize the enterprise service bus (ESB) first vs bypass                                                  | Strangle, do not wait; govern before you wrap                                                       |
| [CD-6](#cd-6)   | Self-hosted graphics processing unit (GPU) estate vs metered APIs                                           | Metered by default; open-weight via API is the cost path                                            |
| [CD-7](#cd-7)   | Kubernetes everywhere vs managed runtimes                                                                   | Split by layer: Kubernetes for self-hosted serving, managed runtimes for orchestration              |
| [CD-8](#cd-8)   | Semantic-layer product vs governed views                                                                    | Per use case, chosen by failure mode, not accuracy points                                           |
| [CD-9](#cd-9)   | Dedicated vector database vs simplest substrate                                                             | Climb the ladder; dedicated is the top rung, not the default                                        |
| [CD-10](#cd-10) | Data mesh vs governed central substrate                                                                     | Mesh ideas on a governed substrate                                                                  |
| [CD-11](#cd-11) | One universal index vs use-case-scoped                                                                      | Two layers: permission-aware universal for discovery, scoped for high stakes                        |
| [CD-12](#cd-12) | Real-time vs batch grounding                                                                                | Change data capture (CDC) is the default; streaming is earned                                       |
| [CD-13](#cd-13) | Dedicated AI security platforms vs security information and event management (SIEM) extension               | Platform absorption is the market answer; baselining stays unsolved                                 |
| [CD-14](#cd-14) | Broad vs narrow AI Act classification                                                                       | Neither: a risk-tiered evidence posture                                                             |
| [CD-15](#cd-15) | Application performance monitoring (APM) extension vs dedicated large language model (LLM) observability    | The question dissolved; choose on open telemetry standards, eval depth, self-hosting                |
| [CD-16](#cd-16) | Guardrail products vs deterministic gates                                                                   | Gates own the boundary; guardrails are advisory wherever they run                                   |
| [CD-17](#cd-17) | Embedded vendor agents vs external through APIs                                                             | Decided by authority boundary; nobody has measured the head-to-head                                 |
| [CD-18](#cd-18) | Brokered operational technology (OT) read paths vs unidirectional                                           | Consequence class decides; transport is downstream of the control point                             |
| [CD-19](#cd-19) | Fine-tuning vs prompt-and-context engineering                                                               | An ordering, not a side: optimise, then distil, then reinforcement fine-tuning behind a hard grader |
| [CD-20](#cd-20) | AI-first vs human-first service                                                                             | Wrong axis: containment as the target is the failure; resolution as the target is the design        |
| [CD-21](#cd-21) | Multi-agent orchestration vs a single good loop                                                             | Parallel breadth only; tokens explain most of the famous gains                                      |
| [CD-22](#cd-22) | Agents as workforce vs agents as tools                                                                      | Keep the accountability, drop the personnel metaphor                                                |
| [CD-23](#cd-23) | One universal assistant vs many specialised agents                                                          | Wrong axis: solitary vs coordinated work is the predictive variable                                 |
| [CD-24](#cd-24) | Separate customer-facing stack vs shared platform                                                           | Separate lane and edge, shared control plane; the justification is legal                            |
| [CD-25](#cd-25) | Purpose-specific embedding views vs matched chunking                                                        | Chunks first; views only on a measured win; never condition the index on the objective              |

## The records

### CD-1. Graph database vs embedding retrieval

**In short:** Use ordinary search plus meaning-based search for most questions; add a graph only to follow exact relationships.

**Verdict: routed hybrid, vector-first.** Keep a canonical raw and event store. Combine lexical search with contextual dense embeddings (numeric fingerprints of text that let a computer find similar meaning). Where content is aspect-rich, keep multiple purpose-specific views. Rerank over candidates. Treat topics as versioned, regenerable navigation metadata. Add a selective, provenance-linked graph only for deterministic relationship traversal: lineage, dependency and impact, authorisation paths, temporal validity, transactional shared state. Edge hygiene if you do: every generated edge carries a source-span identifier (ID), extraction model and version, confidence, and a validity interval. The measured spreads justify routing rather than picking a side. Graph-augmented retrieval wins multi-hop benchmarks while costing an order of magnitude more to build, and dense-plus-graph beat either alone. Rejected outright: graph-only memory, vector-only without lexical and raw sources, topic summaries as source of truth, and fine-tuned weights as factual memory. Status: converged. Owner: [R14](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering), [R02](https://www.agenticarchitectureskills.com/layers/r02-data-platform).

### CD-2. Dedicated MCP gateway vs extending API management

**In short:** Use the API management tools you already own for agent traffic; buy a dedicated gateway only for controls they lack.

**Verdict: extend the incumbent by default.** The incumbent is the application programming interface (API) management platform you already run. The 2026-07-28 Model Context Protocol (MCP) specification was deliberately redesigned to be routable and authorisable by ordinary Hypertext Transfer Protocol (HTTP) gateways. Every incumbent shipped support within a year. Choose a dedicated gateway for agent-specific controls that incumbents do not model well: tool-description diffing and poisoning scans, multi-runtime federation, and elicitation mediation. Status: conditionally approved, converging. Owner: [R03](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric).

### CD-3. Replace RPA vs coexist

**In short:** Keep the old screen-clicking bots for mechanical steps, let agents handle judgement, and retire bots only when a proper interface arrives.

**Verdict: coexist, supervised.** Robotic process automation (RPA) bots stay the deterministic execution layer for systems without APIs; agents reason and handle exceptions above them. Replacement is earned per workload when a governed API arrives, never declared estate-wide. Status: converged. Owner: [R03](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric).

### CD-4. Agent-to-agent protocols now

**In short:** Standards for agents talking directly to other agents are not worth adopting yet, except across company boundaries.

**Verdict: not yet for most.** The standard consolidated and stabilised, but published milestones are organisation counts rather than production evidence. Teams approximate coordination with tool-protocol primitives. Adopt selectively for cross-organisation agent federation, where nothing else fits. Status: position, re-verify quarterly. Owner: [R03](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric).

### CD-5. Modernize the ESB first vs bypass

**In short:** Do not wait for the old integration bus to be modernised; govern what agents use and replace the rest gradually.

**Verdict: strangle, do not wait; govern before you wrap.** To strangle an enterprise service bus (ESB) is to replace it one slice at a time while it keeps running, instead of waiting for a full modernisation. Of modernisation programmes, 74 percent fail to complete. Incumbent gateways expose governed APIs as tools with zero backend change. The discipline: govern the specific API paths agents will use before exposing them, and let each strangler increment retire real load. Status: converged. Owner: [R03](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric).

### CD-6. Self-hosted GPU estate vs metered APIs

**In short:** Pay per use for AI models rather than running your own GPU fleet, unless the work must stay isolated.

**Verdict: metered by default; the cost path is open-weight via metered APIs, not self-hosting.** Open-weight models are models whose weights are published for anyone to run. Break-even for self-hosting sits at sustained nine-figure token volumes per month per workload at high utilisation, with operations multipliers of 1.3 to 2 times. At 10 percent utilisation, cost per token rises roughly tenfold. Against budget open-weight API pricing, break-even recedes to billions of tokens per month. Self-hosting earns its place for air-gap and classification, not for generic residency. Status: refined by evidence. Owner: [R01](https://www.agenticarchitectureskills.com/layers/r01-infrastructure).

### CD-7. Kubernetes everywhere vs managed agent runtimes

**In short:** Use Kubernetes only for model servers you host yourself; run the agents themselves on a managed service.

**Verdict: split by layer.** Model serving belongs on Kubernetes only if you self-host at all. Agent orchestration belongs on managed runtimes with per-session isolation and durability. The lock-in is symmetric: managed runtimes are proprietary control planes, and the portability camp sells its own ecosystem. Status: position with strong support. Owner: [R01](https://www.agenticarchitectureskills.com/layers/r01-infrastructure), [R07](https://www.agenticarchitectureskills.com/layers/r07-agent-platform).

### CD-8. Semantic-layer product vs governed views

**In short:** Whether to buy a shared-definitions product depends on how each use case fails, not on small accuracy differences.

**Verdict: per use case, chosen by failure mode.** The load-bearing property is failure-mode conversion: governed semantics turn silent wrong answers into refusals or deterministic answers. Benchmarks show large gains on modelled scope with partial coverage. A disciplined counter-camp reaches comparable accuracy through data modelling alone. The binding variable is curated business context, and a semantic-layer product is its most governable packaging. Status: split, both camps published. Owner: [R02](https://www.agenticarchitectureskills.com/layers/r02-data-platform).

### CD-9. Dedicated vector database vs the simplest substrate

**In short:** Start with the simplest storage that handles your data volume, and move up only when measurements show strain.

**Verdict: climb the ladder.** Use brute force below roughly 100,000 vectors. Use pgvector up to the low millions. At 1 million vectors it answers in under 20 milliseconds with recall above 95 percent. Build pain starts at roughly 2 million, and partitioning is needed at 5 million and above. Use scale-out Postgres extensions to roughly 50 million. Use a dedicated vector database engine for extreme scale, heavy write rates, or filter-heavy multi-tenancy, where the 99th-percentile (p99) latency gap becomes real. Platform-bundled vector search is table stakes: prefer it where the corpus already lives, because governance and access control list (ACL) inheritance come free. Vendor viability belongs in selection. Status: converged. Owner: [R02](https://www.agenticarchitectureskills.com/layers/r02-data-platform).

### CD-10. Data mesh vs governed central substrate

**In short:** Let business units own their data, but keep the shared store and its permissions central and governed.

**Verdict: mesh ideas on a governed substrate.** Every shipped ACL-sync architecture assumes a governed central index. Pure mesh multiplies permission sync, definitional consistency, and freshness monitoring, which are exactly what agents punish. Keep domain ownership as an operating idea; keep the substrate governed and central. Status: converged. Owner: [R02](https://www.agenticarchitectureskills.com/layers/r02-data-platform).

### CD-11. One universal index vs use-case-scoped

**In short:** Run one permission-aware search across everything for discovery, and separate purpose-built collections where mistakes are costly.

**Verdict: two layers.** A permission-aware universal index for discovery and cross-silo questions, plus purpose-scoped curated indexes (or scoped routing over the universal one) for high-stakes tasks. The trade is formalised as coverage versus trust, and even the largest universal-index vendors shipped scoping controls as mitigation. Status: converged. Owner: [R14](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering).

### CD-12. Real-time vs batch grounding

**In short:** Keep agent data fresh by copying each database change as it happens; buy real-time streaming only where decisions cannot wait.

**Verdict: CDC is the default; streaming is earned.** Change data capture (CDC) delivers minutes-level freshness for grounding at near batch cost; a documented like-for-like comparison ran $400 against $7,600 per month. Streaming is justified by decision cadence (fraud, operational triage), not by default. Status: converged. Owner: [R02](https://www.agenticarchitectureskills.com/layers/r02-data-platform).

### CD-13. Dedicated AI security platforms vs SIEM extension

**In short:** Buy AI security inside the platforms you already run, but know that spotting abnormal agent behaviour is still unsolved.

**Verdict: the market resolved toward platform absorption; buy accordingly, but absorption is not parity.** Six AI-security acquisitions in roughly fourteen months, plus two non-human-identity deals, moved the capability inside platforms. The honest gap: behavioural baselining of agents remains unsolved in mainstream security information and event management (SIEM) systems, and guardian agents persist as a distinct runtime category. Status: refined. Owner: [R10](https://www.agenticarchitectureskills.com/layers/r10-security-and-identity).

### CD-14. Broad vs narrow AI Act classification

**In short:** Do not bet on a broad or narrow reading; keep basic records for every agent and full records for high-risk ones.

**Verdict: neither pole; a risk-tiered evidence posture.** Two currents pull on EU AI Act classification. The legal (de jure) current tilted narrow, through deferrals. The interpretive current tilts broad, through draft classification tests and the multi-purpose presumption. Enforcement capacity is thin. Run an evidence floor for every production agent, and Article 12-grade instrumentation (the Act's record-keeping article) for the plausibly high-risk tier. Re-verify at every regulatory milestone. Status: position, dated. Owner: [R11](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty).

### CD-15. APM extension vs dedicated LLM observability

**In short:** The extend-or-buy monitoring question has largely disappeared because the specialists were bought up; choose on standards, testing depth, and self-hosting.

**Verdict: the question dissolved.** The observability category merged. Choose on the real fault lines. The first is an OpenTelemetry (OTel)-native pipeline versus a proprietary software development kit (SDK); both need a translation layer while the conventions stay unstable. The second is eval-loop depth versus infrastructure correlation. The third is self-hosting. Most enterprises land on the application performance monitoring (APM) incumbent plus one eval-capable tool. Status: dissolved by consolidation. Owner: [R12](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops).

### CD-16. Guardrail products vs deterministic gates

**In short:** Fixed rules decide whether an agent may act; AI-based filters can warn but must never grant or deny.

**Verdict: deterministic gates own the authorisation boundary; guardrails are advisory wherever they run.** In published tests, roughly 72 to 77 percent of attacks got past major commercial guardrails, and up to 100 percent in some configurations. The one guardrail measured at 0 percent bypass cost 16.22 percent false positives and roughly 1.5 seconds of added latency. Policy engines decide in under a millisecond. Status: converged. Owner: [R10](https://www.agenticarchitectureskills.com/layers/r10-security-and-identity).

### CD-17. Embedded vendor agents vs external agents through governed APIs

**In short:** Use the vendor's built-in agent when work stays inside one product; use your own agents when work spans systems.

**Verdict: decided by authority boundary, and nobody has measured the head-to-head.** Inside one system, both paths now enforce identical permissions (stated parity), so choose on model control, the cost meter, and the customisation ceiling. Across systems, no vendor's permission plane is authoritative and entity resolution binds, so external orchestration is a requirement rather than a preference. Generic benchmarks show up to fiftyfold cost variation at similar accuracy; the harness matters more than the badge. Status: reframed. Owner: [R04](https://www.agenticarchitectureskills.com/layers/r04-systems-of-record).

### CD-18. Brokered OT read paths vs unidirectional architectures

**In short:** For plant and grid systems, the design depends on whether agent output could ever affect a physical control.

**Verdict: consequence class decides the control point; transport is downstream.** This record covers operational technology (OT), the systems that run physical equipment. If any output can reach or influence a control action: unidirectional or push-based architectures, plus a documented path back to manual or deterministic control. If output is confined to alerts, recommendations, and data-quality findings, a brokered read path is defensible. It needs per-agent identity, least privilege, inline inspection, operator-custodied logging, and a tested isolation plan. Status: converged across camps. Owner: [R05](https://www.agenticarchitectureskills.com/layers/r05-lob-and-ot).

### CD-19. Fine-tuning and RFT vs prompt-and-context engineering

**In short:** Improve instructions and context first, then teach a smaller model the results; retrain weights only as a last resort.

**Verdict: an ordering, not a side.** Optimise context and prompts against a locked eval suite first; measured wins came at up to 35 times fewer rollouts than reinforcement learning (RL). Distil when latency or unit cost forces it. Use reinforcement fine-tuning (RFT) only when a programmable, hard-to-game grader exists and the prompt-optimised ceiling is demonstrably flat. RFT is the wrong tool for format and tone. Counter-evidence kept honestly: a fine-tuned small model has beaten a prompt-engineered frontier model decisively on cost and accuracy in narrow classification. Status: refined. Owner: [R06](https://www.agenticarchitectureskills.com/layers/r06-intelligence-and-learning).

### CD-20. AI-first vs human-first service

**In short:** Do not aim to keep customers away from staff; aim to solve their problems and measure who has to come back.

**Verdict: the axis is wrong; the target is what fails.** Every documented reversal of an AI-first programme set a containment target (the share of conversations that never reach a person) or a headcount target. Target resolution, instrument repeat contact beside it, and let containment be an outcome. Status: reframed. Owner: [R09](https://www.agenticarchitectureskills.com/layers/r09-experience-and-channels).

### CD-21. Multi-agent orchestration vs a single good loop

**In short:** Splitting one job across several agents pays off only for wide, independent work; most famous gains came from extra tokens.

**Verdict: parallel breadth only, and hold compute constant before believing any comparison.** The famous orchestrator-worker win was bought with roughly 15 times the tokens. Token usage alone explains most of the variance on related benchmarks. At constant reasoning tokens, single agents match or beat multi-agent systems on multi-hop reasoning. Pay the multiplier only when strands are independent and read-heavy, the information exceeds one context window, the accuracy bar exceeds single-pass, and the value clears the cost. Status: supported with reframe. Owner: [R07](https://www.agenticarchitectureskills.com/layers/r07-agent-platform).

### CD-22. Agents as workforce vs agents as tools

**In short:** Give every agent a named accountable person, but do not treat agents as employees with personnel records.

**Verdict: keep the accountability, drop the personnel metaphor.** The accountability substance is productised: a named sponsor on the identity, automatic transfer, and scoped expiring credentials. The flagship attempt to give agents employee records was withdrawn within days. The strongest field deployment achieves per-agent accountability with no org-chart presence. Status: refined. Owner: [R13](https://www.agenticarchitectureskills.com/layers/r13-operating-model).

### CD-23. One universal assistant vs many specialised agents

**In short:** Ask whether the work is done alone or with others, because AI reliably helps solo work and rarely changes teamwork.

**Verdict: the axis is wrong; solitary versus coordinated work is the predictive variable.** Individually provisioned AI reliably improves solitary work and reliably fails to change coordinated work, because coordination requires agreeing new norms. The evidenced third answer is a long tail of narrow agents built by employees inside the horizontal platform. Status: reframed. Owner: [R08](https://www.agenticarchitectureskills.com/layers/r08-productivity-and-collaboration).

### CD-24. Separate customer-facing stack vs shared platform

**In short:** Customer-facing agents get their own channels and legal safeguards, but share knowledge, identity, tools, and monitoring with everything else.

**Verdict: separate lane and separate edge on a shared control plane, justified by legal exposure rather than technology.** Edge-specific: channels and telephony, disclosure mechanics, adversarial hardening, and the legal-evidence layer. Shared, and duplicating them is a defect: knowledge corpus, identity, tool layer, evals, observability, and model access. Honest caveat: no published case measures either choice. Status: position with legal anchors. Owner: [R09](https://www.agenticarchitectureskills.com/layers/r09-experience-and-channels).

### CD-25. Purpose-specific embedding views vs matched chunking

**In short:** Split documents into several vectors, start with plain chunks, and add purpose-specific views only where your own queries prove they help.

**Verdict: chunks first, views on a measured win, and never condition the index on the objective.** Several embeddings per document beat one on aspect-rich material (a pooled index fell from 0.815 to 0.294 nDCG\@10 as aspects grew from one to ten), but most of that benefit is capacity: a blind sliding window recovered 0.610 of the 0.674 that purpose views gained on the LIMIT stress test, and on human-judged scientific abstracts purpose views scored 0.032 to 0.042 below matched chunks. Views won only where queries targeted one aspect (+0.188 at ten aspects, with 25 percent fewer embeddings). Conditioning the view design on the objective, the business context, or the schema made retrieval worse in every form tested, including real instruction-following data, where a plain instruction-prepended encoder beat every view arm. The discriminator is the query distribution: aspect-targeted queries over aspect-rich items earn views; whole-document queries do not. Keyword search stays fused in either case. Status: independently measured, five rounds, two machines. Owner: [R14](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering); the evidence is on the [research pages](https://www.agenticarchitectureskills.com/research), and the design is [the recommended approach](https://www.agenticarchitectureskills.com/research/recommended-approach).
