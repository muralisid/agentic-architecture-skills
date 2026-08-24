# Why the view taxonomy comes from the corpus, not the goal

The evidence behind pattern 4. Showing the view designer a sample of the corpus is worth a great deal; telling it your goal costs you, and the harm grows with the amount of context supplied. Tested in five forms, ending on real human-judged instruction-following data, with the design rule each result produced.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/patterns/why-not-to-condition-on-the-objective (Markdown: https://www.agenticarchitectureskills.com/patterns/why-not-to-condition-on-the-objective.md)
Updated: 2026-08-23
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

> **In plain terms.**
>
> The promising version of the multi-card idea was that a model could decide which cards to build for a particular goal: different cards for legal discovery than for operations, for example. This page follows that idea through five rounds of testing. Each round fixed a real weakness in the previous one, and each round returned the same answer: views designed from the corpus itself are as good or better, and telling the designer the goal makes things worse. The one thing to remember: the goal is the wrong input for building the index, and a cheaper, established technique already does what this idea was meant to do.

## The claim and its five forms

**In short:** Five ways of letting the objective shape the index, five negative results.

| Round   | Form of conditioning                                                                                                                                        | Corpus                                               | Verdict                                                                                                                               |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | The designer is shown the corpus sample plus a narrow research objective; unguided topic model; no gate                                                     | Synthetic, two objectives over one corpus            | Objective made retrieval significantly worse; no cross-over of any size                                                               |
| 2 and 3 | Same, inside an objective-gated pool with guided topics and model-cleaned noise, after a declared repair of a degenerate topic model                        | Synthetic                                            | Cross-over held at two of three gate settings on one machine, zero of three on a second; the ladder changed sign across settings      |
| 4       | The designer is shown business context, then schema metadata, then the narrow objective, on a workload spanning six departments                             | Synthetic, 200 queries                               | Every level of added context made retrieval worse, monotonically; the preregistered stopping rule fired                               |
| 5       | The corpus is embedded once and its topics discovered once with no seeding; the objective enters only when a model selects views from that shared substrate | Synthetic, 5 topic-model seeds                       | Cross-over stable at one of five seeds                                                                                                |
| 5       | The same architecture on real news collections with two sets of human judgements per query                                                                  | FollowIR Core17 (20 queries) and News21 (32 queries) | Objective-selected views are the worst arm; a plain instruction-prepended encoder beats every card arm; instruction following is zero |

## Round 1: the thesis fails

**In short:** Corpus conditioning is worth a great deal; adding the objective subtracts from it.

The conditioning ladder varies only what the designer is shown. Every rung shares an encoder, a builder, and an index.

**Measured result: The conditioning ladder, round 1.** nDCG\@10 on synthetic workload A, 150 queries. Views designed from the corpus alone in the accent colour.

| Category                                | nDCG\@10 |
| --------------------------------------- | -------- |
| Pooled, one vector                      | 0.295    |
| Generic views (no corpus, no objective) | 0.449    |
| Matched blind chunks                    | 0.588    |
| Corpus sample plus the objective        | 0.605    |
| Corpus sample only                      | 0.673    |

Showing the designer the corpus is worth +0.224 over generic views (p=0.0001) and beats blind chunks. Adding the research objective costs −0.068 (p=0.002). The useful signal is the corpus, which is what published taxonomy-design systems already condition on.

**Source:** Benchmark repository, results/e\_dyn/hdyn3/metrics.json, commit 92c18cb (2026-08-22). Byte-identical on a second machine.

The cross-over test asks whether a taxonomy designed for objective A serves A's workload better than one designed for B, and vice versa. It found nothing: +0.020 (p=0.35) in one direction and −0.002 (p=0.92) in the other. Taxonomies designed under different objectives served each other's workloads indistinguishably. A sampler test in the same round, which stratified the designer's sample across discovered topics so that minority material could not vanish, did what it was designed to do (minority-topic coverage of the sample rose from 60 to 100 percent) and bought nothing in retrieval (−0.015, p=0.70); worse, it produced a significant gain on the balanced control corpus where the preregistration said the gap should vanish. An effect that appears where it should not and is absent where it should be is not the claimed mechanism.

An instruction-conditioned baseline in this round was unsound and is recorded as such: the encoder used fixed prefixes rather than following instructions, so prepending the objective to each query merely diluted it. That comparison measured query dilution, not instruction conditioning, and its nominal result is not used anywhere.

## Rounds 2 and 3: the pipeline as specified, and a fragile cross-over

**In short:** With the gate, guided topics, and noise cleaning restored, the cross-over appeared at two of three operating points on one machine, and at none of three on a second.

Round 1 had tested a stripped-down reconstruction: no relevance gate, no model guidance of the topic model, no model cleaning of clustering noise. Each of those plausibly explained the failure, since under partition-mode carding every span must land in some view, and a taxonomy aimed at three departments had to absorb the seven it was not aimed at. Round 2 restored all three, applied the gate identically to every arm, and scored both taxonomies over a common per-workload pool (scoring each over its own gated pool had let the gate carry the comparison, halving the effect when corrected). Round 3 repaired a degenerate topic model (3 topics against 12) that had been diagnosed in round 2's own metrics before any attempt to fix it.

| Gate keep rate | A direction (T\_A beats T\_B on A) | B direction (T\_B beats T\_A on B) | Both directions? |
| -------------- | ---------------------------------- | ---------------------------------- | ---------------- |
| 0.35           | +0.070 (p=0.0001)                  | +0.066 (p=0.0029)                  | Yes              |
| 0.50           | +0.114 (p=0.0001)                  | +0.035 (p=0.0153)                  | Yes              |
| 0.75           | +0.156 (p=0.0001)                  | +0.006 (p=0.59)                    | No               |

The A direction is robust everywhere and grows as the gate loosens. The B direction is fragile. Replicated on a second machine at the same commit, with the encoder on the CPU and a fixed hash seed, the B direction read −0.018 (p=0.32), +0.007 (p=0.65) and −0.040 (p=0.034, the wrong direction): zero of three. The mechanism is understood: dimensionality reduction and density clustering produce different topic models on a different processor architecture, the designer sees different samples and writes different view sets, and the B-direction effect depends on which view set it happens to write. The ladder over the same sweep read +0.019, −0.061 (p=0.0018) and −0.012: it changed sign across operating points, so the single-workload comparison cannot be quoted in either direction.

What rounds 2 and 3 established is narrower than the claim: conditioning produces genuinely different taxonomies, and in one direction each serves its own workload better. It did not establish that an objective-designed taxonomy beats a well-formed corpus-derived one on any workload.

## Round 4: more context, worse retrieval, and the stopping rule

**In short:** Business context and schema metadata, the conditioning signals an enterprise actually has, made retrieval worse in proportion to how much was supplied.

The maintainer's argument for this round was that enterprises do not organise data for one question; they organise a line of business's data so that several agents can ask many questions, and the conditioning signal available in practice is standing business context plus schema metadata rather than a narrow objective. The workload was built accordingly: 200 queries across six departments. The round was preregistered before implementation with a stopping rule: if context plus metadata did not beat the corpus sample alone, the programme would stop pursuing the conditioning claim.

**Measured result: Conditioning by level, on a workload spanning six departments.** nDCG\@10, 200 queries. Each level adds to the previous one. Corpus sample only in the accent colour.

| Category                                     | nDCG\@10 |
| -------------------------------------------- | -------- |
| Pooled, one vector                           | 0.303    |
| Matched blind chunks                         | 0.489    |
| Corpus sample only (30 stratified documents) | 0.562    |
| Plus business context                        | 0.515    |
| Plus schema metadata                         | 0.494    |
| Plus the narrow objective                    | 0.457    |

Context plus metadata against sample only: −0.068, 95 percent interval −0.090 to −0.046, p=0.0001. Business context alone: −0.047 (p=0.0001). The narrow objective on top: a further −0.037 (p=0.018). The harm is monotone in the amount of context supplied.

**Source:** Benchmark repository, results/e\_dyn3/round4.json, commit 92c18cb (2026-08-22). Replicated on a second machine with the same ordering.

The taxonomies show why. From the corpus alone the designer derived six views that followed the data (fault logs, system maintenance, financial risk, legal compliance, logistics and supply, IT incidents). Given the business narrative it produced four elegant views organised around the business (commercial agreements, operations and logistics, finance reporting, risk and compliance). The business framing covers the corpus less well, and on a workload spanning six departments coverage is what matters. The taxonomies were genuinely different (mean pairwise similarity 0.833, so the convergence condition did not fire) and genuinely worse. The stopping rule fired and the programme ceased pursuing the conditioning claim in that form.

## Round 5: the objective enters late, on real data

**In short:** Embedding once and selecting views per objective from a shared, unseeded topic substrate is the practical version of the idea. It does not carry the effect, and on human-judged data it is the worst arm.

The maintainer's final architecture separated two things that rounds 2 to 4 had conflated: conditioning the topic model on the objective (seed topics written from it) and conditioning the view design on it. In round 5 the corpus is embedded once and its topics discovered once with no seeding, a shared substrate reflecting the corpus alone; the objective enters only later, when a model selects and composes a view set from that substrate, and at the per-objective gate. The economic appeal is real: a new objective then costs a few model calls, not a new embedding pass. Preregistration was waived for this round at the maintainer's direction; rigour was held by fixing the decision rules in code before any number was read, requiring every verdict to hold across several topic-model seeds, and reporting every arm including the ones that beat the method.

On the synthetic corpus, with the validated card builder and five topic-model seeds, the two-sided cross-over held at one seed of five. The A direction was robustly positive (+0.034 to +0.099, significant in four of five); the B direction ranged from −0.038 to +0.025. The cross-over of round 3 had lived in the objective seeds, not in the idea; the practical embed-once version does not carry it.

FollowIR supplies the real test: news collections where each query comes with an instruction and two sets of human judgements, before and after the instruction changes, so an index that follows the objective can be told apart from one that ignores it. Five arms were scored: one pooled vector per document; the same encoder with the instruction prepended to the query (a weak instruction-conditioned baseline, since the encoder was not trained to follow instructions); matched blind chunks; a single objective-blind view set derived from the corpus; and the view set a model selected per instruction from the shared substrate.

**Measured result: FollowIR: five arms on human-judged news collections.** nDCG\@10 under each query's own original judgements. Core17: 20 queries, seed 13, validated concatenate-and-encode card representation. News21: 32 queries, mean of two substrate seeds.

| Category                              | Core17 | News21 |
| ------------------------------------- | ------ | ------ |
| Pooled, one vector                    | 0.393  | 0.386  |
| Instruction prepended to the query    | 0.394  | 0.416  |
| Matched blind chunks                  | 0.403  | 0.364  |
| Corpus-derived views, objective-blind | 0.409  | 0.327  |
| Objective-selected views              | 0.349  | 0.331  |

On Core17 the objective-selected views are the worst arm, 0.06 below the corpus-derived view set; a confirmation run with the fully validated card representation sharpened the gap rather than closing it. On News21 the instruction-prepended encoder is the best arm and every card arm is worst. Under the changed instructions the ordering is the same. The instruction-following score p-MRR is about zero for both instruction-aware arms: neither follows the instruction.

**Source:** Benchmark repository, results/e\_dyn4/core17\_concat\_confirm.json, results/e\_dyn4/followir\_core17.json, results/e\_dyn4/followir\_summary.json, and the News21 run, commit 92c18cb (2026-08-22).

Two caveats were recorded with the result, and both point the same way. The encoder is a weak instruction baseline; a retriever trained to follow instructions would widen the gap against the method, not narrow it. And the candidate pool depth and document length were capped for speed, identically across every arm. A third collection (Robust04) was not run once the direction was consistent across the synthetic test and two real collections; it would have added corroboration, not information.

## What this establishes

**Verdict: The objective is the wrong input for building the index.**

Conditioning the view design on the goal, in any of five forms, does not improve retrieval and generally harms it: by −0.068 in round 1, by −0.047 to −0.068 at each level of context in round 4, and by about −0.06 on real human-judged data in round 5. The cross-over that briefly appeared lived in the topic seeds and did not replicate across machines or seeds. Where the objective must shape retrieval, a retriever trained to follow instructions is the established, cheaper tool, and even an untrained encoder with the instruction prepended beat every card arm on one real collection. The one durable positive is that a view set derived from the corpus alone stays competitive with chunks and pooling, and that is not new.

\[Evidence status: Independently measured] Synthetic results across seeds and machines; FollowIR with human judgements.

**The research behind this page**

* Benchmark repository: `results/e_dyn` (round 1), `results/e_dyn2` (rounds 2 and 3, pre- and post-repair), `results/e_dyn3` (round 4), `results/e_dyn4` (round 5), commit 92c18cb, 2026-08-22.
* Weller et al., FollowIR, EMNLP 2024, for the collections and the p-MRR score. [https://arxiv.org/abs/2403.15246](https://arxiv.org/abs/2403.15246)
* Promptriever (ICLR 2025), INSTRUCTOR (ACL Findings 2023), GSTransform (2025), CAMI (2026) and TnT-LLM (KDD 2024), the prior art that subsumes this idea, on the [reading list](https://www.agenticarchitectureskills.com/patterns/reading-list).
* [How the programme was run](https://www.agenticarchitectureskills.com/patterns/how-to-test-a-context-design) for the preregistration, its waiver, and the cross-machine replication.
