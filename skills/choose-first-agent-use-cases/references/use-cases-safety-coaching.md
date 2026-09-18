# Safety coaching from CCTV events

Help people learn from risky situations while keeping incident evidence and teaching material distinct.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/use-cases/safety-coaching (Markdown: https://www.agenticarchitectureskills.com/use-cases/safety-coaching.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

A detected event still needs review, context, and an appropriate lesson. In this proposed workflow, the agent helps turn a supported finding into coaching that a safety owner can approve.

## See the work first

**Figure: Safety coaching from CCTV events.** Proposed agent extension. Each action remains within an explicitly permitted business process.

**What the image shows:** Detect a candidate CCTV event, verify context and procedure, draft a clearly labeled teaching video, approve identity and delivery, then track learning and recurrence. Original incident evidence remains separate.

Image: https\://www\.agenticarchitectureskills.com/images/use-cases/safety-coaching-v1.webp

**Experience behind this example**

The earlier risk-bot work described by the author processed CCTV streams to find at-risk behavior and create a coaching opportunity. The extension below adds an agent-assisted coaching process; it is not a claim that this complete process was deployed.

## Start with evidence

A detector or vision model identifies a candidate event and returns a timestamp, clip reference, and uncertainty. The agent retrieves the applicable safety procedure and checks whether the evidence actually supports the event label. If it does not, the case remains unconfirmed.

## What the agent adds

For a confirmed case, prepare a short explanation of the safer action and a coaching-video draft. Keep any generated teaching video clearly labeled and separate from the unmodified incident evidence. Verify the recipient through an approved identity process. Route uncertain identity or sensitive content to the responsible safety team before delivery.

## How the investigation proceeds

The loop asks whether the event is supported, whether the correct procedure is available, and whether the recipient is verified. Each missing answer triggers a specific lookup or human review. Stop when the coaching item is ready for its permitted delivery step, or when evidence cannot support it.

## Measure the business result

Measure detection precision, missed events in a reviewed sample, review effort, coaching relevance, delivery errors, and recurrence over a suitable period. Compare with the existing detection-plus-manual-coaching process. Coaching completion alone does not prove a reduction in injury risk.

## Responsibility and failure handling

The safety owner approves the operating policy. The agent cannot determine disciplinary action. Access to clips and recipient data is restricted. A failed delivery stays visible as incomplete; it is not reported as completed coaching.

## Start with a bounded trial

Use a representative historical sample and an agreed reference outcome. Run the proposed process without making live operational changes. Review errors and costs with the people who will own the work. Move to a narrow live scope only when quality, permissions, recovery, and supervision are adequate.

## Explore the architecture

* [Business & industrial systems](https://www.agenticarchitectureskills.com/layers/r05-lob-and-ot).
* [Experiences & channels](https://www.agenticarchitectureskills.com/layers/r09-experience-and-channels).
* [Security & identity](https://www.agenticarchitectureskills.com/layers/r10-security-and-identity).

Continue with [knowledge and memory](https://www.agenticarchitectureskills.com/memory), [value and investment](https://www.agenticarchitectureskills.com/use-cases/value-and-investment), or [practical skills](https://www.agenticarchitectureskills.com/skills).

## External sources

* [NVIDIA video search and summarization blueprint, vendor documentation](https://build.nvidia.com/nvidia/video-search-and-summarization/blueprintcard). Accessed 17 September 2026.

Return to [Energy](https://www.agenticarchitectureskills.com/use-cases/energy) or [explore the agent roles](https://www.agenticarchitectureskills.com/use-cases/agent-roles).
