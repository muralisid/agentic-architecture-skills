# Text embeddings: search by meaning

Make differently worded passages discoverable while preserving exact evidence.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/memory/text-embeddings (Markdown: https://www.agenticarchitectureskills.com/memory/text-embeddings.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

“Pump pressure is falling” and “low discharge pressure” may belong near each other even though their words differ. This helps find relevant procedures or earlier incidents. An exact asset number, policy version, or quantity still needs an exact check.

**Figure: Text: find related meaning.** Text similarity helps locate a passage. It does not establish whether that passage is current or applicable.

**What the image shows:** Text encoder maps two differently worded pump-pressure passages near each other and a leave-policy passage elsewhere. A query retrieves nearby passages while retaining the original source, version, and permissions.

Image: https\://www\.agenticarchitectureskills.com/images/memory/text-space-v1.webp

## What the space represents

The picture groups two ways of describing a pressure problem. It is a teaching example of semantic resemblance, not a claim about coordinates from a particular encoder. A text embedding can help retrieve a passage whose wording differs from the query. Sentence-BERT is one research example of training sentence representations for semantic comparison.

## What to retain beside the vector

Keep the document and passage reference, source version, applicable dates, language, entity identifiers, and permissions. Retrieve the original passage so the agent and reviewer can inspect what it says. Keep lexical search or exact queries for identifiers and other details that similarity alone does not settle.

## Where the first approach can fail

Embedding every document as one item may blur several topics together. Summarizing first may remove a qualification or unit. A passage about an old procedure can remain very similar to the replacement. Test those failures with the questions the agent must actually answer.

## How it serves a decision

For a pump investigation, semantic search can locate a relevant inspection method. The asset record and current procedure version establish applicability. The decision record cites the passage used, rather than an embedding distance.

Compare with keyword retrieval and ordinary chunks before adding extra representations. [Choose the representation](https://www.agenticarchitectureskills.com/memory/choosing-representations) and [prepare its sources](https://www.agenticarchitectureskills.com/memory/information-to-memory).

## External source

[Sentence-BERT](https://arxiv.org/abs/1908.10084), 2019. Reviewed 18 September 2026.
