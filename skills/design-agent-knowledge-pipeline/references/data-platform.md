# Data platform

How agents get trustworthy company data: indexes that respect who may see what, fixed business definitions for high-stakes numbers, and freshness matched to how often decisions are made.

Source: https://www.agenticarchitectureskills.com/layers/r02-data-platform (Markdown: https://www.agenticarchitectureskills.com/layers/r02-data-platform.md)

> **In plain terms.**
>
> This page covers the company data that agents read before they answer or act. An agent must only see what the person asking could see, and it must be able to show where each answer came from. For questions where a wrong number is costly, it must give the same answer every time or say that it does not know. The one thing to remember: a search index is a copy of your data and needs the same protection as the original.

## Target state

**In short:** Agents answer from governed company data that respects permissions, carries its source, and is only as fresh as decisions need.

Grounding (answering from trusted company sources) is a governed product, not a side effect of a data lake. The data agents ground on is well modelled. Wherever the stakes demand a deterministic answer (the same answer every time), the business definitions behind it are governed. Indexes are permission-aware, and retrieval is filtered on the caller's live identity before results are returned. Freshness is fed by change data capture (CDC), which streams each database change as it happens. It is sized to how often decisions are made, not to fashion. Provenance runs from every answer back to the exact passage it came from. Catalogues supply ownership, lineage, and definitions as context for agents, not as a portal humans visit. Embeddings (numeric fingerprints of text) are treated as recoverable data, and they carry their sources' classification. Anything derived from several sources inherits the strictest classification among them.

**Figure: Grounding as a governed product.** Permissions crawl into index metadata and retrieval is pre-filtered on the caller's live identity; post-filtering is the anti-pattern.

Fail-close on permission-sync errors; provenance runs from answer back to source span.

**What the diagram shows:** ACL-aware grounding pipeline from source systems through permission crawl into index metadata, pre-filtered retrieval on live identity, and span-level provenance, with fail-close branch. The map contains Source systems: Documents, records, events with native ACLs; Permission crawl: ACLs into index metadata; ReBAC pre-computation; Governed index: Version-stamped vectors; purpose-scoped where stakes demand; Pre-filtered retrieval: Caller's live identity inside the query; Semantic contract: Deterministic answers or refusal for high-stakes numerics; Agent context: Answer with span-level source provenance. Its connections are sources to crawl; crawl to index for fail-close on sync error; index to retrieval; retrieval to agent; semantics to agent for numeric questions. Important boundary: Embeddings are recoverable text; vectors inherit source classification and erasure obligations.

Diagram: https\://www\.agenticarchitectureskills.com/figures/layer-02-hero.svg

| Component           | Responsibility                                              | Control it hosts                                           | Where it runs                       |
| ------------------- | ----------------------------------------------------------- | ---------------------------------------------------------- | ----------------------------------- |
| Permission crawler  | Pull source access control lists (ACLs) into index metadata | Fail-close on sync error                                   | Alongside each connector            |
| Governed index      | Serve retrieval with permissions inside the query           | Pre-filter on live caller identity                         | Existing search or vector substrate |
| Semantic layer      | Answer high-stakes numerics deterministically or refuse     | Semantic contract; refusal over improvisation              | Warehouse or semantic product       |
| CDC pipeline        | Keep indexes fresh at decision cadence                      | Freshness lag as a monitored service level objective (SLO) | Existing streaming or batch estate  |
| Catalog and lineage | Supply ownership, definitions, and lineage as context       | Definition authority                                       | Existing catalog                    |
| Provenance store    | Bind every claim to its source span                         | Citability by construction                                 | With the index                      |

## Mechanisms

### ACL-aware retrieval is deterministic security applied to grounding

**In short:** Check who is asking before searching, so an agent can never surface a document its user could not open.

ACL-aware retrieval checks the access control list (ACL), the record of who may open each document, before returning results. The shipped pattern: crawl source permissions into index metadata, then filter **inside** the vector query on the caller's live identity. Document-level directory ACLs are native on the major search platforms. Connector-crawled permission maps ship with fail-close behaviour: on an error, they deny rather than allow. Relationship-based authorisation engines of the Zanzibar class pre-compute the authorised objects for the hard cases. **Filtering after the search is the anti-pattern.** It leaks result counts and starves the result set. Four named failure modes survive a correct implementation and must be designed for. First, permission-sync lag: a revoked permission takes effect at the next crawl, not at the click. Second, group-membership drift. Third, documents with no ACL defaulting to public. Fourth, inherited oversharing, where agents amplify a decade of accumulated permission sprawl. Vendor-published estimates put roughly 16 percent of business-critical data in an overshared state. The mitigation shipped by one major vendor is a scoped-search allowlist that its own documentation calls a stopgap. Hygiene comes before retrieval. No retrieval layer fixes wrong ACLs.

