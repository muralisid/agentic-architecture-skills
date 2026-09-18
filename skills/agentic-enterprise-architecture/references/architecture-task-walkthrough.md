# Follow one inspection task

See how evidence, reasoning, permission, action, and confirmation fit together.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/architecture/task-walkthrough (Markdown: https://www.agenticarchitectureskills.com/architecture/task-walkthrough.md)
Updated: 2026-09-17
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

**Figure: One inspection task, end to end.** Permission is checked before an action; evidence and human responsibility span the task.

**What the image shows:** Request: Inspect this asset. Evidence: Read records and images. Investigation: Check what is missing. Allowed action: Create an inspection. Confirmation: Record the result

Image: https\://www\.agenticarchitectureskills.com/figures/architecture/agent-task.svg

## 1. Give the task an owner and a boundary

“Investigate possible vegetation risk on this circuit and prepare inspection requests.” Record the circuit, deadline, allowable systems, and the person responsible. The task permits an inspection request, not equipment switching or tree removal.

## 2. Gather evidence

Read asset coordinates, image dates, previous inspections, and current work orders. Keep the original image reference and the date of each observation. A location match is a candidate association until checked against the asset record.

## 3. Resolve the missing information

If the imagery is too coarse or too old, seek better observations or propose a field inspection. If a work order already exists, link the finding to it. A repeated investigation should ask a specific question each time, not collect data without a stopping rule.

## 4. Request the permitted action

The model proposes a structured inspection request. The work-order service checks permissions, required fields, duplication, and any review requirement. The agent cannot grant itself more authority by changing its prompt.

## 5. Confirm and report

Read the accepted work-order identifier and status. A successful API request is not proof that a field inspection occurred. Report what was created, what still needs review, and what evidence supports the priority. An independent action record supports later investigation.

## When to stop

Stop when an inspection request is confirmed, a duplicate is resolved, the evidence is insufficient, the time or cost limit is reached, or a responsible person must decide. Preserve enough state to resume without repeating a completed action.

## Apply the design

Explore [vegetation inspection](https://www.agenticarchitectureskills.com/use-cases/vegetation-inspection), [integration and tools](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric), and [official records](https://www.agenticarchitectureskills.com/layers/r04-systems-of-record). The repeated investigation is an application of the reasoning-and-action pattern described in ReAct; the specific operational design here is a proposal.

## External sources

* [ReAct: reasoning and acting with language models](https://arxiv.org/abs/2210.03629). Accessed 17 September 2026.
