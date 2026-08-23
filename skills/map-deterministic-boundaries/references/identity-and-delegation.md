# The identity and delegation chain

How every action an agent takes stays traceable to the person who asked, at each hop from the agent's own identity to the system of record.

Source: https://www.agenticarchitectureskills.com/architecture/identity-chain (Markdown: https://www.agenticarchitectureskills.com/architecture/identity-chain.md)

> **In plain terms.**
>
> When an AI agent does something in a company system, someone must be able to say which person asked for it. This page describes the chain of checks that keeps that link intact at every step. The agent has its own registered identity, it borrows only the requesting person's permissions, and the business system records the action against that person. The one thing to remember: an agent should never be able to do anything its requesting user could not do themselves.

## The chain

**In short:** An agent acts as the person who asked, and that claim must survive every hand-off from one system to the next.

**Figure: Identity follows the delegation chain.** Every consequential action must identify the agent, requesting person, sponsor, and granted scope.

Entitlement decisions stay in the authoritative identity or record system.

**What the diagram shows:** Delegation chain from accountable sponsor and requesting user through an individually registered agent identity to policy enforcement and the system of record. The sequence contains 6 stages: 1, Sponsor: Owns purpose and risk.; 2, Requesting user: Supplies authority for this task.; 3, ID2 production identity: First-class IAM principal with task scope, audit, and named sponsor.; 4, Policy decision: Checks scope and context.; 5, System of record: Makes final entitlement decision.; 6, Evidence record: Binds action to the full chain..

Diagram: https\://www\.agenticarchitectureskills.com/figures/identity-delegation-chain.svg

**Hop 1: the agent's own identity (the ID2 floor).** Every agent is a first-class principal: an account in its own right. This guide calls that minimum ID2. It means the agent is registered, holds least privilege (only the access its current task needs), uses short-lived credentials, and carries a named sponsor and a risk tier. Sharing a human's credentials is the ID1 anti-pattern. The baseline is bad: non-human identities outnumber human ones by roughly 100 to 1, and 97 percent of them hold more access than they need. Three families of workload identity (the machine equivalent of an ID badge) are in production. Directory-based: the Entra Agent ID class. Standards-track: the IETF WIMSE architecture, where IETF is the Internet Engineering Task Force and WIMSE stands for Workload Identity in Multi System Environments. In that family, SPIFFE (Secure Production Identity Framework for Everyone) already runs for agents in production at scale. OAuth-extension based, where OAuth is the standard web protocol for delegated access. The example is Cross App Access (XAA), adopted as the Enterprise Managed Authorization (EMA) extension of the Model Context Protocol (MCP). It had 25 or more independent software vendors (ISVs) behind it by mid-2026.

**Hop 2: delegation at the gateway.** The gateway, the single door every agent request passes through, exchanges the caller's identity rather than copying it. The mechanisms are token exchange under the internet standard RFC 8693, on-behalf-of flows, and XAA in its EMA form. The IETF ID-JAG draft (Identity Assertion JWT Authorization Grant) joins them as it lands. The gateway injects credentials at execution time, so agents never hold secrets. Access above a minimal baseline is granted just in time for a single action, using OAuth Rich Authorization Requests (RAR, RFC 9396), and drops back automatically afterwards.

**Hop 3: run-as-user in the system of record.** Inside the business system the agent operates run-as-user: it is the requesting person, with that person's permissions and nothing more. The tool layer is a wrapper, not a second policy engine. The system of record keeps its own create, read, update, and delete (CRUD) rules, its field-level security, and its sharing rules in force. Its audit log attributes the action to the human identity. Vendor parity statements now make this explicit: if the user cannot do something in the platform, their agent cannot do it through the tool server.

**Hop 4: constrained identities at the edges.** In operational technology (OT), the systems that run physical equipment, the agent is a security principal with least privilege. Assets without a registered name are not reachable on the network, and access can be cut in seconds. Sub-agents inherit a narrower scope than their parent, never a wider one, and the stated purpose travels with each delegation.

## Sponsor at access identity, presence by exception

**In short:** Every agent carries a named accountable person on its access identity; giving it a mailbox is a separate, rare decision.

The accountable human sponsor is an attribute of the agent's access identity, not a reward for giving it a mailbox. Platform architectures carry the sponsor field on the service principal itself, the agent's own directory account. Agents can be named and mentioned in chat and collaboration tools without any user account. Presence is different. It means a mailbox, a calendar seat, licence consumption, a place in the human resources (HR) system, or a seat on a meeting roster. Presence is a separate, optional, one-to-one user account, granted by an administrator and revocable. It is decided per capability surface, meaning per thing the agent could actually do, and only for a small set of long-lived agents. Being nameable is not the same as having presence.

**Figure: Accountability is not enforcement.** A named sponsor answers for purpose and outcomes; a deterministic control prevents or permits the action.

Both are necessary and neither substitutes for the other.

**What the diagram shows:** Side-by-side distinction between human accountability for purpose and outcomes and technical enforcement of permissions at the action boundary. The comparison contains 2 groups: Accountability, containing Named human sponsor, Purpose and outcome ownership, Exception and appeal responsibility; Enforcement, containing Deterministic policy decision, Permission at the gateway, Allow, deny, limit, or stop.

Diagram: https\://www\.agenticarchitectureskills.com/figures/support-accountability-enforcement.svg

Accountability is also not enforcement. A named sponsor answers for purpose and outcomes. A deterministic control, one that follows fixed rules and always gives the same answer, permits or prevents the action. In testing, a prompt from a phished employee asking an agent to send credentials out of the company succeeded in 24 of 25 attempts. The name on the agent stopped nothing. Both are necessary; neither substitutes for the other.

## Operational floor

**In short:** You must be able to switch any agent off fast, from more than one place, and know from drills how long it takes.

The time it takes to revoke one agent's credentials is a drilled, measured number. Kill switches exist in the identity system as well as in the runtime, the gateway, and the harness (the engineering shell around the model). Each covers what the others cannot. Policy engines fail closed: if the engine fails, the answer is no. Only a minority of enterprises have a formal agent identity strategy. The chain above is what one looks like.

**The research behind this page**

* [The identity and security model](https://www.agenticarchitectureskills.com/library/architecture/identity-security-model)
* [Security and identity findings](https://www.agenticarchitectureskills.com/library/layers/r10-security-and-identity/findings)
* [Productivity and collaboration findings](https://www.agenticarchitectureskills.com/library/layers/r08-productivity-and-collaboration/findings)
