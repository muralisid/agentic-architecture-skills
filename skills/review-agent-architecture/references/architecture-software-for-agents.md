# Make software that agents can use

Give external agents clear capabilities, bounded authority, and reliable business operations.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/architecture/software-for-agents (Markdown: https://www.agenticarchitectureskills.com/architecture/software-for-agents.md)
Updated: 2026-09-17
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

An agent using your product needs to discover what it can do, invoke a well-defined operation, and understand the result. Design that experience alongside the human interface.

**Figure: An agent requests; the product controls the transaction.** A proposed interface pattern. A preview is useful when a change is consequential; not every read needs one.

**What the image shows:** Discover: Read tools and limits. Authorize: User, tenant, purpose. Preview: Validate the intended change. Commit: Execute once, record receipt. Confirm: Read status or hand over

Image: https\://www\.agenticarchitectureskills.com/figures/architecture/software-transactions.svg

## Offer capabilities with clear boundaries

Document inputs, required permissions, side effects, limits, and error behavior. Expose a business operation such as “create inspection request” instead of allowing arbitrary database changes. Explain which operations only read and which make commitments.

## Carry identity through the operation

Keep the customer, user, agent, and task identifiable. The product checks the delegated permission at execution time. A tenant identifier provided by the caller is not proof that the caller may access that tenant. Keep sensitive content out of error messages and diagnostic traces.

## Support work that takes time

Return an operation identifier for a long-running job. Provide a documented status check, cancellation rules, and a resumable handover. Make retry behavior explicit: a repeated request must not silently create another purchase, payment, or inspection.

## Report what actually happened

Return a receipt containing the operation, affected record identifiers, status, and any remaining conditions. Separate acceptance of a job from its completion. Let people see the evidence, current state, unresolved questions, and choices when a task is handed over.

## Make agent use operable

Publish limits and metering semantics. Test incorrect inputs, expired permissions, partial failures, duplicate requests, and cross-customer access. Include example integrations and a small skill only when it helps agents use the product correctly.

## Choose the simplest interface that works

A clear existing API may be sufficient. A tool protocol helps discovery and invocation but does not replace authorization, transaction design, or support ownership. See [tool gateway decisions](https://www.agenticarchitectureskills.com/decisions), [integration](https://www.agenticarchitectureskills.com/layers/r03-integration-fabric), and [identity](https://www.agenticarchitectureskills.com/architecture/identity-chain).
