# Intelligence ladder

How much intelligence does an agent need for its job, and what should that intelligence cost?

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/ladder (Markdown: https://www.agenticarchitectureskills.com/ladder.md)
Updated: 2026-10-15
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

A team wants an agent to do a job. Before anyone picks a model, one question comes first. **What must this agent understand, decide and do to finish the job well, and at what cost?** The answer is to change the cheap things first. Those are the instructions, the context, and the tools and loop around the model. Change the model itself only when a measured limit remains. The intelligence ladder is the order in which to try those changes. It belongs to [the build step](https://www.agenticarchitectureskills.com/start#5-build) on the Start page.

**Figure: Two pillars within the enterprise architecture.** The architecture provides the whole system. Intelligence and memory shape what an agent can do and what supports its decisions.

**What the image shows:** Enterprise architecture is the base: systems, people, tools, controls, data, integrations, policies and governance. Two pillars stand on it. Intelligence: understand, investigate and act within limits. Memory: find, verify and cite. Together they hold up useful work and verified results.

Image: https\://www\.agenticarchitectureskills.com/images/ladder/enterprise-pillars-v1.webp

## Two pillars: intelligence and memory

An agent needs two things. **Intelligence** decides how it handles the task. **Memory** gives it information it can find, check and use as evidence. This page covers intelligence. [Knowledge and memory](https://www.agenticarchitectureskills.com/memory) covers the other pillar. Models and their training sit in [the intelligence and learning layer (R06)](https://www.agenticarchitectureskills.com/layers/r06-intelligence-and-learning), one of [the fourteen layers](https://www.agenticarchitectureskills.com/layers) of the estate.

## Match intelligence to the work

Using one capable model for every task makes trials easy. It does not show where reasoning adds value, or whether a complex agent pays for itself. Compare three kinds of work instead. These are choices to test, not a fixed order.

**Figure: Match intelligence to the work and its full cost.** These are task choices, not maturity levels or measured cost rankings.

**What the image shows:** Three kinds of task. Known steps need rules or a fixed workflow, a small effort. Choosing the next check needs a bounded agent, a medium effort. Specialist judgement may justify testing a trained model, a larger effort with expert review. The cost elements are models, tools, data, review and errors. A testing gate compares the cost per successful task.

Image: https\://www\.agenticarchitectureskills.com/images/ladder/intelligence-budget-v1.webp

**Known steps.** Checking required fields before an inspection request goes in has known steps. Ordinary software or a fixed workflow may do it.

**Steps that depend on what is found.** Investigating an unexplained gap in production figures changes as it goes. The agent finds missing evidence, picks a tool, reads the result and decides what to check next.

**Specialist judgement.** Spotting a particular defect pattern needs expert judgement. Compare better inputs, specialist models and training. Train only when it fixes a demonstrated limit you can maintain.

A capable agent does not need broad authority. Set how freely it acts in [the autonomy contract](https://www.agenticarchitectureskills.com/architecture/autonomy-contract), apart from the model's capability.

## Change the cheap things first

Try the three changes that cost least first.

**Instructions: define good work (/ladder/instructions)**Tell the agent the goal, the limits and the result you need. Otherwise its effort goes to the wrong task.
**Context: supply what matters now (/ladder/context)**Give it the relevant evidence and the current state of the task. General knowledge cannot tell it the condition of one asset.
**Tools and the loop: investigate and act (/ladder/tools-and-the-loop)**Let it fill a specific gap or perform an allowed operation. Then check what happened.

If those are enough, stop there. [The Agentic OS](https://www.agenticarchitectureskills.com/agentic-os) sets out the harness you build around the model and the runtime you buy.

## Count the full cost

Judge cost against the business outcome, not one model call. An investigation can involve many calls, tools, retries and expert review. A cheaper answer that creates rework can cost more in the end.

For a trial, add up the full cost of the evaluated cases, failed attempts included. Add supervision time at the full hourly cost of the people doing it. Add the cost of fixing wrong outcomes. Divide the total by the outcomes accepted as resolved to the agreed standard. That is the cost per resolved outcome. Report failures and serious errors separately, so a good average cannot hide them.

Compare designs on the same cases. For example, test a rules-based workflow, a smaller model with retrieval, and a stronger model allowed to investigate. Route hard cases to a stronger model only if you can reliably spot them. Spread build and upkeep costs over realistic volumes. Each agent has a budget with hard caps, tracked in [the observability and FinOps layer (R12)](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops). [Value and full cost](https://www.agenticarchitectureskills.com/use-cases/value-and-investment) builds the business case.

## Change the model only when a measured limit remains

When the cheap changes stop helping, five options change the model itself. They can be combined. Use only the ones the failure calls for.

**Adapters and fine-tuning (/ladder/adapters-and-fine-tuning)**Teach a repeatable behaviour from examples when the current behaviour is the limit.
**Distillation (/ladder/distillation)**Test whether a proven capability can run on a smaller model at acceptable quality.
**Reinforcement fine-tuning (/ladder/reinforcement-fine-tuning)**Use feedback on outcomes where the quality of a decision can be graded reliably.
**Continued pretraining (/ladder/continued-pretraining)**Train on your own raw text when the evidence supports that investment.
**Custom pretraining (/ladder/custom-pretraining)**Consider a specialist model when the task and data justify its full development cost.

Any model change re-runs the evals and the risk check at the change stage of [the agent lifecycle](https://www.agenticarchitectureskills.com/architecture/agent-lifecycle). [The learning flywheel](https://www.agenticarchitectureskills.com/architecture/learning-flywheel) sets out how it is tested and promoted.

## More help while you build

* [Diagnose a failed task](https://www.agenticarchitectureskills.com/ladder/choosing-an-approach) before changing anything.
* Choose between [a workflow, one agent or several](https://www.agenticarchitectureskills.com/ladder/single-and-multiple-agents).
* [Combine specialist models](https://www.agenticarchitectureskills.com/ladder/combining-models) around one task.
* Give the agent evidence it can check, in [knowledge and memory](https://www.agenticarchitectureskills.com/memory).

## Evidence and limits

The three kinds of work and the order of changes are teaching designs, not measured rankings. Each step page carries its own sources, dates and limits.

## Next step

Diagnose a failed task before changing anything, on [choose what to change](https://www.agenticarchitectureskills.com/ladder/choosing-an-approach).
