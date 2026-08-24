# Agent data engineering

How the data behind agents is prepared: documents read with their source attached, permissions that travel with every copy, governed memory, and deletion that reaches every derivative.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering (Markdown: https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering.md)
Updated: 2026-08-23
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

> **In plain terms.**
>
> This page covers the data work that decides whether agents answer well. Documents must be read accurately and keep a record of where they came from. Anything copied or derived from a document must carry that document's access rules and be deleted when the original is deleted. What an agent remembers must be checked before it becomes permanent, because a small amount of poisoned input can hijack it. The one thing to remember: carefully chosen data with a named owner beats a large pile of data.

## Target state

**In short:** Agents answer only as well as their data, so every data set gets a named owner, a traceable source, and a working delete.

A curation pipeline (data prepared for a purpose, with someone responsible for its quality) with named ownership per corpus, meaning each collection of documents. Layout-aware parsing attaches provenance, the record of where each piece came from, at parse time. Chunking, the splitting of documents into retrievable pieces, is evaluated per corpus rather than adopted as a universal recipe. Contextual enrichment is added where retrieval quality matters. Embeddings (the numeric fingerprints that make text searchable by meaning) are versioned and monitored for drift. Indexes carry permissions. Memory tiers have write governance, time-to-live, and erasure. Freshness is fed by change data capture, which streams each database change as it happens. Span-level lineage runs from every answer to its source. Curation labour is sized to risk. It is automated, with calibrated judges and sampled audits, where volume demands it. It is human where liability demands it. It always sits under a named accountable owner.

**Figure: The curation pipeline with provenance end to end.** Layout-aware parsing attaches provenance at page and cell level; it survives chunking, versioned embedding, permission-carrying indexing, and retrieval into every cited answer.

Side rails: CDC freshness, memory-write quarantine, erasure cascade with exclusion sets, blue/green re-embeds.

**What the diagram shows:** Agent data engineering pipeline from source through layout-aware parsing with provenance, contextual chunking, versioned embedding, permission-carrying index, pre-filtered retrieval, to span-cited answers, with freshness, quarantine, and erasure rails. The map contains Source: Owned corpus; authenticity at ingestion; Layout-aware parse: Provenance at page and cell level; Chunk + enrich: Per-corpus evaluated; contextual enrichment; Versioned embeddings: Blue/green migration; drift monitored; Permission-carrying index: ACLs in metadata; erasure exclusion sets; Memory tiers: Writes quarantined before durable promotion; Cited answer: Span-level lineage to source. Its connections are source to parse; parse to chunk; chunk to embed; embed to index; index to answer for pre-filtered retrieval; memory to index for promoted writes only. Important boundary: Derived artifacts inherit the strictest source classification; deletion cascades or it did not happen.

Diagram: https\://www\.agenticarchitectureskills.com/figures/layer-14-hero.svg

| Component                 | Responsibility                                               | Control it hosts                                                                              | Where it runs                 |
| ------------------------- | ------------------------------------------------------------ | --------------------------------------------------------------------------------------------- | ----------------------------- |
| Layout-aware parser       | Extract structure and attach page and cell provenance        | Parsing fidelity spot checks                                                                  | Ingestion                     |
| Chunker and enricher      | Produce retrievable units with surrounding context           | Per-corpus evaluation, not a global recipe                                                    | Ingestion                     |
| Embedding service         | Produce version-stamped vectors                              | Blue/green migration; drift alerts                                                            | Batch and incremental         |
| Permission-carrying index | Serve retrieval with access control lists (ACLs) in metadata | Pre-filter on live identity; exclusion sets before approximate nearest neighbour (ANN) search | Search substrate              |
| Memory store              | Hold durable agent memory                                    | Provenance on every write; quarantine before promotion                                        | Platform or dedicated service |
| Erasure controller        | Execute deletion across every derivative                     | Deletion as an audited callable operation                                                     | Cross-cutting                 |

## Mechanisms

### Parsing caps everything downstream

**In short:** If a document is read badly at the start, nothing later can recover what was lost.

Even the best document parsers lose at least 14 percent of retrieval performance compared with ground-truth structure (OHR-Bench, ICCV 2025, the International Conference on Computer Vision). Nothing downstream recovers what parsing dropped. That makes layout-aware parsing with provenance the floor rather than an optimisation. It also makes parsing fidelity a permanent sampled metric rather than a one-time acceptance test. Where data cannot leave the perimeter, the neutral default is a provenance-preserving open-source parser under a permissive licence.

