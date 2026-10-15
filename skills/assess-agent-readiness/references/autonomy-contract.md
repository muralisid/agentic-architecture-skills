# The autonomy contract

How much an agent may do on its own, how it may learn, and the controls, readiness checks, and oversight capacity that earn each step up.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/architecture/autonomy-contract (Markdown: https://www.agenticarchitectureskills.com/architecture/autonomy-contract.md)
Updated: 2026-10-15
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

> **In plain terms.**
>
> Every task an agent takes on sits at a chosen level of independence, from a person doing the work with help to the agent running unattended under policy. This page sets out those levels, the controls each one requires, the readiness a company must show before moving up, and how much human supervision each level really needs. The one thing to remember: a level you cannot supervise is a level you have not reached.

## Why autonomy needs a contract

**WHY:** "Autonomous" is not a useful architecture property by itself. A workload can only operate as independently as its weakest readiness area and the organisation's real ability to supervise bursts of exceptions. Raising autonomy without the controls, learning loop, evidence and oversight capacity behind it creates an operational gap rather than a capability.

**WHAT:** Give every workload two explicit, reversible settings: **autonomy A0 to A5** and **learning L0 to L3**. Treat the required-controls column as the actual contract. Gate higher autonomy on seven readiness areas, let the weakest area set the ceiling, require governed learning and proven oversight at A4+, and size supervision using burst-rate queueing capacity rather than daily averages.

**Figure: Autonomy and learning: floors, ceiling and gate.** A level you cannot supervise is a level you have not reached.

**What the image shows:** A grid crosses autonomy levels A0 to A5 with learning levels L0 to L3. Each column shows the human's job. A1 and A2 carry a Tier 1 floor, A3 Tier 2, and A4 and A5 Tier 3. A0 has no floor. The cells for A4 and A5 at L0 and L1 are hatched: A4 and above need L2. A solid line before A4 marks the oversight gate, burst capacity proven. A dashed line marks the readiness ceiling, set by the weakest area. The chat and vegetation agents sit at A2. The billing-exception agent sits at A3. One agent shows three readings: designed, permitted and exercised. Exercised above permitted is an incident.

Image: https\://www\.agenticarchitectureskills.com/figures/architecture/axl-floors-and-gate.svg

## Two axes, applied per workload

**In short:** Each piece of work gets two settings, how independent the agent is and whether it may learn, both chosen on purpose and reversible.

The first axis is the autonomy level: who executes the work, and what the human keeps hold of. Its levels are A0 manual, A1 assisted, A2 delegated tasks, A3 supervised autonomy, A4 managed autonomy, and A5 governed lights-out. The second axis is the learning level: whether the agent improves, and under what control. Its levels are L0 fixed policy, L1 curated learning, L2 governed learning (the learning flywheel), and L3 continuous learning inside guardrails. The two axes move independently. Every workload sits somewhere on the grid deliberately, and movement is earned and reversible.

Autonomy is recorded three ways. Designed autonomy is what the build allows. Permitted autonomy is what this contract grants. Exercised autonomy is what the logs show the agent doing. Controls follow the higher of permitted and exercised. Exercised above permitted is an incident. This happens in practice. The [MIT AI Agent Index](https://aiagentindex.mit.edu/) (2025 edition) studied enterprise agents. They were configured at low autonomy but often ran at high autonomy once deployed. How A0 to A5 lines up with other published ladders is in [the crosswalk on the risk profile](https://www.agenticarchitectureskills.com/architecture/risk-profile#the-autonomy-crosswalk).

**Figure: The A×L maturity matrix.** Autonomy and learning are independent; higher is not automatically better.

Choose the cell that is justified for a workload rather than treating the top-right as a destination.

**What the diagram shows:** Six autonomy levels A0 through A5 crossed with four learning levels L0 through L3, with governed scaling emphasized in the middle of the matrix. The matrix crosses A0 Manual, A1 Assisted, A2 Delegated tasks, A3 Supervised autonomy, A4 Managed autonomy, A5 Governed lights-out with L0 Fixed policy, L1 Curated learning, L2 Governed learning, L3 Continuous learning. Annotated cells are A2 Delegated tasks by L1 Curated learning: Common starting point; A4 Managed autonomy by L2 Governed learning: Oversight gate; A5 Governed lights-out by L3 Continuous learning: Rare and domain-scoped.

Diagram: https\://www\.agenticarchitectureskills.com/figures/autonomy-learning-matrix.svg

## The controls column is the contract

**In short:** Each step up in independence comes with a fixed list of controls, and that list, not the level name, is the agreement.

| Level | Human role                                      | Required controls                                                                                               |
| ----- | ----------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| A2    | Review every output                             | Task scoping, output review, audit                                                                              |
| A3    | Approve irreversible actions, handle exceptions | Approval gates, evals, budgets, kill switch                                                                     |
| A4    | Manage exception queues, supervise              | Eval-gated change, cross-cutting concern register enforced, supervisor dashboards, designed oversight capacity  |
| A5    | Set policy, own accountability, audit outcomes  | Proven eval maturity, continuous assurance, regulator-ready evidence, oversight capacity measured in production |

Three rules connect the axes. **A4 and above require L2 or better.** At that level reliability must be improvable, not merely observable. **A4 and above require proven oversight capacity.** A level you cannot supervise is a level you have not reached. **Without a learning loop you have a fixed-policy agent, not a teammate.** Fixed policy is the right choice for many workloads, as long as it is named honestly.

## Readiness gates autonomy

**In short:** Seven areas of readiness are each scored from 0 to 3, and the weakest area, not the total, decides how much autonomy is safe.

Seven areas are each scored from 0 to 3: absent, ad hoc, managed, operated. Each area has four yes, partly or no questions in [the readiness assessment](https://www.agenticarchitectureskills.com/library/frameworks/readiness-assessments).

1. **Data** covers who owns the data, its class, its quality, and agent memory. It includes ACL-aware retrievability, meaning retrieval that respects each person's access rights.
2. **Integration and tools** covers governed API coverage (application programming interfaces, the defined ways software talks to software) and tool exposure through a gateway. It also covers on-behalf-of flows, in which the agent acts with the requesting person's permissions, and safe long-running actions.
3. **Identity and registry** covers agents as first-class principals in one registry, with a named sponsor. The registry shows the two estates: agents behind your own gateway and agents inside vendor products. Credentials are short-lived and never held by agents, and the off switch is tested.
4. **Controls on actions** covers the risk tier, a policy decision point outside the model, sandboxed code, and a person who decides when a decision affects a person.
5. **Testing and operations** covers observability, offline and online evals, re-testing on every change, and incident practice.
6. **Cost and value** covers intake with kill criteria (agreed conditions for stopping), token budgets with a hard stop, and cost per resolved outcome.
7. **People and operating model** covers named owners and supervisors, clear exceptions, and burst supervision capacity.

The profile governs, never the total. Read it in this order: data, integration, identity, controls, testing, cost, people.

| Profile                                                                             | Highest autonomy                                              |
| ----------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| Any area at 0 for the target workload                                               | A1 only                                                       |
| Data and integration at 2 or more, all others at 1 or more                          | A2                                                            |
| Data, integration, identity, controls and testing at 2 or more, others at 1 or more | A3                                                            |
| All seven at 2 or more, with controls, testing and cost at 3                        | A4, with L2 governed learning and the oversight-capacity gate |
| All seven at 3, plus regulator-ready evidence                                       | A5 candidacy, per domain only                                 |

**Figure: The weakest area sets the ceiling.** Northstar is a fictional teaching example. Read the profile, not the total.

**What the image shows:** Seven bars score the readiness areas from 0 to 3. Northstar scores 2 for data, 2 for integration and tools, 1 for identity and registry, 1 for controls on actions, 2 for testing and operations, 1 for cost and value, and 2 for people and operating model. A dashed line runs from the lowest score, 1, to the ceiling table. The row for data and integration at 2 or more, with all others at 1 or more, gives A2.

Image: https\://www\.agenticarchitectureskills.com/figures/architecture/readiness-profile-to-ceiling.svg

Two overrides tie the ceiling to [the risk profile](https://www.agenticarchitectureskills.com/architecture/risk-profile). Each can only lower it. A Tier 3 workload needs controls at 3 for A3 or above. A session with untrusted input, sensitive data and external action is capped at A2, whatever the scores. That second override is the Rule of Two.

Identity gaps cap autonomy without blocking a start. A workload can begin at A1 while the identity chain is built.

Readiness is scored on controls that are in place, not on a tally of clean runs, because a run count is a weaker instrument than it appears. A gate of twenty runs at a 95 percent pass rate is consistent with a true pass rate as low as 78 percent, and it revokes a genuinely compliant workload most of the time. The arithmetic is on [what an Agentic OS is, and what it does not solve](https://www.agenticarchitectureskills.com/agentic-os#a-worked-caution-the-trust-ledger).

**Figure: Stepping autonomy up and down.** Step up one level at a time, on controls and eval results. Step down at once. Every move re-runs the evals and the risk profile.

**What the image shows:** Six levels run from A0 manual at the bottom to A5 governed lights-out at the top. Each shows the human's job, what it takes to step up to it, and its tier floor. A2 needs data and integration at 2 or more and the rest at 1 or more. A3 needs data, integration, identity, controls and testing at 2 or more, plus approval gates, budgets, a kill switch and evals against a human baseline. A line before A4 marks the oversight gate, burst capacity proven. A4 also needs L2 governed learning and all seven areas at 2 or more, with controls, testing and cost at 3. A5 needs all seven at 3, regulator-ready evidence and oversight measured in production, per domain only. An anomaly, a change of scope, or exercised autonomy above permitted demotes the agent at once. Promotion rests on controls and eval results, never a count of clean runs. An example agent is designed for A4, permitted at A3 and exercised at A2.

Image: https\://www\.agenticarchitectureskills.com/figures/architecture/autonomy-step-up-and-down.svg

## The oversight gate, as a burst rate

**In short:** No credible supervision ratio is published, so oversight capacity comes from queueing maths, budgeted per ten minutes, never daily.

No credible published human-to-agent supervision ratio exists from any source. The vendor that coined the metric has published no number in two annual editions. What transfers instead is queueing arithmetic and alarm-management standards:

**Figure: Supervision capacity at burst.** Budget oversight per ten minutes, never as a daily average. No credible supervision ratio is published, so use your own measured wait times.

**What the image shows:** Fan-out equals neglect time divided by interaction time plus wait time, plus one. Leaving wait time out overstates capacity by up to 67 percent. A timeline shows routine exceptions, then a burst that crosses the capacity line in the busiest ten minutes. The system degrades safely, then recovers. The daily average stays under the capacity line the whole time.

Image: https\://www\.agenticarchitectureskills.com/figures/architecture/supervision-burst-capacity.svg

* **Capacity follows the fan-out relation.** Fan-out is how many agents one supervisor can watch at once. It equals neglect time (how long an agent can safely run unattended) divided by interaction time (how long a person needs per intervention) **plus wait time**, plus one for the agent being handled at that moment, the form the R13 research uses. Leaving wait time out overstates capacity by up to 67 percent, and by 36 percent even in exception-only designs.
* **Budgets are burst rates, never daily averages.** Oversight budgets are set as burst rates per ten minutes (demand at its busiest, not averaged), never as daily averages. The alarm-management standards hold that a per-ten-minute rate cannot validly be converted to a longer window. They removed their per-day metric because averaging destroys its meaning. A daily-average target will be met on the dashboard and violated in every burst.
* **Expect calibrated oversight, not a ratchet.** Calibrated oversight means that with experience, standing permission broadens **and** intervention rates rise. In measured deployments, auto-approval roughly doubled while interrupt rates nearly doubled alongside it. Rising interventions with expanding autonomy is the system working. Falling interventions with expanding autonomy is the thing to investigate.

Measure these, as [R13](https://www.agenticarchitectureskills.com/layers/r13-operating-model), the operating model layer, sets out. Track the intervention rate and its trend, the mix of escalations by trigger, wait time per item, and verification cost per review. Add periodic blind checks against self-reported figures.

**Next step:** score the agent's risk on [the risk profile](https://www.agenticarchitectureskills.com/architecture/risk-profile).

**Explore this topic**

* [The maturity model](https://www.agenticarchitectureskills.com/library/architecture/maturity-model)
* [Readiness assessments](https://www.agenticarchitectureskills.com/library/frameworks/readiness-assessments)
* [Operating model findings](https://www.agenticarchitectureskills.com/library/layers/r13-operating-model/findings)
