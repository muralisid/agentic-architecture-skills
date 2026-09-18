# Architecture of the agentic enterprise

See how intelligence, memory, tools, people, and controls work together, then explore the fourteen enterprise layers.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/architecture (Markdown: https://www.agenticarchitectureskills.com/architecture.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

How do you turn model intelligence into useful enterprise work? Start with a task, such as investigating a possible safety issue and arranging an inspection. The architecture must connect the agent to evidence, give it appropriate tools, limit what it can do, and confirm what actually happened.

Connecting a model to documents can help it answer a question. Completing the work requires more: current information, permission to act, reliable business systems, and someone responsible when the task cannot be completed.

## See the whole system first

**Figure: From a business goal to a confirmed result.** Start with the outcome. Intelligence and memory help the agent work toward it; tools, controls, and people make that work possible.

**What the image shows:** A business owner defines a goal. An agent uses intelligence and memory, passes an independent permission check, and uses enterprise systems. The system returns a result for the agent to check. People oversee the work and independent records capture what happened.

Image: https\://www\.agenticarchitectureskills.com/images/architecture/enterprise-overview-v1.webp

For example, an agent reviewing vegetation near power lines needs images, the correct asset location, and the inspection policy. It may request a closer look or propose an inspection. A separate permission check determines whether it can create the work order. The task ends with a confirmed result or a clear handover to a person.

This is a proposed design example, not a claim that an image alone establishes a safety risk. The [task walkthrough](https://www.agenticarchitectureskills.com/architecture/task-walkthrough) follows an inspection in more detail.

## Break the system into responsibilities

The reference design uses seven **planes** to group responsibilities. These are a way to reason about the system, not seven products to buy.

**Figure: Seven responsibilities in one system.** Every responsibility needs an owner and an implementation. Several may be supported by systems the enterprise already operates.

**What the image shows:** Human: set goals and handle exceptions. Execution: run the agent and workflow. Knowledge: supply information and memory. Action: connect tools and business systems. Control: enforce permissions and limits. Evidence: independently record what happened. Improvement: evaluate changes before release.

Image: https\://www\.agenticarchitectureskills.com/images/architecture/architecture-responsibilities-v1.webp

Read the diagram around one task: a person sets the goal; execution runs the agent; knowledge supplies context; action connects it to tools. Control limits what is allowed. Evidence records what happened. Improvement tests proposed changes before they enter use.

Two boundaries matter throughout this design. **The model does not enforce its own permissions.** Enforcement belongs outside its reasoning. **The agent is not the sole author of its audit trail.** Trusted collection must capture calls, approvals, and outcomes independently. Read the [complete system view](https://www.agenticarchitectureskills.com/architecture/system-view) for the boundaries and their implementation options.

## Connect intelligence and memory

Intelligence and memory are two important parts of this architecture. Their design starts with different questions: how capable must the agent be for this task, and what information must it have to make a supported decision?

**Figure: How intelligence and memory work together.** Memory supplies context and referenceable evidence. Intelligence chooses the next step. The actual result determines whether to continue, stop, or ask for help.

**What the image shows:** Memory supplies the current task, past experience, and reference evidence to intelligence. Intelligence chooses the next check. A separate permission gate precedes tool use. The result returns for checking and the agent continues or finishes. Task progress is saved; updates to shared memory require review.

Image: https\://www\.agenticarchitectureskills.com/images/architecture/intelligence-memory-loop-v1.webp

In the inspection example, thread memory keeps track of the location being investigated and checks already completed. Longer-lived memory may supply an earlier inspection, an approved procedure, or a relevant past case. The agent uses that context to decide whether it has enough information or needs another observation.

Keep two kinds of evidence distinct. **Reference evidence** supports the decision: which image, record, or procedure was used, and when it applied. **Execution evidence** establishes what happened: which tool was called, who approved it, and what the business system returned. A summary written by the agent cannot replace those records.

Saving task progress is also different from changing shared knowledge or improving a model. Review proposed durable updates for accuracy, access, and freshness. Test changes to models, prompts, and policies through the improvement process before release.

**Design the intelligence (/ladder)**Choose the level of reasoning, tool use, and coordination the task needs. Consider quality, time, cost, and supervision together.
**Design the memory (/memory)**Start with current context, thread memory, and longer-lived knowledge. Then organize sources, representations, retrieval, and lifecycle.

## Find these responsibilities in the fourteen layers

The seven planes describe responsibilities across the system. The fourteen layers below locate the enterprise capabilities that provide them. They are two views of the same architecture, not twenty-one separate components.

For intelligence, start with **Intelligence & learning** and **Agent platform**, supported by **Infrastructure & compute**. For memory, start with **Data platform** and **Data engineering for agents**, connected to the agent platform. Both depend on security, governance, monitoring, and the people operating the service.

Explore all fourteen enterprise architecture layers at https\://www\.agenticarchitectureskills.com/layers. The layers cover infrastructure, data, integration, official records, industrial systems, models, agent platforms, collaboration, channels, security, governance, monitoring, operating practices, and agent data engineering.

Open a layer to see its role, then follow its detailed design. The [plane-to-layer crosswalk](https://www.agenticarchitectureskills.com/architecture/system-view#the-crosswalk) connects the two views explicitly.

## Add detail when you need it

Once the main flow is clear, work through the boundaries for your task:

* [Protect consequential actions](https://www.agenticarchitectureskills.com/architecture/deterministic-zones): access, money, physical safety, and official regulatory records.
* [Identify the agent and its sponsor](https://www.agenticarchitectureskills.com/architecture/identity-chain), then [enforce permission outside the model](https://www.agenticarchitectureskills.com/architecture/enforcement).
* [Choose autonomy for the task](https://www.agenticarchitectureskills.com/architecture/autonomy-contract), with enough supervision capacity to support it.
* [Test proposed improvements](https://www.agenticarchitectureskills.com/architecture/learning-flywheel), [check all ten cross-cutting concerns](https://www.agenticarchitectureskills.com/architecture/concern-matrix), and [examine security threats](https://www.agenticarchitectureskills.com/security).

**Make software usable by agents (/architecture/software-for-agents)**Design interfaces, delegated access, reliable transactions, and human handover.
**Compare technology choices (/decisions)**Explore twenty-five decisions with alternatives, evidence, and conditions that change the answer.

## Adapt the design to your enterprise

A company using agents inside purchased software has different control interfaces from a team operating its own agent platform. Check what each system exposes rather than assuming one gateway observes every action. The [enterprise reference designs](https://www.agenticarchitectureskills.com/library/architecture/master-target-state) compare starting points.

Start from a [business use case](https://www.agenticarchitectureskills.com/use-cases), explore [all fourteen detailed layers](https://www.agenticarchitectureskills.com/layers), or apply an [architecture review skill](https://www.agenticarchitectureskills.com/skills) to a concrete design.

**Detailed system explanations**

[Why this architecture exists](https://www.agenticarchitectureskills.com/architecture/system-view#why-this-architecture-exists)

[The whole thing, on one page](https://www.agenticarchitectureskills.com/architecture/system-view#the-whole-thing-on-one-page)

[The shape](https://www.agenticarchitectureskills.com/architecture/system-view#the-shape)

[The crosswalk](https://www.agenticarchitectureskills.com/architecture/system-view#the-crosswalk)

[The two-estate reality](https://www.agenticarchitectureskills.com/architecture/system-view#the-two-estate-reality)

[Three builds of the same planes](https://www.agenticarchitectureskills.com/architecture/system-view#three-builds-of-the-same-planes)

[Where to go deep](https://www.agenticarchitectureskills.com/architecture/system-view#where-to-go-deep)
