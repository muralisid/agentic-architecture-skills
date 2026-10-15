# The fourteen layers

The fourteen parts of the enterprise estate that agents touch, grouped by the job they do, with one page for each: what sits there today, what agents add, and what must be true first.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/layers (Markdown: https://www.agenticarchitectureskills.com/layers.md)
Updated: 2026-10-15
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

Agents do not arrive on a blank page. They sit on technology a company already runs, from its servers to the people who supervise the work. This guide splits that estate into fourteen layers you own. Every agent passes through [a lifecycle you run](https://www.agenticarchitectureskills.com/architecture/agent-lifecycle), from registration to retirement. Each stage of that lifecycle calls on [seven capabilities you add](https://www.agenticarchitectureskills.com/architecture/system-view), such as a tool gateway and an audit trail. Agents touch all fourteen layers. Find the layer you run in the groups below, and read its page.

**Figure: Fourteen layers you own, seven capabilities you add.** The layers are what the enterprise owns; the seven capabilities are what it adds so governed agent work can run across them.

A layer can contribute to more than one capability; the capabilities cut across the estate rather than containing its layers.

**What the diagram shows:** Crosswalk matrix showing the fourteen enterprise layers down the rows and the seven agent platform capabilities across the columns, with several layers contributing to more than one capability. The matrix crosses R01 Infrastructure, R02 Data platform, R03 Integration fabric, R04 Systems of record, R05 LOB and OT, R06 Intelligence and learning, R07 Agent platform, R08 Productivity and collaboration, R09 Experience and channels, R10 Security and identity, R11 Governance, risk and sovereignty, R12 Observability and FinOps, R13 Operating model, R14 Agent data engineering with Runtime, Tool gateway, Knowledge and memory, Identity and policy, Evaluation and release, Observability and audit trail, Human oversight. Annotated cells are R01 Infrastructure by Runtime: Runtime and model serving; R02 Data platform by Knowledge and memory: Governed source data; R03 Integration fabric by Tool gateway: Gateway and tool path; R04 Systems of record by Tool gateway: Authoritative action boundary; R05 LOB and OT by Tool gateway: Operational actuation boundary; R06 Intelligence and learning by Evaluation and release: Evaluation and promotion; R07 Agent platform by Runtime: Agent runtime; R07 Agent platform by Identity and policy: Registry and runtime controls; R08 Productivity and collaboration by Human oversight: Human work surface; R09 Experience and channels by Human oversight: Customer and employee edge; R10 Security and identity by Identity and policy: Identity and policy; R11 Governance, risk and sovereignty by Identity and policy: Risk and sovereignty rules; R11 Governance, risk and sovereignty by Observability and audit trail: Decision and consultation records; R12 Observability and FinOps by Observability and audit trail: Independent traces and cost; R13 Operating model by Human oversight: Accountability and supervision; R14 Agent data engineering by Knowledge and memory: Curation and memory; R14 Agent data engineering by Evaluation and release: Eval-data flywheel. Important boundary: The cells show primary contributions, not exclusive ownership. Every deployed workload uses all seven capabilities across the relevant layers.

Diagram: https\://www\.agenticarchitectureskills.com/figures/layers-planes-crosswalk.svg

**Figure: The fourteen layers, grouped by the job they do.** Start with the job you want to understand, then pick the layer. Real work touches several groups at once.

**What the image shows:** Six groups of layers. Run the agents holds infrastructure and compute (R01) and the agent platform (R07). Let them act holds the integration fabric (R03), systems of record (R04), and line of business and OT (R05). Give them knowledge holds the data platform (R02) and agent data engineering (R14). Control and check them holds security and identity (R10), governance, risk and sovereignty (R11), and observability and FinOps (R12). Improve them holds intelligence and learning (R06). Work with people holds productivity and collaboration (R08), experience and channels (R09), and operating model and supervision (R13). Every agent touches several layers at once.

Image: https\://www\.agenticarchitectureskills.com/figures/layers/fourteen-layers-by-job.svg

## Run the agents

| Layer                                                                                                   | What good looks like                                                                                              |
| ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| [Infrastructure and compute (R01)](https://www.agenticarchitectureskills.com/layers/r01-infrastructure) | Each agent session is sealed off, with one guarded exit and its own identity. Model capacity is rented by default |
| [Agent platform (R07)](https://www.agenticarchitectureskills.com/layers/r07-agent-platform)             | Buy the runtime that runs agents. Build your own code around the model, and test every change before release      |

## Let them act

| Layer                                                                                               | What good looks like                                                                       |
| --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| [Integration fabric (R03)](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric) | One tool gateway checks every agent request, supplies the credentials and keeps the record |
| [Systems of record (R04)](https://www.agenticarchitectureskills.com/layers/r04-systems-of-record)   | Agents act as the person who asked. The business system keeps its own permission checks    |
| [Line of business and OT (R05)](https://www.agenticarchitectureskills.com/layers/r05-lob-and-ot)    | Agents advise the people who run equipment. They never control it                          |

## Give them knowledge

| Layer                                                                                                       | What good looks like                                                                               |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| [Data platform (R02)](https://www.agenticarchitectureskills.com/layers/r02-data-platform)                   | Agents find only what the person asking may open, and every answer shows its source                |
| [Agent data engineering (R14)](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering) | Data is prepared for agents with an owner and a source on every piece. Deletion reaches every copy |

## Control and check them

| Layer                                                                                                                      | What good looks like                                                                            |
| -------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| [Security and identity (R10)](https://www.agenticarchitectureskills.com/layers/r10-security-and-identity)                  | Every agent has its own identity. A fixed rule outside the model checks each risky action       |
| [Governance, risk and sovereignty (R11)](https://www.agenticarchitectureskills.com/layers/r11-governance-risk-sovereignty) | A register of every agent, records kept to match the risk, and data kept where the law requires |
| [Observability and FinOps (R12)](https://www.agenticarchitectureskills.com/layers/r12-observability-and-finops)            | A trace of every step that the agent cannot alter, and a budget it cannot exceed                |

## Improve them

| Layer                                                                                                             | What good looks like                                                                                                          |
| ----------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| [Intelligence and learning (R06)](https://www.agenticarchitectureskills.com/layers/r06-intelligence-and-learning) | Experts write the tests. Model judges are checked against people. A change ships only after it passes, and can be rolled back |

## Work with people

| Layer                                                                                                                       | What good looks like                                                                                            |
| --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| [Productivity and collaboration (R08)](https://www.agenticarchitectureskills.com/layers/r08-productivity-and-collaboration) | Office agents act with their own agent identity. A user account that joins meetings and chats is granted rarely |
| [Experience and channels (R09)](https://www.agenticarchitectureskills.com/layers/r09-experience-and-channels)               | Agents that talk to customers get their own front door, because what they say carries legal weight              |
| [Operating model and supervision (R13)](https://www.agenticarchitectureskills.com/layers/r13-operating-model)               | Supervisor capacity is planned like a queue, counting waiting time and the busiest ten minutes                  |

## How the pages are built

Every layer page follows the same order.

1. An opening paragraph: what the layer is, what sits in it today, and what agents need from it.
2. What sits in this layer today. A table shows the systems in four kinds of organisation. They are an electricity distributor, a water utility, a hospital network, and a generator or miner.
3. What agents add to the layer.
4. What must be true before an agent touches it, and where that rule is enforced.
5. Choices and their verdicts, each linked to the [decision catalog](https://www.agenticarchitectureskills.com/decisions).
6. The concerns this layer must honour, linked to the [concern matrix](https://www.agenticarchitectureskills.com/architecture/concern-matrix). A concern is a requirement every layer must honour, such as identity, privacy or cost.
7. Evidence and limits: what the sources support and where they stop.
8. A next step, and the research behind the page with its dated sources.

The research for each layer, with findings and sources, is in [the research library](https://www.agenticarchitectureskills.com/library/layers).

## Evidence and limits

The list of fourteen layers is this guide's own. No standards body publishes one. The Cloud Security Alliance's MAESTRO model has seven layers of an agentic system (6 February 2025). That is a different list, about the agent system itself, not the enterprise around it.

The systems named in each layer table come from industry knowledge and three research briefs written on 15 October 2026. Vendor names are examples, not a market-share claim.

## Next step

Read the page for the layer you run. If you are new to the guide, start with [Start here](https://www.agenticarchitectureskills.com/start), then [the agent lifecycle](https://www.agenticarchitectureskills.com/architecture/agent-lifecycle).
