# The data-to-memory pipeline

The nine-stage path from company data to a cited answer, with the source trail intact, and the two rules that make it a governed record rather than plumbing.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/architecture/data-to-memory (Markdown: https://www.agenticarchitectureskills.com/architecture/data-to-memory.md)
Updated: 2026-08-23
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

> **In plain terms.**
>
> An AI agent is only as trustworthy as the information put in front of it. This page follows company data through nine stages, from the original document to an answer that cites its sources, and on into what the agent remembers afterwards. Each stage has a known way of failing, and each failure has a control. The one thing to remember: anything derived from your data carries the same access rules, privacy duties, and deletion duties as the original. That includes the searchable copies agents use and the memories they keep.

## The pipeline

**In short:** Data passes through nine steps on its way to an agent's answer, and every step keeps a record of where the information came from.

**Figure: From source data to governed memory.** Permission, provenance, and classification travel with content from ingestion onward.

Promotion to durable memory is gated; derived artifacts inherit the strictest source classification.

**What the diagram shows:** Nine-stage data-to-memory pipeline covering source intake, permission capture, parsing, classification, curation, indexing, retrieval, promotion, and erasure propagation. The sequence contains 9 stages: 1, Source: Acquire governed content.; 2, Permissions: Capture ACLs and purpose.; 3, Parse: Attach provenance immediately.; 4, Classify: Apply strictest inherited class.; 5, Curate: Select for the use case.; 6, Index: Build permission-aware retrieval.; 7, Retrieve: Filter before model access.; 8, Promote: Gate durable memory changes.; 9, Erase: Cascade deletion to derivatives..

Diagram: https\://www\.agenticarchitectureskills.com/figures/data-to-memory-pipeline.svg

There are nine stages, each with a measured failure mode. The deep treatment is on [R02](https://www.agenticarchitectureskills.com/layers/r02-data-platform), the data platform layer, and [R14](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering), the agent data engineering layer. The architectural spine:

1. **Parse with provenance.** Parsing that understands page layout attaches provenance, a record of exactly where each piece came from, at page and cell level as it reads. Even the best parsers lose at least 14 percent of retrieval performance compared with the true document structure, so parsing fidelity is spot-checked forever.
2. **Chunk per corpus, enrich contextually.** Documents are split into chunks small enough to retrieve, and no single splitting recipe survives evaluation across every collection. Enriching each chunk with context is the best-evidenced upgrade: 49 percent fewer retrieval failures, and 67 percent fewer with reranking \[vendor].
3. **Embed versioned.** Every embedding (a numeric fingerprint used to find similar meaning) carries the version of the model that produced it. Upgrades run blue/green, with the new version alongside the old, and migrate only when a stated eval gain is met. The reason for caution is cost: re-embedding everything takes hours on serious hardware, or a four-figure sum through a paid application programming interface (API).
4. **Index with permissions inside.** The access control lists (ACLs) of each source are carried into the vector index as metadata. Retrieval is filtered on the caller's live identity before the search runs, and a failed permissions sync fails closed, returning nothing rather than too much. Filtering after the search is the anti-pattern: it leaks counts and starves results.
5. **Retrieve with refusal available.** A semantic contract, an agreed business definition of each measure, routes high-stakes numbers either to a deterministic answer computed by fixed rules or to a refusal. That turns silent wrong answers into visible ones.
6. **Cite by construction.** Answers carry lineage back to their sources at the level of individual text spans. This is also the single most valuable component of the evidence posture, as [R11](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty), the governance, risk, and sovereignty layer, sets out.
7. **Write memory through quarantine.** Anything written to durable agent memory carries provenance and waits in quarantine until it is promoted. The reason is measured. Poisoning less than 0.1 percent of a memory store has achieved more than 80 percent attack success. Injection through queries alone has reached 98.2 percent.
8. **Refresh by CDC.** Change data capture (CDC), which streams each database change as it happens, keeps indexes fresh to within minutes at close to batch cost. Full streaming has to be earned by how often decisions are made, not chosen by default. In one documented case the two approaches cost $400 versus $7,600 per month for the same stated requirement.
9. **Erase in cascade.** Deleting a record triggers an erasure cascade: the deletion reaches raw stores, embeddings, memories, traces, and every derived artifact. Search consults a list of deleted embeddings before any approximate-nearest-neighbour query (the fast similarity search), so deleted items cannot resurface. Deletion itself is exposed as an audited operation.

## The two rules that make it governance, not plumbing

**In short:** Searchable copies of your data are still your data, and multi-document summaries have no complete permissions answer yet.

**Embeddings are recoverable data.** Exact reconstruction of short inputs from their embeddings has been demonstrated at a 92 percent rate. So embeddings inherit everything from their sources, in full. That means the sensitivity classification, the access control lists, the data residency rules (which country or region the data may sit in), and the erasure obligations. Any derived artifact inherits the strictest classification among its sources.

**The open gap, stated rather than papered over:** artifacts built from many sources at once (cross-document summaries, extracted memories) have no complete published permissions solution. Current practice gives such an artifact only the permissions that all of its sources share (the intersection), and rebuilds it whenever a source's access list changes. This is emerging, practitioner-grade practice, and it is flagged as such.

## Memory tiers

**In short:** What an agent holds during one task is an engineering matter; what it keeps afterwards is a record with ownership and privacy duties attached.

Working context, the model's working memory for one task, is engineering. Durable memory is a record. The line sits where information persists past the end of a session. From that point, ownership, consent, retention, and erasure obligations attach. Promotion into a durable tier is a gated act, never an accumulation.

**Figure: Memory persistence increases obligation.** More durable memory is not more intelligence; it is more ownership, consent, retention, and erasure work.

The M1–M5 namespace keeps memory distinct from learning maturity.

**What the diagram shows:** Five-tier memory stack from thread and retrieved knowledge through session, entity, and cross-domain memory, with obligations increasing as persistence rises. The sequence contains 5 stages: 1, M1 Thread: The current conversation or run.; 2, M2 Retrieved knowledge: Permission-aware evidence for the current turn., followed by the Provenance on every span gate; 3, M3 Session: Bounded continuity across hours or days., followed by the Residency and retention gate; 4, M4 Entity memory: Durable profiles of customers, assets, cases, or employees., followed by the Consent, ownership, and erasure gate; 5, M5 Cross-domain: Shared memory with the broadest blast radius., followed by the Strictest governance gate.

Diagram: https\://www\.agenticarchitectureskills.com/figures/memory-obligation-tiers.svg

**The research behind this page**

* [The memory-pipeline architecture](https://www.agenticarchitectureskills.com/library/architecture/memory-pipeline-architecture)
* [Agent data engineering findings](https://www.agenticarchitectureskills.com/library/layers/r14-agent-data-engineering/findings)
* [Data platform findings](https://www.agenticarchitectureskills.com/library/layers/r02-data-platform/findings)
* [The multi-card retrieval experiments](https://www.agenticarchitectureskills.com/patterns), the measured evidence behind the purpose-scoped curation step
