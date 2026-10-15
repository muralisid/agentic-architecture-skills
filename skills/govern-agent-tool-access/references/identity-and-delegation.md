# The delegation chain: trace every action to the person who asked

How every action an agent takes stays traceable to the person who asked, from the agent's own identity, through the gateway, to the system of record.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/architecture/delegation-chain (Markdown: https://www.agenticarchitectureskills.com/architecture/delegation-chain.md)
Updated: 2026-10-15
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

An agent changed a record in a business system. Who asked for it, and under whose permissions did it act? The delegation chain answers both questions for every action. The agent has its own registered identity. At the gateway it takes on the permissions of the person who asked, and no more. The business system records the action against that person. At every later hop, access can only get narrower. So an agent can never do anything its requesting user could not do.

**Figure: Identity follows the delegation chain.** Every consequential action must identify the agent, requesting person, sponsor, and granted scope.

Entitlement decisions stay in the authoritative identity or record system.

**What the diagram shows:** Delegation chain from accountable sponsor and requesting user through an individually registered agent identity to policy enforcement and the system of record. The sequence contains 6 stages: 1, Sponsor: Owns purpose and risk.; 2, Requesting user: Supplies authority for this task.; 3, ID2 production identity: First-class IAM principal with task scope, audit, and named sponsor.; 4, Policy decision: Checks scope and context.; 5, System of record: Makes final entitlement decision.; 6, Evidence record: Binds action to the full chain..

Diagram: https\://www\.agenticarchitectureskills.com/figures/identity-delegation-chain.svg

## Three levels of agent identity

Three levels describe how an agent is identified.

* **Shared credentials (ID1).** The agent uses a person's login or a shared service account. Nobody can tell the agent's actions from the person's. Avoid it.
* **The agent's own identity (ID2).** The agent has its own registered account, called an agent identity. It holds only the access its task needs and uses short-lived credentials. It has a named sponsor and a [risk tier](https://www.agenticarchitectureskills.com/architecture/risk-profile). This is the minimum for any agent in production.
* **The agent's own identity plus an agent user account (ID3).** Some agents also need a mailbox, a calendar seat, or a seat in a meeting or chat. That needs a second account, an agent user account. It is a separate decision, made for a few long-lived agents.

Microsoft's products draw the same line. An agent identity lets an agent act on systems. An agent user account lets it join a meeting or a chat.

## Hop 1: the agent's own identity

