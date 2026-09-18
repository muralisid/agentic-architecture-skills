# Knowledge & memory

Help an agent continue its work, use past experience, and support decisions with evidence.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/memory (Markdown: https://www.agenticarchitectureskills.com/memory.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

An agent should not start every task from nothing. It also should not treat everything it has ever seen as current, trusted, or available to everyone. **Good memory helps it carry work forward and show what supports its decisions.**

**Figure: Three questions before choosing a memory product.** Purpose, retention scope, and representation are different design choices. They can be combined.

**What the image shows:** Working context holds what the model needs now. Thread memory preserves the current case. Long-term memory can retain episodes, facts, and approved methods for future tasks.

Image: https\://www\.agenticarchitectureskills.com/images/memory/memory-map-v1.webp

## Start with a task that continues tomorrow

An agent is collecting evidence for an inspection. Today it finds a report, identifies a missing photograph, and asks for a site check. Tomorrow it should know what remains open. Next month a different investigation may benefit from the completed case, but should not inherit an unverified guess as an established fact.

A long chat transcript alone does not make these distinctions. Neither does putting every document into a vector database. We need to decide what belongs to this task, what may help future tasks, and what must remain traceable to a source.

## Follow the memory story

The main path has three parts. Start with the first and follow the continuation at the end of each page.

**1. Understand what to remember (/memory/memory-types)**Working context, thread memory, and long-term episodes, facts, and procedures. See how they cooperate in one investigation.
**2. Make it usable as evidence (/memory/information-to-memory)**Capture sources, choose representations, combine observations, and handle changing facts and permissions.
**3. Test the design (/memory/what-the-benchmarks-measure)**Check retrieval, answers, and completed work separately. Then investigate cost and performance at scale.

## Go deeper when the question calls for it

The sidebar separates the main story from optional visual tours and advanced design choices. You do not need to read every embedding article to understand memory. The [vector-space tour](https://www.agenticarchitectureskills.com/memory/vector-spaces) explains the different information forms together; its individual articles offer more detail.

The advanced pages compare storage designs, long context, large histories, and research findings. They are choices to investigate, not a list of components every enterprise needs.

Memory supplies evidence within the [enterprise architecture](https://www.agenticarchitectureskills.com/architecture). The [Intelligence ladder](https://www.agenticarchitectureskills.com/ladder) explains how an agent uses that evidence to do useful work at an acceptable cost.
