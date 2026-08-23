# The multi-card retrieval experiments

Five rounds of experiments on public corpora, with human relevance judgements, testing whether several purpose-specific embeddings per document beat one, whether a cheap gate and topic-level processing pay for themselves, and whether telling the index the goal helps. What held, what did not, and the approach the evidence supports.

Source: https://www.agenticarchitectureskills.com/research (Markdown: https://www.agenticarchitectureskills.com/research.md)

> **In plain terms.**
>
> Most search systems turn each document into one numeric fingerprint, an embedding. A document that is about several things then gets an average of all of them. This section reports a programme of experiments that tested a different design: several fingerprints per document, one per purpose, plus a cheap first-pass filter, topic-level processing instead of document-level processing, and a selection rule that changes with who will read the results. Every experiment ran on public data with fixed seeds, so anyone can rerun it. The one thing to remember: the parts that worked are the ordinary parts (several vectors beat one; keyword search still matters), and the parts that were meant to be new did not survive testing.

## The question

**In short:** Does giving each document several purpose-specific embeddings, designed with a model and executed with classical machinery, beat the usual single vector, and does it pay?

The pattern under test came from the authors' production experience in the social media domain, where it replaced reading every post with a frontier model. It is treated here as a hypothesis validated in one domain and tested on public corpora only. Four claims were separated and tested one at a time:

1. **Aspect dilution.** A pooled vector of a multi-aspect document matches each aspect weakly; several purpose cards keep each aspect addressable. Tested on a synthetic corpus where the number of aspects is a dial, on a published stress test, and on human-judged scientific abstracts.
2. **The cheap gate and the bill.** A relevance gate built from embeddings alone can discard off-purpose material before any expensive step, and processing discovered topics instead of documents makes the cost advantage widen with corpus size. Tested on 20,000 corporate emails.
3. **Diversity for the consumer.** The right amount of diversity in a result set depends on whether a model or a person will read it. Tested with a constructed coverage task and a consumer study judged by three model families.
4. **Objective conditioning.** Telling the view designer the goal (the research objective, the business context, the schema) produces an index that serves that goal better than a corpus-derived one. Tested in five forms over five rounds, ending on real human-judged instruction-following data.

## The five rounds at a glance