Every agent is registered before it gets any credential. Its identity is an account in its own right. It holds least privilege, meaning only the access its current task needs. Its credentials are short-lived. It carries a named sponsor and a risk tier. Agent identity belongs to identity and policy, one of [the seven capabilities](https://www.agenticarchitectureskills.com/architecture/system-view) an agent platform provides. It is built in the [security and identity layer (R10)](https://www.agenticarchitectureskills.com/layers/r10-security-and-identity).

The starting point is poor. Non-human identities outnumber human ones by roughly 100 to 1 \[vendor]. About 97 percent of them hold more access than they need \[vendor].

Three kinds of workload identity are in production. A workload identity is the machine version of an ID badge. The first kind lives in a company directory, such as Microsoft Entra Agent ID \[vendor]. The second comes from open standards work at the Internet Engineering Task Force (IETF). SPIFFE, one of those standards, already runs for agents at scale. The third extends OAuth, the standard web protocol for delegated access. Cross App Access is the main example \[vendor].

## Hop 2: delegation at the gateway

The tool gateway sits between agents and the systems they touch. It does not copy the caller's identity. It exchanges it, so the next system sees who asked and through which agent. The standard way is token exchange under OAuth (RFC 8693), or an on-behalf-of flow.

The gateway adds credentials at the moment of the call, so the agent never holds secrets. Access above a small baseline is granted just in time for one action. Then it drops back on its own. How the gateway checks each call is on [enforcement outside the model](https://www.agenticarchitectureskills.com/architecture/enforcement).

## Hop 3: run-as-user in the system of record

Inside the business system the agent acts as the person who asked. It has that person's permissions and nothing more. The system keeps its own rules in force. Those rules say who may read, create, change or delete each record and field. Its audit log names the person.

The tool in between is a wrapper, not a second set of rules. Vendors now say this plainly. If the user cannot do something in the platform, their agent cannot do it either.

## Hop 4: narrower at every edge

A sub-agent gets a narrower scope than the agent that started it, never a wider one. The stated purpose travels with each hand-off.

In operational technology (OT), the systems that run physical equipment, the agent is a security principal with least privilege. Assets without a registered name are not reachable on the network. Access can be cut in seconds.

## The sponsor and the agent user account

Every agent identity carries a named sponsor. The sponsor is the business person who answers for the agent's purpose and results. The sponsor is named when the agent is created, not added later. When a sponsor leaves, Microsoft passes sponsorship to the leaver's manager automatically (3 September 2026) \[vendor].

An agent can be named and mentioned in chat without any user account. An agent user account is different. It brings a mailbox, a calendar seat, a licence, or a place in the HR system. It is optional, granted by an administrator, and revocable. Decide it by what the agent would do with it, and only for a few long-lived agents. Being nameable is not the same as having an account.

**Figure: Accountability is not enforcement.** A named sponsor answers for purpose and outcomes; a deterministic control prevents or permits the action.

Both are necessary and neither substitutes for the other.

**What the diagram shows:** Side-by-side distinction between human accountability for purpose and outcomes and technical enforcement of permissions at the action boundary. The comparison contains 2 groups: Accountability, containing Named human sponsor, Purpose and outcome ownership, Exception and appeal responsibility; Enforcement, containing Deterministic policy decision, Permission at the gateway, Allow, deny, limit, or stop.

Diagram: https\://www\.agenticarchitectureskills.com/figures/support-accountability-enforcement.svg

A sponsor answers for the agent. A rule is what stops an action. In one test, a phished employee's prompt asked an agent to send credentials out of the company. It worked in 24 of 25 attempts. The sponsor's name stopped nothing. You need both.

## Switch any agent off

**Figure: The delegation chain, request to retirement.** An agent should never do more than its requesting user could. Revoke time is drilled and measured.

**What the image shows:** The top lane follows one request. The requesting user and the sponsor lead to the agent, which has its own identity (ID2). The request passes the gateway for token exchange, then the policy decision point. The system of record acts as the user, and the decision lands in the audit trail. A sub-agent branches off the agent, and its scope only narrows. Kill switches sit at the identity, runtime, harness and gateway, and the revoke time is drilled. The bottom lane follows the agent's life: register, entitle with a grant that expires, operate, change, review and retire.

Image: https\://www\.agenticarchitectureskills.com/figures/architecture/identity-request-to-retirement.svg

You must be able to switch any agent off fast, from more than one place. Kill switches sit in the identity system, the runtime, the gateway and the harness. The harness is the engineering shell around the model. Each switch covers what the others cannot. Time how long it takes to revoke one agent's credentials, in drills. Policy engines fail closed: if the engine fails, the answer is no.

The identity is created at the first stage of [the agent lifecycle](https://www.agenticarchitectureskills.com/architecture/agent-lifecycle) and revoked at the last. The level an agent works at is set on [the autonomy contract](https://www.agenticarchitectureskills.com/architecture/autonomy-contract). What its identity lets it reach is one of [the four questions](https://www.agenticarchitectureskills.com/architecture/agent-types) asked of every agent.

## A worked example: booking a referral in a hospital

This is a proposed design. A care coordinator asks an agent to book a referral appointment for a patient. The agent has its own identity and a named sponsor in the outpatient team. At the gateway, its request carries the coordinator's identity. In the scheduling system it acts as the coordinator. It can book only the clinics the coordinator can book. The audit log shows the coordinator, acting through the agent.

The agent passes one sub-task to a second agent that checks the referral letter. That sub-agent can read the letter and nothing else. To stop the agent, the hospital can revoke the identity, block it at the gateway, or stop its runtime. The full design is on [referral coordination](https://www.agenticarchitectureskills.com/use-cases/referral-coordination).

## Evidence and limits

This guide once called this the identity chain. The four hops rest on shipped products and on standards still in progress. As of October 2026, only Microsoft confirms on its own pages that its agent identity is generally available. Google confirms it for one runtime only. Other vendors' dates come from summaries or trade press.

The figures on non-human identities come from vendor surveys. A sponsored survey found that only 23 percent of organisations have a formal agent identity strategy (January 2026). The test of the phished prompt is a single account. The split between an agent identity and an agent user account follows Microsoft's products. Other vendors may draw the line elsewhere.

## Next step

Give the agent a sponsor and a path from registration to retirement on [the agent lifecycle](https://www.agenticarchitectureskills.com/architecture/agent-lifecycle).

**Explore this topic**

* [The identity and security model](https://www.agenticarchitectureskills.com/library/architecture/identity-security-model)
* [Security and identity findings](https://www.agenticarchitectureskills.com/library/layers/r10-security-and-identity/findings)
* [Productivity and collaboration findings](https://www.agenticarchitectureskills.com/library/layers/r08-productivity-and-collaboration/findings)

**Workload identity families.** Directory-based: the Entra Agent ID class \[vendor]. Standards-track: the IETF WIMSE architecture (Workload Identity in Multi System Environments). SPIFFE (Secure Production Identity Framework for Everyone) already runs for agents in production at scale. OAuth-extension based: Cross App Access (XAA), adopted as the Enterprise Managed Authorization (EMA) extension of the Model Context Protocol (MCP). It had 25 or more independent software vendors behind it by mid-2026 \[vendor].

**Delegation at the gateway.** The mechanisms are token exchange under RFC 8693, on-behalf-of flows, and XAA in its EMA form. The IETF ID-JAG draft (Identity Assertion JWT Authorization Grant) joins them as it lands. Just-in-time access uses OAuth Rich Authorization Requests (RAR, RFC 9396).

**Survey figures.** Non-human identities outnumber humans roughly 100 to 1, and 97 percent carry excessive privileges \[vendor surveys]. Only 23 percent of organisations have a formal agent identity strategy (CSA and Oasis, January 2026, sponsored).

**Sponsorship.** Microsoft Entra Agent ID requires a sponsor per agent identity and passes sponsorship to a leaver's manager (Microsoft Learn, 3 September 2026) \[vendor].