### Embeddings are recoverable data

**In short:** The numeric form of a document can often be turned back into its text, so it needs the same protection as the document.

Exact reconstruction of short inputs from their embeddings has been demonstrated at 92 percent. The result is vec2text, presented at the Empirical Methods in Natural Language Processing conference (EMNLP) in 2023 and reproduced in 2025. The architectural consequence is not optional. Vectors inherit the source's classification, ACLs, residency rules, and privacy obligations. Erasure cascades into vectors and every derived artifact: delete the record, and every copy made from it goes too. This is the reasoning behind the named risk in the OWASP (Open Worldwide Application Security Project) application list. Treat an index as a copy of the data, because that is what it is.

### Semantic contracts convert silent errors into refusals

**In short:** Fixed business definitions turn a confidently wrong number into either the right number or an honest refusal.

For high-stakes numeric questions, the value of a governed semantic layer (a shared set of business definitions) is not a few points of accuracy. It is failure-mode conversion: a wrong number becomes either a refusal or a deterministic answer. Ontology-checked querying moved accuracy from 54 percent to 72 percent. It also produced explicit "I do not know" responses on about 8 percent of questions, which is the property that matters. A vendor's paired benchmark compares a semantic layer against text-to-SQL, where the model writes Structured Query Language (SQL) database queries directly. It reports 98 to 100 percent accuracy through the semantic layer on the modelled scope, against 84 to 90 percent for text-to-SQL. The semantic layer covered 72.7 percent of the full question set \[vendor]. A semantic-document approach added 17 to 23 points across three frontier models \[vendor]. The honest counter-camp reaches comparable accuracy through disciplined data modelling alone. It argues that good modelling **is** the semantic layer. The floor everyone should know: on the hardest public text-to-SQL benchmark, frontier models score between single digits and the low twenties, in percent. On its predecessor they score above 90 percent.

### The retrieval substrate ladder

**In short:** Start with the simplest storage that fits the number of documents, and move up only when measurements say so.

The ladder has rungs with thresholds, because "which vector database" is the wrong first question. Below roughly 100,000 vectors, brute-force search is enough. Postgres with the pgvector extension serves roughly 1 to 10 million vectors. At 1 million it answers in under 20 milliseconds with above 95 percent recall (the share of relevant items it finds). Index-build pain appears around 2 million, and partitioning becomes necessary past 5 million. Scale-out Postgres extensions reach roughly 50 million. Published comparisons show large advantages at 99 percent recall against a managed peer, at lower cost \[vendor]. The advantages are in p95 latency (the time within which 95 percent of queries return) and in queries per second (QPS). Dedicated or managed engines earn the top rung for extreme scale, heavy write rates, or filter-heavy multi-tenancy (many tenants on one index). Take 100 million vectors with filters that select 20 percent of the data. There, Postgres p99 latency (the time within which 99 percent of queries return) runs several times that of a purpose-built engine. Two operational cautions decide real migrations. Index builds consume tens of gigabytes of memory (RAM) for hours. Filtered search has recall cliffs: past certain filters, it suddenly misses relevant items. Vector storage on object stores has reached general availability at up to 90 percent lower cost \[vendor]. That tilts the economics toward more, smaller, purpose-scoped indexes rather than one large one.

### Freshness is a cost decision, not a virtue

**In short:** Keep data as fresh as the decisions need, because instant updates cost far more than near-instant ones.

Change data capture feeding incremental indexing delivers freshness measured in minutes at close to batch cost. One documented like-for-like requirement priced at about $400 per month as a five-minute batch, against about $7,600 per month as streaming. Streaming commonly runs an order of magnitude (roughly ten times) above batch. Streaming is earned by decision cadence: fraud, operational triage, inventory. The failure mechanism to design against is specific. Similarity ranking ignores time, so a superseded document outranks its current replacement unless freshness or validity is part of the ranking.

