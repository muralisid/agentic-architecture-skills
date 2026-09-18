# Investigate a water-network anomaly

Bring telemetry, asset history, and field evidence into one bounded investigation.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/use-cases/water-operations (Markdown: https://www.agenticarchitectureskills.com/use-cases/water-operations.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

An alarm identifies unusual behavior, but an operator must still distinguish a faulty sensor, planned work, and a possible network issue. The proposed agent gathers the evidence needed for that decision.

## See the work first

**Figure: Investigate a water-network anomaly.** Proposed agent extension. Each action remains within an explicitly permitted business process.

**What the image shows:** Observe unusual pressure or flow, compare normal operation and recent work, investigate sensor issues, planned changes or leaks, and prepare a reviewed field request.

Image: https\://www\.agenticarchitectureskills.com/images/use-cases/water-operations-v1.webp

**Experience behind this example**

This is a proposed application informed by utility integration experience. It is not presented as a personally delivered autonomous water-operations system.

## Start with evidence

Begin with a defined zone, observation period, sensor quality, and operating conditions. Keep units, sampling interval, missing values, maintenance events, and planned operations with the readings. Compare against an appropriate operating baseline.

## What the agent adds

An agent can retrieve similar historical periods, inspect work orders, and request a sensor check or field investigation. A time-series representation may help find related behavior; it does not establish a leak or equipment fault by itself.

## How the investigation proceeds

Consider competing explanations such as a bad sensor, a planned operating change, or a genuine operational issue. Choose the next check by whether it distinguishes those possibilities. Stop at a justified work request, an unresolved evidence gap, or required operator intervention.

## Measure the business result

Measure confirmed issues, false alarms, missed-event samples, investigation time, and full cost. Compare with existing alarms and an operator’s current workflow before adding a more complex model.

## Responsibility and failure handling

The agent does not change treatment parameters, operate valves, or issue public safety advice. Those actions remain in the utility’s approved engineering and operating processes. A missing reading is not silently converted into a normal state.

## Start with a bounded trial

Use a representative historical sample and an agreed reference outcome. Run the proposed process without making live operational changes. Review errors and costs with the people who will own the work. Move to a narrow live scope only when quality, permissions, recovery, and supervision are adequate.

## Explore the architecture

* [Business & industrial systems](https://www.agenticarchitectureskills.com/layers/r05-lob-and-ot).
* [Data engineering for agents](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering).
* [Operating model](https://www.agenticarchitectureskills.com/layers/r13-operating-model).

Continue with [knowledge and memory](https://www.agenticarchitectureskills.com/memory), [value and investment](https://www.agenticarchitectureskills.com/use-cases/value-and-investment), or [practical skills](https://www.agenticarchitectureskills.com/skills).

## External sources

* [TS2Vec: representation learning for time series](https://arxiv.org/abs/2106.10466). Accessed 17 September 2026.

Return to [Utilities](https://www.agenticarchitectureskills.com/use-cases/utilities) or [explore the agent roles](https://www.agenticarchitectureskills.com/use-cases/agent-roles).
