# Keep current facts and history distinct

Separate event time, arrival time, and the period a fact applies to.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/memory/changing-facts (Markdown: https://www.agenticarchitectureskills.com/memory/changing-facts.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

On Monday, an inspection is due. It is completed on Tuesday, but its report arrives on Friday. A question about Monday and a question about today need different answers. Simply choosing the last document received does not solve either question reliably.

**Figure: A fact has a time and a source.** Teaching illustration. The example is a proposed design, not a measured deployment.

**What the image shows:** An inspection is due Monday, completed Tuesday, and reported Friday. Questions about Monday and after Tuesday follow different evidence. Event time differs from the time the report arrives.

Image: https\://www\.agenticarchitectureskills.com/images/memory/memory-time-v1.webp

## Preserve the episode without freezing the status

Keep the due notice and completion event as history. Derive current status from applicable, verified evidence. Completion of an inspection does not by itself establish that every finding was resolved.

An episodic record preserves the event. A current fact or entity profile may need an update. A procedure changes only through its own approval process. These are different consequences of the same new evidence.

## Record the dates that matter

Retain when an event occurred, the period a statement applies to, and when the system received or recorded it. Include the source version. A late report can change our understanding of the past without becoming a new event in the present.

## Treat corrections differently from new events

A corrected asset identifier may invalidate earlier joins. A revised completion date may change which procedure was applicable. Track affected indexes, extracted facts, summaries, and retained task context, then update or invalidate them.

Preserve the correction history where policy allows. Do not keep exposing information that must be removed merely to preserve an audit trail.

## Keep unresolved contradictions explicit

Check source authority, scope, date, and support. Do not overwrite a fact because a new generated statement sounds more confident. When evidence cannot resolve the conflict, report the disagreement and which decision depends on it.

## Test time as part of memory quality

Include questions about past status, present status, delayed reports, revised procedures, and expired sources. LongMemEval explicitly evaluates knowledge updates and temporal reasoning in conversational memory: [paper](https://arxiv.org/abs/2410.10813), first published 2024, reviewed 18 September 2026. The enterprise timeline here is illustrative.

**Continue the story:** [Decide who can retain and recall it](https://www.agenticarchitectureskills.com/memory/permissions-and-lifecycle).