### Re-embedding is the hidden line item

**In short:** Changing the model behind the fingerprints means redoing every document, which costs real money and needs a plan.

Model upgrades force a re-embed of the full corpus. Reference costs run from hours on multi-GPU (graphics processing unit) hardware to four figures through an API (application programming interface). The operational discipline has four parts. Version-stamp every vector. Run blue/green index migrations: build the new index beside the old one and switch over only when it passes. Evaluate embedding models quarterly. Migrate only for eval gains (gains on test tasks with known right answers) above a stated threshold, and 5 percent is the working figure. Cross-model conversion, published at roughly 100 times cheaper than re-embedding, is worth testing before any large migration. Re-embed changed chunks (the pieces documents are split into) continuously, and keep a periodic full re-index as the recovery baseline.

## Design decisions

* **Semantic-layer product vs governed views** ([CD-8](https://www.agenticarchitectureskills.com/decisions#cd-8)): decided per use case, by failure mode rather than by accuracy points. The binding variable is curated business context.
* **Dedicated vector database vs the simplest substrate** ([CD-9](https://www.agenticarchitectureskills.com/decisions#cd-9)): climb the ladder above one rung at a time. Prefer the vector capability bundled with the platform where the corpus already lives. Governance and ACL inheritance then come free.
* **Data mesh vs governed central substrate** ([CD-10](https://www.agenticarchitectureskills.com/decisions#cd-10)): mesh ideas on a governed substrate. Every shipped ACL-sync architecture assumes a governed central index.
* **Real-time vs batch grounding** ([CD-12](https://www.agenticarchitectureskills.com/decisions#cd-12)): CDC is the default. Streaming is earned by decision cadence.
* **One universal index vs use-case-scoped** ([CD-11](https://www.agenticarchitectureskills.com/decisions#cd-11)): two layers. The detail is resolved on [R14](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering), the agent data engineering page.

## Cross-cutting concerns

| #   | Concern                | Treatment at this layer                                                                                                                  |
| --- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| C1  | Identity and access    | ACLs crawled into index metadata; pre-filtered retrieval on live identity; relationship-based pre-computation; fail-close on sync errors |
| C2  | Observability          | Retrieval traces, permission-sync lag metrics, freshness telemetry per index                                                             |
| C3  | Traceability and audit | Answer-to-source-span provenance; embedding model version stamps; lineage carried into agent context                                     |
| C4  | Grounding              | The layer's whole purpose: curated context, semantic contracts, refusal over improvisation                                               |
| C5  | Impersonation          | Source authenticity via connector provenance; no unattributed corpora in grounding                                                       |
| C6  | Sovereignty            | Indexes and embeddings carry source residency; region-scoped indexes; derived artifacts inherit the strictest classification             |
| C7  | Privacy                | Embeddings treated as personal data where sources are; erasure cascades to vectors and derived artifacts; minimisation at index scope    |
| C8  | Safety and oversight   | High-stakes numeric answers gated by semantic contracts; refusal behaviour monitored                                                     |
| C9  | Cost                   | Re-embedding and index costs per corpus; freshness cost against decision cadence                                                         |
| C10 | Resilience             | Blue/green index migrations; degraded-mode retrieval; periodic full re-index as the recovery baseline                                    |

## Evidence and limits

The vec2text reconstruction result, the ontology-checked accuracy figures, and the substrate benchmarks are peer-reviewed or reproducible. The semantic-layer coverage comparisons and the substrate performance claims are vendor-published and flagged as such. The oversharing percentage is secondary-sourced and carried with that status. Two refusals. First, a widely circulated projection says that a majority of agentic analytics projects relying solely on tool protocols will fail by 2028. It is secondhand, with no located primary source, and this guide excludes it. Second, the substrate ladder's rung thresholds are working figures from published benchmarks, not guarantees for your corpus, so measure before you migrate. Re-verify quarterly: platform vector general-availability states, semantic interchange specification adoption, and embedding model releases that would trigger a re-embed decision.

**The research behind this page**

* [Data platform findings](https://www.agenticarchitectureskills.com/library/layers/r02-data-platform/findings)
* [Sources](https://www.agenticarchitectureskills.com/library/layers/r02-data-platform/sources)
* [Products named for orientation](https://www.agenticarchitectureskills.com/architecture), on the one-page wall chart
