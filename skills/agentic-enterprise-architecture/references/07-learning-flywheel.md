# The learning flywheel

How agent behaviour improves over time without anyone losing control of it: tested promotion, calibrated judges, and staged rollout.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/architecture/learning-flywheel (Markdown: https://www.agenticarchitectureskills.com/architecture/learning-flywheel.md)
Updated: 2026-08-24
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

> **In plain terms.**
>
> Agents can get better at their work over time, but every change in behaviour is a change to a production system. This page describes the controlled loop that makes improvement safe. Collect evidence from real use, test a proposed change against known failures, and have a person approve it. Roll it out to a small share of traffic first, and pull it back if it stops passing. The one thing to remember: an agent that changes its own behaviour without passing through that gate has deployed a change nobody approved.

## Why learning needs a deployment gate

**WHY:** When an agent changes how it behaves, the production system has changed. Letting instance memory or automatically learned rules alter behaviour directly creates an unversioned deployment that nobody tested or approved. Improvement is valuable only if it remains reversible and measurable.

**WHAT:** Separate **a fast instance-memory loop** from **a slow governed learning loop**. Production traces feed evals; failures become counterexamples; proposed changes are curated, tested, reviewed and promoted; rollout starts in shadow and canary stages; promoted hard rules land outside the model; dead rules can be demoted. Judges are calibrated, versioned and kept separate from the systems they grade.

![Visual summary of the governed learning flywheel](/figures/architecture/learning-flywheel.webp)

## Two loops, separated by governance

**In short:** A slow, tested loop changes how agents behave; a fast loop lets one agent remember things; only the slow loop may change behaviour.

The system flywheel runs offline. It is evaluated, versioned, and can be rolled back. Its steps are trace (record what each run did), evaluate, curate, promote, roll out. Instance memory, what one running agent remembers, is online and immediate. Learnings move from the second loop into the first, never the reverse. Instance memory that reshapes behaviour without a gate is an unversioned deployment that nobody approved.

**Figure: Memory serves work; learning changes future work.** Do not let online memory updates silently become offline policy changes.

Learning promotion passes through evaluation, approval, staged release, and a demotion path.

**What the diagram shows:** Two connected loops separating online memory used during work from an offline learning loop that evaluates and promotes changes into governed enforcement. The comparison contains 2 groups: Online memory loop, containing Retrieve approved context, Execute bounded task, Capture candidate fact, Expire or queue for review; Offline learning loop, containing Build eval case, Judge against counterexamples, Approve and stage, Promote or demote artifact.

Diagram: https\://www\.agenticarchitectureskills.com/figures/memory-learning-flywheel.svg

## The architectural fork

**In short:** Improvement compounds only when real-run records and the test suite share one store, so a production failure becomes a test case automatically.

One property separates pipelines that compound from pipelines that stagnate: **production traces and eval datasets share a data layer**. An eval is a set of test tasks with known right answers. When the two share storage, a failing score in production promotes its trace into the offline test suite automatically. Without that join, every improvement cycle starts with a manual export, and most never start.

## The promotion gate, as the evidence left it

**In short:** A rule is accepted for surviving tests, not for being frequent, lands outside the model, and can be removed later.

Measurements from 2026 force three edits to the intuitive design:

1. **Gate on counterexample survival and eval regression, not frequency.** In the direct study, only 7 of 32 automatically learned policies were grounded in evidence and executable. A gate based on how often a pattern appeared failed in both directions. It accepted a rule that collapsed success from 5 in 20 to 1 in 20, and it rejected a rule worth five points. Rule induction guided by counterexamples (test cases built from real failures), with human review, reached an F1 score of 0.93 to 0.98 against expert baselines of 0.49 to 0.70. F1 is a standard accuracy measure. The process converged in four to five iterations.
2. **Land promoted artifacts outside the model.** The hard tier is policy-as-code: rules written as versioned code, deployed independently of the model. Details are on [the enforcement page](https://www.agenticarchitectureskills.com/architecture/enforcement).
3. **Keep a demotion path.** Accumulated context is not free. Machine-generated context files reduced task success while raising inference cost (the cost of running the model) by roughly a fifth. A pipeline that only ever promotes compounds cost and never sheds dead rules.

## Lifecycle and rollout

**In short:** An agent moves through named stages from draft to retired, each with a measured bar, and new versions reach a small share of traffic first.

The one fully specified published lifecycle runs DRAFT, APPROVED, PUBLISHED, DEPRECATED, RETIRED. It names a threshold for each gate: faithfulness at least 0.80, correctness 0.90, tool accuracy 0.90, helpfulness 0.70, latency (response time) at most 15 seconds, harm at most 5 percent. A seven-day staleness policy triggers automated re-evaluation. Its enforcement is architecturally elegant: **discovery returns only PUBLISHED agents**. An agent whose quality degrades therefore becomes harder to reach, without a policy engine intervening. Rollouts run in shadow mode first, alongside production and affecting nothing. Next comes a canary release, where 1 to 5 percent of traffic uses the change, gated on session success, satisfaction, and escalation. Then it goes to everyone, with feature flags separating activation from deployment.

**Figure: From trace to rollout, gated at every step.** A learning reaches production only through evaluation, versioning, and staged release, and it can always come back out.

The promotion pipeline: evidence in, counterexample-gated, versioned outside the model, released in stages, demotable on staleness.

**What the diagram shows:** Seven stages from captured trace through eval case, counterexample gate, versioning outside the model, shadow, canary, and full rollout with an armed demotion path. The sequence contains 7 stages: 1, Trace captured: A production run lands in the shared trace and eval data layer.; 2, Eval case built: A failing online score promotes its own trace into the offline suite.; 3, Counterexample gate: The candidate survives the counterexample suite with no eval regression; frequency alone never promotes., followed by the Human review before approval gate; 4, Versioned outside the model: The approved artifact lands as policy-as-code or a pinned version, deployable and rollback-capable.; 5, Shadow: Runs beside production, observed, with no effect on outcomes.; 6, Canary: 1 to 5 percent of traffic, gated on session success, satisfaction, and escalation., followed by the Flags decouple activation from deployment gate; 7, Full, demotion armed: Seven-day staleness re-evaluation; a failing score demotes the artifact while its eval case stays..

Diagram: https\://www\.agenticarchitectureskills.com/figures/learning-promotion-pipeline.svg

## Judges are governed components

**In short:** A model that grades another model's work is itself a system to check, version, and keep separate from what it grades.

Judge systems, models that grade other models' answers, agree with themselves more than they measure the intended property. They also drift silently when accessed as a hosted service. So judges are calibrated against human labels and re-validated on a schedule. Versions are pinned. Rubrics are structured and include an explicit Unknown option. Outcomes are graded, rather than the sequence of tool calls. And **the optimizer and the evaluator stay decoupled**, so nothing grades its own work. Expert review costs roughly a hundred times (two orders of magnitude) more per output than model judging. That is why the working design is an expert-owned bar, judging at volume, and sampled human verification.

## The harness is an attack surface

**In short:** The test set-up itself can be gamed, so it is locked down like a production system.

The evaluation harness, the shell that runs an agent through its tests, can itself be attacked. An agent with no real capability has scored perfectly on several major public benchmarks by editing the evaluation configuration rather than solving anything. The recurring weakness was the absence of isolation between the agent and its evaluator. Eval infrastructure therefore gets the same isolation discipline as production.

**The research behind this page**

* [The learning-loops map](https://www.agenticarchitectureskills.com/library/architecture/learning-loops-map)
* [Intelligence and learning findings](https://www.agenticarchitectureskills.com/library/layers/r06-intelligence-and-learning/findings)
* [Agent platform findings](https://www.agenticarchitectureskills.com/library/layers/r07-agent-platform/findings)