### Chunking is evaluated, never inherited

**In short:** There is no universal best way to split documents; test each collection against its own real questions.

Gains from semantic chunking are inconsistent across corpora. Fixed-size chunking frequently matches it. Page-level chunking was best on average in one vendor benchmark \[vendor]. The rule that survives: evaluate per corpus, against that corpus's real questions. The best-evidenced upgrade is contextual enrichment. It reduced retrieval failures by 49 percent, and by 67 percent when combined with reranking \[vendor]. The published cost floor is about $1.02 per million document tokens with caching, where a token is the unit AI usage is billed in.

### Embedding operations and the re-embed budget

**In short:** Changing how text is turned into searchable numbers is costly, so version everything and switch only for proven gains.

Select an embedding model on a public multilingual benchmark rather than on vendor claims. Use dimension-truncation techniques where storage is the constraint. Upgrading the embedding model forces a full re-embed of the corpus. Reference costs run from more than ten hours on eight high-end graphics processing units (GPUs) to roughly $166 to $1,079 through an application programming interface (API) for a standard corpus. The discipline has five parts. Version-stamp every vector. Run blue/green index migrations. Evaluate embedding models quarterly. Migrate only for evaluation (eval) gains above a stated threshold, meaning gains on a test set with known right answers. Test cross-model conversion, published at roughly 100 times cheaper, before committing to a full re-embed. Object-store vector storage at up to 90 percent lower cost \[vendor] favours more, smaller, purpose-scoped indexes.

### Memory is an attack surface with quantified exposure

**In short:** Very little poisoned data can hijack an agent's memory, so each write is checked before it sticks.

Poisoning under 0.1 percent of a memory or knowledge base achieved over 80 percent attack success (AgentPoison, NeurIPS 2024, the Conference on Neural Information Processing Systems). Query-only memory injection reached 98.2 percent success without any write access (MINJA, 2025). Memory poisoning is named as a first-class failure mode in the current vendor failure-mode taxonomy. The controls follow directly. Provenance goes on every write. Memories are quarantined before promotion to durable tiers, with human or eval gates on that promotion. Poisoning is monitored, and memory-write quarantine rates are a standing metric. The functional tiers are working, episodic, semantic, and procedural. Hot-path writes happen during sessions and background consolidation happens between them. Treat any vendor's tier naming as a product detail rather than an architecture.

### Permissions must travel with derivations

**In short:** Anything made from a document inherits that document's access rules, because the copies can be turned back into the original.

Access control lists (ACLs) go into chunk and vector metadata, and retrieval pre-filters on the caller's live identity. This is non-negotiable because embeddings are recoverable text: 92 percent exact reconstruction of short inputs has been demonstrated and reproduced. So vectors inherit their sources' classification (sensitivity label), ACLs, and privacy obligations. **The open gap, stated rather than solved**: many-to-one derived artifacts (cross-document summaries, extracted memories, cluster labels) have no fully published permissions solution. Current practice stamps the intersection, meaning the most restrictive combination of the source permissions, and re-derives when an ACL changes. That is emerging practitioner-grade work, not a settled pattern.

### Erasure cascades or it did not happen

**In short:** Deleting a record must also delete every copy made from it, or the deletion did not really happen.

Deletion must reach raw logs, derived memories, and vectors. The published mechanics have three parts. Deleted-vector exclusion sets are consulted before approximate nearest neighbour (ANN) queries, the fast similarity search behind retrieval. Purpose-scoped namespaces give deletion a bounded blast radius. Deletion is exposed as an audited callable operation rather than a manual runbook. Derived artifacts inherit residency: embeddings, memories, and summaries built from in-region data are in-region data. Bitemporal facts separate event time from ingestion time. They let a superseded fact be invalidated without destroying the history that explains an earlier decision.

### Curation is the accuracy lever, and it is measurable

**In short:** Well-chosen data beats more data, and the gain shows up in how often the agent is wrong.

