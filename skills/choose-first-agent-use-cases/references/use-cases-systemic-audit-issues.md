# Investigate recurring audit issues

Use patterns across sites to ask better questions and test possible systemic causes.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/use-cases/systemic-audit-issues (Markdown: https://www.agenticarchitectureskills.com/use-cases/systemic-audit-issues.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

Similar findings across sites can be worth investigating, but similar wording is not enough to establish a common cause. This proposed agent searches for evidence that supports or challenges each explanation.

## See the work first

**Figure: Investigate recurring audit issues.** Proposed agent extension. Each action remains within an explicitly permitted business process.

**What the image shows:** Find patterns across sites, state competing explanations, investigate evidence and counterexamples, and report support and uncertainty.

Image: https\://www\.agenticarchitectureskills.com/images/use-cases/systemic-audit-issues-v1.webp

**Experience behind this example**

The author described using topic modeling on audit gaps and action details, particularly geotechnical audits, to look for systemic issues across sites. The proposed agent adds targeted follow-up investigation and tests competing explanations.

## Start with evidence

Keep finding text, site, audit scope, date, severity, action owner, closure evidence, and changes to the audit method. Clustered language is a starting point for investigation, not proof that several sites share a cause.

## What the agent adds

The agent can request maintenance history, inspection records, action closure evidence, or procedure changes relevant to a specific hypothesis. Keep a record of what would disprove the explanation. Check whether apparent recurrence comes from different audit coverage, copied wording, or inconsistent classification.

## How the investigation proceeds

For each hypothesis, specify the missing evidence and the next discriminating question. Search for sites that did not show the issue as well as those that did. Stop when the evidence supports a bounded conclusion, competing explanations remain unresolved, or the investigation budget is exhausted.

## Measure the business result

Measure expert agreement, useful issues discovered, false systemic conclusions, evidence completeness, and investigation effort. Compare with topic modeling plus expert review. A larger number of clusters or retrieved records is not the business outcome.

## Responsibility and failure handling

An engineering or assurance owner decides the response. The agent reports associations and uncertainty, not unproved causation. Keep site permissions and traceability across every combined source.

## Start with a bounded trial

Use a representative historical sample and an agreed reference outcome. Run the proposed process without making live operational changes. Review errors and costs with the people who will own the work. Move to a narrow live scope only when quality, permissions, recovery, and supervision are adequate.

## Explore the architecture

* [Intelligence & learning](https://www.agenticarchitectureskills.com/layers/r06-intelligence-and-learning).
* [Governance & risk](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty).
* [Data engineering for agents](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering).

Continue with [knowledge and memory](https://www.agenticarchitectureskills.com/memory), [value and investment](https://www.agenticarchitectureskills.com/use-cases/value-and-investment), or [practical skills](https://www.agenticarchitectureskills.com/skills).

## External sources

* [ReAct: reasoning and acting with language models](https://arxiv.org/abs/2210.03629). Accessed 17 September 2026.

Return to [Utilities](https://www.agenticarchitectureskills.com/use-cases/utilities) or [explore the agent roles](https://www.agenticarchitectureskills.com/use-cases/agent-roles).
