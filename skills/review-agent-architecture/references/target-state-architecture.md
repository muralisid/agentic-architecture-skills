# Architecture of the agentic enterprise

How model intelligence becomes useful enterprise work: the layers you own, the lifecycle every agent runs through, the capabilities you add, and the controls set along the way.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/architecture (Markdown: https://www.agenticarchitectureskills.com/architecture.md)
Updated: 2026-10-15
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

How do you turn model intelligence into useful enterprise work? Start with a task, such as checking a possible safety issue and arranging an inspection. A model and some documents can answer a question about it. Finishing the work needs more. The agent needs current information, permission to act, reliable business systems, and a person who answers for the result. This guide builds that in three parts: [the layers you own](https://www.agenticarchitectureskills.com/layers), [the lifecycle you run](https://www.agenticarchitectureskills.com/architecture/agent-lifecycle) and [the capabilities you add](https://www.agenticarchitectureskills.com/architecture/system-view). Controls are set as each agent passes through its lifecycle. For the whole route in order, read [Start here](https://www.agenticarchitectureskills.com/start).

## See the whole system first

**Figure: From a business goal to a confirmed result.** Start with the outcome. Intelligence and memory help the agent work toward it. Tools, controls and people make that work possible.

**What the image shows:** A business owner defines a goal. An agent uses intelligence and memory. It passes an independent permission check, then uses enterprise systems. The system returns a result for the agent to check. People oversee the work. Independent records show what happened.

Image: https\://www\.agenticarchitectureskills.com/images/architecture/enterprise-overview-v1.webp

Take an agent that reviews vegetation near power lines. It needs images, the correct asset location and the inspection policy. It may ask for a closer look or propose an inspection. A separate permission check decides whether it can create the work order. The task ends with a confirmed result or a clear handover to a person.

This is a proposed design example. An image alone does not prove a safety risk. [The task walkthrough](https://www.agenticarchitectureskills.com/architecture/task-walkthrough) follows an inspection in more detail.

## The layers you own

Every agent works inside systems the company already runs. This guide groups them into fourteen layers. They run from infrastructure and compute (R01) to agent data engineering (R14). The layers hold the data, the records, the integration, the security and the people. Agents do not replace them. Agents add new demands on each one.

For intelligence, start with the [intelligence and learning layer (R06)](https://www.agenticarchitectureskills.com/layers/r06-intelligence-and-learning) and the [agent platform layer (R07)](https://www.agenticarchitectureskills.com/layers/r07-agent-platform). Both rest on [infrastructure and compute (R01)](https://www.agenticarchitectureskills.com/layers/r01-infrastructure). For memory, start with the [data platform layer (R02)](https://www.agenticarchitectureskills.com/layers/r02-data-platform) and the [agent data engineering layer (R14)](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering). All of them depend on security, governance, monitoring and the people who run the service.

Explore all fourteen enterprise architecture layers at https\://www\.agenticarchitectureskills.com/layers. The layers cover infrastructure, data, integration, official records, industrial systems, models, agent platforms, collaboration, channels, security, governance, monitoring, operating practices, and agent data engineering.

Open a layer to see its role, then follow its detailed design.

## The lifecycle you run

Every agent passes through nine stages: register, sponsor and owner, entitle, evaluate, approve, operate, change, periodic review and retire. Building and piloting come before stage 1. The registry record holds the agent's state: active, under review, deprecated or retired. AWS and Microsoft guidance both frame agent management as a lifecycle like this one.

The inspection agent is registered with a named sponsor before it touches a record. It is entitled to read imagery and draft work orders, and nothing more. It is evaluated on past inspections before anyone approves it. Once live, a change to its model sends it back to evaluate.

## The capabilities you add

Seven capabilities let agents run safely across the layers. Three let agents work: a runtime, a tool gateway, and [knowledge and memory](https://www.agenticarchitectureskills.com/memory). Four keep them in bounds: identity and policy, evaluation and release, observability and an audit trail, and human oversight. Each lifecycle stage calls on some of them.

**Figure: Layers you own, a lifecycle you run, capabilities you add.** The layers are what you own. The capabilities are what you add across them. Each lifecycle stage calls on the capabilities it needs.

**What the image shows:** On the left, a building of fourteen floors shows the layers you own. They run from infrastructure and compute (R01) at the bottom to agent data engineering (R14) at the top. In the centre, seven bands show the capabilities you add. Each band names the industry products and the layers that build it. The runtime is built from R01 and R07. The tool gateway is built from R03, R04 and R05. Knowledge and memory is built from R02 and R14. Identity and policy is built from R10, R11 and R07. Evaluation and release is built from R06 and R12. Observability and audit trail is built from R12 and R11. Human oversight is built from R13, R08 and R09. On the right, the nine lifecycle stages run in order, and each change loops back to evaluate. Lines link each stage to the capabilities it calls on. Register, entitle and retire call on identity and policy. Sponsor and owner calls on human oversight. Evaluate and change call on evaluation and release. Approve calls on human oversight and on identity and policy. Operate calls on the runtime, the tool gateway, knowledge and memory, and observability. Periodic review calls on observability and on human oversight. A strip at the bottom gives the two rules. Policy is enforced outside the model. The audit trail is written where the agent cannot touch it.

Image: https\://www\.agenticarchitectureskills.com/figures/architecture/layers-lifecycle-capabilities.svg

Read the diagram around one task. A person sets the goal. The runtime runs the agent. Knowledge and memory supply the context. The tool gateway connects the agent to tools. Identity and policy limit what is allowed. Observability and audit trail record what happened. Evaluation and release test each change before it enters use.

Two rules hold the design together.

* **[Policy is enforced outside the model](https://www.agenticarchitectureskills.com/architecture/enforcement).** The model never checks its own permissions. The gateway and the policy decision point do.
* **The audit trail is written where the agent cannot touch it.** A separate channel records calls, approvals and outcomes.

[What an agent platform provides](https://www.agenticarchitectureskills.com/architecture/system-view) sets out each capability and the products behind it.

## Connect intelligence and memory

Intelligence and memory need their own questions. How capable must the agent be for this task? What information must it have to make a supported decision?

**Figure: How intelligence and memory work together.** Memory supplies context and evidence you can point to. Intelligence chooses the next step. The actual result decides whether to continue, stop or ask for help.

**What the image shows:** Memory supplies the current task, past experience and reference evidence to intelligence. Intelligence chooses the next check. A separate permission gate comes before tool use. The result returns for checking. The agent then continues or finishes. Task progress is saved. Updates to shared memory need review.

Image: https\://www\.agenticarchitectureskills.com/images/architecture/intelligence-memory-loop-v1.webp

In the inspection example, thread memory tracks the location under review and the checks already done. Longer-lived memory may supply an earlier inspection, an approved procedure or a past case. The agent uses that context to decide whether it needs another observation.

Keep two kinds of evidence apart. **Reference evidence** supports the decision: which image, record or procedure was used, and when it applied. **Execution evidence** shows what happened: which tool was called, who approved it, and what the system returned. A summary written by the agent cannot replace those records.

Saving task progress is not the same as changing shared knowledge. Review proposed lasting updates for accuracy, access and freshness. Test changes to models, prompts and policies before release.

**Design the intelligence (/ladder)**Choose the level of reasoning, tool use and coordination the task needs. Weigh quality, time, cost and supervision together.
**Design the memory (/memory)**Start with current context, thread memory and longer-lived knowledge. Then organise sources, retrieval and how long each item is kept.

## The controls, in order

Once the main flow is clear, set the controls for your task. Most are set at the evaluate and approve stages.

1. [The four questions](https://www.agenticarchitectureskills.com/architecture/agent-types): what the agent does, what its credentials allow, how freely it acts, and what it can damage.
2. [The autonomy contract](https://www.agenticarchitectureskills.com/architecture/autonomy-contract): how freely it may act, and how far its behaviour may learn.
3. [The risk profile](https://www.agenticarchitectureskills.com/architecture/risk-profile): score the agent to set its risk tier. The tier decides the controls.
4. [The deterministic zones](https://www.agenticarchitectureskills.com/architecture/deterministic-zones): access, money, safety actuation and formal regulatory records. A model never approves in these.
5. [The delegation chain](https://www.agenticarchitectureskills.com/architecture/delegation-chain): trace every action back to the person who asked.
6. [Enforcement outside the model](https://www.agenticarchitectureskills.com/architecture/enforcement): where each check sits and who runs it.
7. [The learning flywheel](https://www.agenticarchitectureskills.com/architecture/learning-flywheel): how a proposed improvement is tested before it ships.

## Where to go next

**Make software usable by agents (/architecture/software-for-agents)**Design interfaces, delegated access, reliable transactions and handover to a person.
**Compare technology choices (/decisions)**Twenty-five decisions, each with alternatives, evidence and the conditions that change the answer.

A company using agents inside purchased software has different control points from a team running its own agent platform. Check what each system exposes. Do not assume one gateway sees every action. The [enterprise reference designs](https://www.agenticarchitectureskills.com/library/architecture/master-target-state) compare starting points.

Start from a [business use case](https://www.agenticarchitectureskills.com/use-cases), or check all ten cross-cutting concerns in [the concern matrix](https://www.agenticarchitectureskills.com/architecture/concern-matrix). Look up any term in [plain words](https://www.agenticarchitectureskills.com/architecture/plain-words). Read about [security threats](https://www.agenticarchitectureskills.com/security), or apply an [architecture review skill](https://www.agenticarchitectureskills.com/skills) to a real design.

## Evidence and limits

This is a reference design, not a product to buy. The three-part frame is this guide's own. The lifecycle stages follow AWS and Microsoft guidance closely. The capability names follow AWS, Microsoft and Google products, dated on [What an agent platform provides](https://www.agenticarchitectureskills.com/architecture/system-view). The inspection example is a proposed design. It is not a measured deployment.

**Next step:** see the seven capabilities in detail on [What an agent platform provides](https://www.agenticarchitectureskills.com/architecture/system-view).

**Explore this topic**

* [Master target-state architecture](https://www.agenticarchitectureskills.com/library/architecture/master-target-state)
* [Vision and target state](https://www.agenticarchitectureskills.com/library/architecture/vision-and-target-state)
* [The concerns-by-layers matrix](https://www.agenticarchitectureskills.com/library/architecture/concerns-by-layers-matrix)
