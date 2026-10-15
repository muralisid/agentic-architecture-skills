# Where the cost saving really comes from

A cheap first-pass filter tells relevant from irrelevant email well, but removes only a third of the documents. The real saving comes from paying the model per topic, not per document. It is about two hundred times cheaper, and the factor does not grow with size.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/patterns/gate-and-economics (Markdown: https://www.agenticarchitectureskills.com/patterns/gate-and-economics.md)
Updated: 2026-10-15
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

Reading every document with a large model is costly. A common design runs in two passes. A cheap filter goes over everything first. The expensive model then reads only what survives, grouped into topics. We asked where this design actually saves money. The filter works, but at the recall you need it removes only about a third of the documents. The big saving comes from paying the model per topic instead of per document. That is about two hundred times cheaper. The factor stays roughly constant as the collection grows.

Recall is the share of relevant documents a filter keeps. The two-pass design sets the cost of preparing [knowledge and memory](https://www.agenticarchitectureskills.com/memory) for agents at scale. The documents usually sit in the [data platform layer (R02)](https://www.agenticarchitectureskills.com/layers/r02-data-platform). The [agent data engineering layer (R14)](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering) runs the filter and the topic work. The filter and the topic work sit early in the [data-to-memory pipeline](https://www.agenticarchitectureskills.com/architecture/data-to-memory).

## Step 1: does the filter tell relevant from irrelevant?

Yes. The on-purpose set is 4,000 messages from a public company email collection (Enron). The off-purpose set is 4,000 posts from unrelated Usenet newsgroups, an old public discussion forum. Where each item came from gives exact labels at no cost.

The filter is what we call a gate. It works on vectors, lists of numbers that stand for each item's meaning. Three sets of anchor phrases describe parts of the purpose. An anchor phrase is a short description the filter compares each item against. Each item scores the mean of its best few matches to each set. We fitted the combination on one half of the data and report results on the other half.

The filter scores ROC-AUC 0.933 on the held-out half. ROC-AUC is a 0 to 1 score of how well a filter ranks relevant items above irrelevant ones. 0.5 is a coin toss. At the target recall of 0.95, the filter keeps 66 percent of the documents and sets the rest aside. Precision at that point is 0.71. Precision is the share of kept items that are relevant.

| Measure                           | Value | Note                                                                                        |
| --------------------------------- | ----- | ------------------------------------------------------------------------------------------- |
| Held-out ROC-AUC                  | 0.933 | PR-AUC 0.935. The first pass is a filter, not a sample.                                     |
| Equal anchor weights              | 0.931 | Fitting the weights is worth 0.002. The power comes from having several anchor sets at all. |
| Deliberately irrelevant anchors   | 0.860 | Three sets of off-purpose phrases still reach 0.860. The data is already easy to separate.  |
| Logistic regression, same vectors | 0.995 | A simple trained classifier on the raw vectors beats the anchor filter by 0.062.            |

Two checks matter more than the headline. First, fitting the anchor weights is worth almost nothing. Equal weights give 0.931 against 0.933.

Second, a reviewer added a null control that the original design lacked. A null control is a version that should not work. Three sets of deliberately irrelevant anchors still reach ROC-AUC 0.860. One purpose-specific set alone reaches 0.852. Plain logistic regression on the raw vectors reaches 0.995. Logistic regression is a simple classifier trained on labelled examples. So most of the filter's power comes from the data being easy to separate. Where labels exist, a trained classifier on the same vectors is far better.

## Step 2: how much does the filter remove?

At the recall a production filter must hold, it removes about a third. At 0.99 recall, it removes about an eighth.

**Measured result: Share of documents the filter discards, by recall target.** Held-out half of the email-against-Usenet data. Precision at each point is in the table view.

| Category                     | Percent of documents discarded |
| ---------------------------- | ------------------------------ |
| Recall 0.80 (achieved 0.781) | 57.7                           |
| Recall 0.90 (achieved 0.901) | 46.5                           |
| Recall 0.95 (achieved 0.954) | 33.7                           |
| Recall 0.98 (achieved 0.981) | 20.0                           |
| Recall 0.99 (achieved 0.993) | 12.1                           |

A first pass saves money in proportion to what it removes. At recall 0.95 the filter removes a third. At 0.99 it removes an eighth. That is a saving factor between one and two, paid for with recall.

**Source:** Author-reported experiment, August 2026. The comparison and limitations are described on this page.

A first pass is often described as discarding most of a collection. On this evidence it does not. The large saving in a two-pass design comes from somewhere else. It comes from tying model cost to the number of topics found, not the number of documents. Crediting the filter overstates the filter. It also hides the real cause of the saving.

One caveat limits the result from above. Telling company email from Usenet is easier than sorting material inside one collection. A real filter faces the harder task. Failing this easy test would have ruled the filter out. Passing it is needed, but it is not enough.

## Step 3: the bill, measured

At similar topic detail, the two-pass design costs about two hundred times less than sending every document to a model. The claim that this advantage grows with size did not survive.

Nothing here is a rule of thumb. Token counts come from a real tokenizer run over the real documents. A token is a small piece of text that models charge by. The number of model calls comes from actually running the filter and the clustering at each size. So the topic count K is measured, not assumed.

Only the per-token prices are external. They come from a published price table dated 2026-08-19. The prices are listed in the results so readers can change them. Encoder compute is priced at zero. The encoder is the model that turns text into vectors. Pricing it at zero flatters the ratio, and we say so.

Our first run seemed to show a scaling law. Topics grew as N to the power 0.52, where N is the number of documents. The cost advantage widened as N to the power 0.44. We then reran the costs at two clustering settings, with topic coverage reported beside cost. That reversed the finding.

**Measured result: Cost advantage of the two-pass design by collection size, at two levels of topic detail.** Full-model cost divided by two-pass cost. Enron, 500 to 20,000 messages. Coarse clustering (minimum cluster size 25) against useful detail (minimum cluster size 10).

| Messages in the collection | Coarse clustering | Useful detail |
| -------------------------- | ----------------- | ------------- |
| 500                        | 325               | 216           |
| 1,000                      | 586               | 861           |
| 2,000                      | 1481              | 1505          |
| 5,000                      | 947               | 418           |
| 10,000                     | 1824              | 152           |
| 20,000                     | 1841              | 204           |

With coarse clustering the advantage grows (N to the power 0.44). That is because the clusters get coarser as the collection grows. 14 topics over 10,000 messages, at 485 documents per topic, summarise nothing useful. At useful detail, topics grow faster than the collection (N to the power 1.25). The advantage then shrinks (N to the power -0.27). What remains is a constant factor of about two hundred.

**Source:** Author-reported experiment, August 2026. The comparison and limitations are described on this page.

Coverage is the share of surviving documents that land in any topic.

| Messages | Topics, coarse | Coverage of survivors, coarse | Topics, fine | Coverage, fine | Documents per topic, fine |
| -------- | -------------- | ----------------------------- | ------------ | -------------- | ------------------------- |
| 500      | 2              | 49.6%                         | 3            | 54.0%          | 45                        |
| 2,000    | 2              | 59.8%                         | 2            | 78.6%          | 393                       |
| 5,000    | 7              | 97.6%                         | 16           | 97.1%          | 152                       |
| 10,000   | 7              | 94.8%                         | 88           | 32.1%          | 18                        |
| 20,000   | 14             | 67.9%                         | 132          | 26.3%          | 20                        |

Coverage shows how coarse the coarse setting is. It also shows that the exponents depend on a clustering setting, not on the design. On a second machine, the steps that shrink and cluster the vectors produced different topics. The fitted exponents moved again, to 0.27 and 0.71 at the original setting. The exponents are a side effect of clustering. The constant factor is not.

Two more caveats stand. The two designs produce different things. A topic-level summary of a collection is not an understanding of each document. So the ratio applies to finding topics, not to reading. And pricing local encoder compute at zero overstates the saving for anyone who rents that compute by the hour.

## A worked example

Take an energy retailer's customer inbox. A cheap filter can set aside newsletters and spam, but it will likely keep most of the mail. The real saving comes next. Group the remaining complaints into topics, and pay the model once per topic to name and summarise each one. This example shows the shape of the design. We tested it on Enron email, not on a retailer's inbox.

## What we conclude

**Verdict: A real constant saving, and a filter that sets material aside.**

Processing the topics found in the data, instead of each document, is about two hundred times cheaper at similar detail. That is the saving. The filter is worth building to set material aside against a recall target. It contributes a factor of one to two. It is not where the large saving comes from. Where a labelled sample exists, a trained classifier on the same vectors beats hand-weighted anchors by a wide margin. We withdraw the scaling law.

## Evidence and limits

\[Evidence status: author-measured] Exact labels from where each item came from. Measured token counts. Dated public prices.

We reran the work on a second machine. Nobody else has repeated it yet. The filter test used one easy split, company email against Usenet. Prices are as of 2026-08-19, and local compute is priced at zero.

## Next step

See how to choose the ten results that reach the agent, in [choosing varied results](https://www.agenticarchitectureskills.com/patterns/diversity-and-consumer). Or go back to the [nine context patterns](https://www.agenticarchitectureskills.com/patterns).

**Explore this topic**

* TnT-LLM (KDD 2024), Databricks (Jul 2026) \[vendor] and Distilling Step-by-Step (ACL Findings 2023). They give the published economics of letting a model design and cheap tools do the bulk work. All are on the [reading list](https://www.agenticarchitectureskills.com/patterns/reading-list).
* Prices from a published price table dated 2026-08-19. The experiment ran in August 2026.
