# Investigate production discrepancies

Combine visual measurements with production records to find and explain differences.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/use-cases/production-measurement (Markdown: https://www.agenticarchitectureskills.com/use-cases/production-measurement.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

When production estimates disagree, a dashboard shows the gap without explaining it. This proposed investigation checks the measurements and operating records before a person accepts an adjustment.

## See the work first

**Figure: Investigate production discrepancies.** Proposed agent extension. Each action remains within an explicitly permitted business process.

**What the image shows:** Compare calibrated visual measurements with scales and production records, investigate timing and calibration, then reconcile with an accountable owner. Preserve units, uncertainty and source measurements.

Image: https\://www\.agenticarchitectureskills.com/images/use-cases/production-measurement-v1.webp

**Experience behind this example**

The author described computer-vision work around iron-ore production measurement. This proposed extension investigates inconsistent measurements rather than treating one model output as the final production figure.

## Start with evidence

Keep the original image, camera calibration, measurement interval, equipment identity, and uncertainty with the visual estimate. Reconcile it with available weighbridge, belt-scale, survey, or production-system evidence. Volume needs an appropriate density assumption before it becomes an estimate of mass.

## What the agent adds

When the estimates differ materially, an agent can check maintenance events, sensor health, operating interruptions, and record timing. It can request another measurement or prepare a reconciliation case with competing explanations. The accepted production record remains a controlled business decision.

## How the investigation proceeds

Use the size and timing of a discrepancy to choose the next evidence request. For example, a difference only during a camera outage suggests a different check from a difference across every shift. Stop when the discrepancy is explained within an agreed tolerance or needs an engineer.

## Measure the business result

Measure error against an accepted reference, unresolved discrepancy rate, investigation time, and the cost of calibration and review. Compare a fixed reconciliation rule with the adaptive agent. Track the economic effect only after demonstrating that the measurement is reliable.

## Responsibility and failure handling

Do not let generated explanations replace measurements. Preserve units, uncertainty, timing, and every adjustment. Missing or uncalibrated evidence should produce an unresolved case rather than an apparently precise tonnage.

## Start with a bounded trial

Use a representative historical sample and an agreed reference outcome. Run the proposed process without making live operational changes. Review errors and costs with the people who will own the work. Move to a narrow live scope only when quality, permissions, recovery, and supervision are adequate.

## Explore the architecture

* [Business & industrial systems](https://www.agenticarchitectureskills.com/layers/r05-lob-and-ot).
* [Systems of record](https://www.agenticarchitectureskills.com/layers/r04-systems-of-record).
* [Data engineering for agents](https://www.agenticarchitectureskills.com/layers/r14-agent-data-engineering).

Continue with [knowledge and memory](https://www.agenticarchitectureskills.com/memory), [value and investment](https://www.agenticarchitectureskills.com/use-cases/value-and-investment), or [practical skills](https://www.agenticarchitectureskills.com/skills).

## External sources

* [Roboflow Workflows documentation](https://docs.roboflow.com/workflows). Accessed 17 September 2026.

Explore [mining and resources](https://www.agenticarchitectureskills.com/library/blueprints/verticals/mining-and-resources) or [explore the agent roles](https://www.agenticarchitectureskills.com/use-cases/agent-roles).
