# Measure value and full cost

Connect agent performance to useful business outcomes and a realistic operating budget.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/use-cases/value-and-investment (Markdown: https://www.agenticarchitectureskills.com/use-cases/value-and-investment.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

Choose the business result before choosing a model. Production throughput, customer resolution, evidence coverage, and proposal quality need different measures.

**Figure: Measure value per completed outcome.** Keep the current process as the comparison. Count outcomes the business accepts.

**What the image shows:** Compare business quality, time, capacity and service with the full cost of models, tools, data, integration, review, rework and operations.

Image: https\://www\.agenticarchitectureskills.com/images/use-cases/value-and-investment-v1.webp

## Establish the starting point

Record the current time, quality, cost, and volume of work, including exceptions. Keep the same definition of a completed outcome when comparing alternatives. Record what changed besides the agent so that unrelated improvements are not attributed to it.

## Count the full cost

Include model calls, tools, infrastructure, data preparation, integration, licenses, human review, retries, incorrect outcomes, and maintenance. See the [full economics model](https://www.agenticarchitectureskills.com/library/architecture/economics-model).

The unit is **cost per resolved outcome**: all model, tool and platform cost for the period, failed and retried attempts included, plus supervision time at a loaded rate, plus the cost of fixing wrong outcomes, divided by the outcomes accepted as resolved under the agreed quality standard. Divide by resolution, never by containment. A cheap run that creates expensive rework is not a cheap outcome. Keep severe or delayed harms visible separately rather than hiding them inside an average.

**Figure: Cost per resolved outcome.** A cheap run that creates expensive rework is not a cheap outcome. Use the same definition of a resolved outcome when you compare options.

**What the image shows:** Model, tool and platform cost, failed and retried attempts included, plus supervision time at a loaded rate, plus the cost of fixing wrong outcomes. The sum is divided by the outcomes accepted as resolved under the agreed quality standard. Side notes say divide by resolution, never by containment, and report the resolution rate, failure rate, serious errors and repeat contacts beside it.

Image: https\://www\.agenticarchitectureskills.com/figures/use-cases/cost-per-resolved-outcome.svg

## Separate different benefits

* Time released creates capacity; it is not automatically a cash saving.
* More qualified opportunities are not yet signed contracts.
* Contract value is not recognized revenue or profit.
* Faster evidence collection is not proof of compliance.
* A larger number of automated actions is not necessarily better service.

## Include the people

Measure the time required to review and resolve exceptions, especially at peak demand. Plan for absence, escalations, and reviewer training. See the [operating model](https://www.agenticarchitectureskills.com/layers/r13-operating-model).

## Decide whether to expand

Continue when quality, value, permissions, and support capacity meet agreed requirements. Change scope when a particular evidence or integration gap dominates the result. Stop when a simpler process delivers a better outcome at acceptable cost.

Use the [portfolio framework](https://www.agenticarchitectureskills.com/library/frameworks/use-case-portfolio) to compare work across departments.

**Figure: The use-case portfolio: gates to funding.** Gate first, then test, then score. A collection of good cases can still exceed the people who supervise them.

**What the image shows:** Ideas pass three gates in order. Gate 1, evaluability: a domain expert can write 20 to 50 pass-or-fail tasks from real failures. Gate 2, the deterministic-zone check: for a decision on access, money, safety actuation or a formal record, the model may only analyse, draft and flag. Gate 3, reliable evidence: a curated corpus with a named owner. A fail goes to the make-it-evaluable queue, to redesign or rejection, or to grounding preparation. Two packaged-application tests follow. One package with a vendor agent available or dated means wait or buy. Across packages, or on an excluded edition, the agent is built thin. Survivors are scored as value per resolved outcome times outcomes per quarter, divided by cost per resolved outcome, times the reversibility factor. Constraints across the whole set include shared supervision capacity. Each funded use case carries kill criteria written at funding time. The portfolio is re-ranked every quarter with measured inputs.

Image: https\://www\.agenticarchitectureskills.com/figures/use-cases/portfolio-gates-to-funding.svg

**Next step:** grow from one task to shared capability on [build an agentic enterprise](https://www.agenticarchitectureskills.com/use-cases/enterprise-transformation).