A curated domain knowledge base cut hallucination (confident false statements) from 35 percent to 6 percent. Growing a corpus from 54 to 1,128 uncurated documents dropped accuracy from 75 percent to under 40 percent until domain scoping fixed it: more data made the system worse. The trade is formalised as coverage versus trust. Where content is aspect-rich, an item can be represented through several purpose-specific embeddings, each indexed separately and queried by the view that matches the question. That improves precision per question type, at embedding cost rather than model cost. The taxonomy of views is designed with a model from the corpus and hardened by a human; classical machinery executes at scale, and a model names the discovered clusters. The guide tested this pattern in five rounds on public corpora ([the research pages](https://www.agenticarchitectureskills.com/patterns)): several vectors per document beat one decisively, purpose views beat matched chunks only where queries target one aspect and lose where they concern whole documents, and conditioning the views on the objective made retrieval worse in every form tested. The design that survived is [the recommended approach](https://www.agenticarchitectureskills.com/patterns). Measure with coverage-aware metrics such as alpha-nDCG (normalised discounted cumulative gain, coverage-aware form) or sub-question coverage, never plain recall.

## Design decisions

* **One universal index vs use-case-scoped** ([CD-11](https://www.agenticarchitectureskills.com/decisions#cd-11)), a challenged default about whether to build one big search index or several. The answer is two layers. A permission-aware universal index serves discovery and cross-silo questions. Purpose-scoped curated indexes serve high-stakes tasks.
* **Graph database vs embedding retrieval** ([CD-1](https://www.agenticarchitectureskills.com/decisions#cd-1)), a challenged default about whether a knowledge graph should replace vector search. The answer is a routed hybrid, vector-first, with a selective provenance-linked graph only for deterministic traversal (fixed-rule, repeatable lookups). If you add a graph, every generated edge carries a source-span identifier (ID), the extraction model and its version, a confidence value, and a validity interval.
* **Purpose-specific embedding views vs matched chunking** ([CD-25](https://www.agenticarchitectureskills.com/decisions#cd-25)), a challenged default about whether to split documents by purpose or by fixed windows. The answer is chunks first, views only on a measured win against a control with the same embedding budget, and never a view taxonomy conditioned on the objective.
* **Corpus ownership**: every corpus an agent depends on has a named accountable owner. Curation labour is sized to risk. The dedicated-curator-per-domain form is not supported as published fact, and accountability cannot be automated.

## Cross-cutting concerns

| #   | Concern                | Treatment at this layer                                                                                                                                   |
| --- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| C1  | Identity and access    | ACLs propagated into chunks, vectors, and derived artifacts; pre-filtered retrieval; intersection-stamping for many-to-one derivations                    |
| C2  | Observability          | Pipeline telemetry: parsing fidelity, embedding drift, freshness lag, memory-write rates                                                                  |
| C3  | Traceability and audit | Provenance from parse time through chunk, embedding version, retrieval, and claim; memory writes audited                                                  |
| C4  | Grounding              | Curated corpora with owners; contextual enrichment; freshness discipline; bitemporal fact handling                                                        |
| C5  | Impersonation          | Source authenticity at ingestion; no unattributed content into grounding or memory                                                                        |
| C6  | Sovereignty            | Derived artifacts inherit source residency; region-scoped pipelines and indexes                                                                           |
| C7  | Privacy                | Embeddings as recoverable personal data; erasure cascades across logs, memories, vectors, exclusion sets; time-to-live (TTL) limits; consent at ingestion |
| C8  | Safety and oversight   | Memory write governance with quarantine; poisoning monitoring; human gates on promotion to durable tiers                                                  |
| C9  | Cost                   | Re-embedding budgets; curation labour accounting; per-corpus index costs                                                                                  |
| C10 | Resilience             | Everything regenerable from raw; blue/green migrations; full re-index as the recovery baseline                                                            |

## Evidence and limits

The parsing loss, the poisoning success rates, the embedding reconstruction, and the corpus-curation accuracy results are peer-reviewed. The contextual-enrichment improvements, the chunking comparisons, and the storage economics are vendor-published and flagged. One standing refusal: every memory-service benchmark now in circulation is vendor-authored and publicly disputed between vendors, so this guide cites none of them. Run your own acceptance suite instead. Build that suite to cover local facts, semantic recall, exact identifiers, multi-hop questions, temporal contradictions, corpus-global synthesis, unanswerable questions, deletions, and ACL enforcement. Measure correctness, evidence recall, faithfulness, 95th-percentile (p95) latency, cost, ingestion lag, and permission leakage. Re-verify two things: whether any complete solution to many-to-one derived-artifact permissions is published, and whether independent memory benchmarks emerge.

**The research behind this page**

* [Agent data engineering findings](https://www.agenticarchitectureskills.com/library/layers/r14-agent-data-engineering/findings)
* [Sources](https://www.agenticarchitectureskills.com/library/layers/r14-agent-data-engineering/sources)
* [Products named for orientation](https://www.agenticarchitectureskills.com/architecture), on the one-page wall chart