| Round  | What was tested                                                                      | Corpus                                                  | Verdict                                                                                                       | Page                                                                                                                                                               |
| ------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1      | Several vectors per document against one; purpose cards against matched blind chunks | Synthetic (aspects as a dial), LIMIT, SciFact           | Multi-vector wins decisively; purpose framing wins only when queries target one aspect                        | [Aspect dilution](https://www.agenticarchitectureskills.com/research/aspect-dilution), [Real prose](https://www.agenticarchitectureskills.com/research/real-prose) |
| 1      | The cheap gate; the two-pass economics                                               | Enron email against Usenet                              | The gate discriminates but discards little at high recall; the saving is a constant factor, not a scaling law | [Gate and economics](https://www.agenticarchitectureskills.com/research/gate-and-economics)                                                                        |
| 1      | Diversity policies; the consumer-dependent flip                                      | Constructed coverage task; 60 synthesis tasks, 3 judges | The harvest sits on the efficient frontier; the consumer flip is not supported                                | [Diversity and the consumer](https://www.agenticarchitectureskills.com/research/diversity-and-consumer)                                                            |
| 2 to 4 | Conditioning the view design on the objective, then on business context and schema   | Synthetic, two objectives over one corpus               | No stable effect; harm grows with the amount of context supplied; the stopping rule fired                     | [Objective conditioning](https://www.agenticarchitectureskills.com/research/objective-conditioning)                                                                |
| 5      | Selecting views late from a shared substrate, on real instruction-following data     | Synthetic (5 seeds), FollowIR Core17 and News21         | Objective-selected views are the worst arm; a plain instruction-prepended encoder beats every card arm        | [Objective conditioning](https://www.agenticarchitectureskills.com/research/objective-conditioning)                                                                |

| Measure                     | Value          | Note                                                                                                                     |
| --------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------ |
| One vector, aspects 1 to 10 | 0.815 to 0.294 | nDCG\@10 of the pooled index as a document grows from one aspect to ten. Several vectors per document hold it near 0.74. |
| Cards over matched chunks   | +0.188         | At ten aspects per document, when queries target one aspect, with 25 percent fewer embeddings than the chunk control.    |
| Cards under matched chunks  | −0.032         | On human-judged scientific abstracts, where a query concerns a whole finding rather than one aspect.                     |
| Objective conditioning      | 0 of 5         | Forms of telling the index the goal that produced a stable benefit. On real data it cost about 0.06 nDCG\@10.            |

## What held and what did not

**Held: Four findings survived every check.**

* Several embeddings per document beat one on aspect-rich material, by any method of splitting the document.
* Purpose alignment helps when the card taxonomy matches what queries ask about, and hurts when it does not. Both sides are measured.
* A cheap embedding-space gate discriminates (ROC-AUC 0.933), and processing topics rather than documents is about two hundred times cheaper at comparable topic granularity.
* Harvesting the low-similarity tail of a gated pool buys sub-topic coverage about twice as cheaply as maximal marginal relevance, and produces summaries with less unsupported content.

**Did not hold: Four claims are withdrawn.**

* "Alignment, not count" as an unconditional claim. A blind three-word sliding window recovers 0.610 of the 0.674 that purpose cards gain on LIMIT; most of the benefit is capacity.
* The economics scaling law. At a fixed useful topic granularity the cost advantage shrinks with corpus size (N to the power −0.27). A large constant-factor saving remains.
* The gate as the source of the saving. At recall 0.95 it discards 33.7 percent of a corpus; at 0.99, 12.1 percent.
* Consumer-dependent diversity and objective-conditioned views, the two ideas the programme was built to prove. Neither produced evidence that survives a cross-family judge or real human-judged data.

## How to read the numbers

**In short:** Every comparison is a paired test over the same queries, the control arm always gets the same budget as the method, and every headline had to hold across seeds and on a second machine.

* The retrieval metric is nDCG\@10, reported with 95 percent bootstrap intervals and paired permutation p-values, Holm-corrected wherever several comparisons run together. Wins, ties, and losses over the query set are recorded beside every delta.
* Every experiment carries three arms: one pooled vector, the same text cut into blind fixed-size windows, and the same text split by purpose. The gap between pooled and chunk is what more embeddings buy; the gap between chunk and card is what purposes buy. Only the second gap is the hypothesis, and the chunk control is matched on units per document. Getting that wrong was the single largest error in the programme, and it is described on the [method page](https://www.agenticarchitectureskills.com/research/method-and-reversals).
* The corpora form a ladder of realism, so a technique that works only on the top rung is an artefact of the test rather than a technique.

| Corpus                    | What it is                                                                                             | Why it is in the study                                                                                   |
| ------------------------- | ------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| Synthetic                 | Documents built from k passages drawn from k unrelated topic pools; a query targets one fact           | The best case: aspects genuinely exist, queries genuinely target them, and k is a dial                   |
| LIMIT (small)             | 46 documents, each a person and 44 things they like; 1,000 queries ask who likes one thing             | A published stress test designed to break single-vector retrieval; the decomposition is free and perfect |
| SciFact                   | 5,183 scientific abstracts, 300 real claims, human relevance judgements                                | The honest case: real prose, real labels, and queries about a whole finding rather than one aspect       |
| Enron                     | 20,000 corporate emails                                                                                | The enterprise case, used for the gate and the cost study                                                |
| FollowIR (Core17, News21) | News collections with two sets of human judgements per query, before and after the instruction changes | The real test of whether an index can follow a stated objective                                          |

## Reproducibility

**In short:** One command per experiment, seeded, cached, and byte-identical between runs.

Every number on these pages is produced by one command against committed code and seeds. Two seeded runs must produce byte-identical per-query output, and a test enforces it; reaching that required accumulating similarities in double precision, because a single-precision matrix product varies by around one part in a hundred million with the reduction order, enough to move a value across a rounding boundary. Generative calls are metered and cached; the design and judging calls for a full round cost between a tenth of a cent and ten US cents. Per-query scores are released alongside the aggregates so the significance tests can be recomputed independently. The experiment code and every artifact live in the benchmark repository, `multicard-bench`, which is released with the write-up.

Two machines were used, an Intel Mac and an Apple Silicon Mac, and the replication found two harness defects that are also documented on the [method page](https://www.agenticarchitectureskills.com/research/method-and-reversals): a GPU encoder path that silently produced different vectors, and an unfixed hash seed that changed which training queries a designer saw.

## Where to go next

* [Aspect dilution: several vectors beat one, and why](https://www.agenticarchitectureskills.com/research/aspect-dilution)
* [Real prose: where purpose views lose](https://www.agenticarchitectureskills.com/research/real-prose)
* [The cheap gate and the bill](https://www.agenticarchitectureskills.com/research/gate-and-economics)
* [Diversity, and who consumes the results](https://www.agenticarchitectureskills.com/research/diversity-and-consumer)
* [Objective conditioning: five rounds, five forms, no effect](https://www.agenticarchitectureskills.com/research/objective-conditioning)
* [How the programme was run, and how it caught its own errors](https://www.agenticarchitectureskills.com/research/method-and-reversals)
* [The recommended approach](https://www.agenticarchitectureskills.com/research/recommended-approach), with the evidence behind each recommendation
* [The papers behind the recommendation](https://www.agenticarchitectureskills.com/research/reading-list)

**The research behind this page**

* The benchmark repository (`multicard-bench`), results directory, commit 92c18cb, 2026-08-22: one `metrics.json` and one `per_query.csv` per experiment.
* The programme's hypothesis register and findings summary, 2026-08-20 to 2026-08-22, held privately until the write-up is released.
* [The data-to-memory pipeline](https://www.agenticarchitectureskills.com/architecture/data-to-memory) and [agent data engineering](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering), where the pattern sits in the architecture.
