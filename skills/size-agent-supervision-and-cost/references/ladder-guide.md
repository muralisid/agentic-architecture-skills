# Intelligence ladder

How intelligent should an agent be, and what should that intelligence cost?

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/ladder (Markdown: https://www.agenticarchitectureskills.com/ladder.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

To turn an enterprise into an agentic enterprise, we need agents that can do useful work at an acceptable cost. The intelligence question is simple: **what must this agent understand, decide, and do to complete its job well?**

**Figure: Two pillars within the enterprise architecture.** Architecture provides the whole system. Intelligence and memory deserve a closer look because they shape what an agent can do and what supports its decisions.

**What the image shows:** Enterprise systems, people, tools, and controls support intelligence and memory. Intelligence enables understanding, investigation, and permitted action. Memory supplies discoverable, verifiable, cited evidence. Together they support useful work and verified results.

Image: https\://www\.agenticarchitectureskills.com/images/ladder/enterprise-pillars-v1.webp

## Architecture gives us the whole system; now we examine intelligence

The [enterprise architecture](https://www.agenticarchitectureskills.com/architecture) explains the layers that connect models, data, business systems, people, and controls. Within that system, we now look closely at two pillars. **Intelligence** determines how the agent handles the task. **Memory** supplies information the agent can find, check, and use as evidence.

A powerful model is a useful starting point, but its general capability is not yet an enterprise capability. We have to shape it around the work: the goal, the available evidence, the tools, the limits, and the measure of success. That is what this guide means by distilling model intelligence into an enterprise agent.

## How much intelligence does the job need?

A natural starting point is to use one capable model for every task and give it broad instructions. That makes experimentation easy, but it does not tell us where reasoning adds value, where a known workflow is enough, or whether a complex agent pays for its extra effort.

Compare three kinds of work. These are design choices to test, not a mandatory progression.

**Figure: Match intelligence to the work and its full cost.** These are task choices, not universal maturity levels or measured cost rankings.

**What the image shows:** Compare known steps handled by a workflow, choosing the next check in a bounded investigation, and specialist judgment that may justify adaptation. Count models, tools, data, review, and errors, then evaluate cost per successful task.

Image: https\://www\.agenticarchitectureskills.com/images/ladder/intelligence-budget-v1.webp

**When the steps are known**, such as checking required fields before submitting an inspection request, ordinary software or a fixed workflow may do the job. A model might help interpret free text without choosing the whole process.

**When the next step depends on what is discovered**, such as investigating an unexplained production discrepancy, an agent may need to identify missing evidence, select a tool, examine its result, and decide what to check next. Its useful intelligence lies in managing that bounded investigation.

**When specialist behavior remains difficult**, such as recognizing a particular defect pattern or consistently applying a domain classification, compare better inputs, specialist models, and adaptation. Training becomes a candidate when it addresses a demonstrated limitation and the enterprise can maintain the result.

A capable agent does not automatically need broad authority. An excellent analysis may still require a person to approve an action. Choose [autonomy and supervision](https://www.agenticarchitectureskills.com/architecture/autonomy-contract) separately from the model's capability.

## The Intelligence ladder helps us build the capability deliberately

Begin with an outcome the business can recognize. Then examine the choices that make the agent capable of achieving it.

**Instructions: define good work (/ladder/instructions)**Tell the agent the goal, constraints, and required result. Otherwise capability may be spent on the wrong task.
**Context: supply what matters now (/ladder/context)**Give it relevant evidence and current task state. General knowledge does not establish the current condition of a particular asset.
**Tools and the loop: investigate and act (/ladder/tools-and-the-loop)**Let it fill a specific information gap or perform an allowed operation, then check what happened.

If those are sufficient, stop there. If a measured limitation remains, the model-adaptation methods below explain additional options. Improving the system and adapting the model can be combined; the names do not prescribe a shopping list.

## What should that intelligence cost?

Judge cost against the business outcome, not just one model call. An investigation can involve many calls, data retrieval, external tools, retries, and expert review. A cheaper answer that creates more rework may be the more expensive way to finish the job.

For a trial, record the total cost of the evaluated cases, including unsuccessful attempts, and divide it by the number of outcomes accepted as successful under the agreed quality standard. Also report the failure rate and serious errors separately, so a favorable average cannot hide them.

Compare configurations on the same representative cases. For example, test a rules-based workflow, a smaller model with retrieval, and a more capable model allowed to investigate. Route difficult cases to additional capability only if you can reliably recognize those cases and measure the improvement. Count the cost of building and maintaining that routing too.

For a production decision, spread build and integration costs over realistic task volumes and include recurring evaluation, monitoring, and maintenance. Training may add preparation cost while reducing effort per task; an investigation loop may add calls while avoiding expensive errors. Measure those tradeoffs rather than assuming that one arrangement is always cheaper.

Ask whether more capability improves correctness, time to completion, or the human effort required enough to justify its full cost. The [value and investment guide](https://www.agenticarchitectureskills.com/use-cases/value-and-investment) develops this business comparison.

## When changing the model is justified

**Adapters and fine-tuning (/ladder/adapters-and-fine-tuning)**Teach a repeatable behavior from examples when current behavior is the limitation.
**Distillation (/ladder/distillation)**Test whether a demonstrated capability can run on a smaller model at acceptable quality.
**Reinforcement fine-tuning (/ladder/reinforcement-fine-tuning)**Use outcome feedback where the quality of a decision can be graded reliably.
**Continued pretraining (/ladder/continued-pretraining)**Investigate additional domain training when the evidence supports that investment.
**Custom pretraining (/ladder/custom-pretraining)**Consider a specialist model when the task and data justify its full development cost.

Model distillation is one specific training technique. The broader goal of distilling intelligence into enterprise work includes all the system choices above.

## Continue into the other pillar: memory

An agent's judgment is useful only if we can examine what supported it. [Knowledge and memory](https://www.agenticarchitectureskills.com/memory) starts with what an agent should remember during a task and across future tasks. It then explains how to represent enterprise information, keep it current, and recover referenceable evidence for decisions.

For implementation choices, [diagnose a failed task](https://www.agenticarchitectureskills.com/ladder/choosing-an-approach), compare [one agent with several](https://www.agenticarchitectureskills.com/ladder/single-and-multiple-agents), or explore [combining specialist models](https://www.agenticarchitectureskills.com/ladder/combining-models).
