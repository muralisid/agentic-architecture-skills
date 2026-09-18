# Explore memory in vector space

A visual tour of text, image, video, audio, geospatial, and time-series representations.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/memory/vector-spaces (Markdown: https://www.agenticarchitectureskills.com/memory/vector-spaces.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

You have chosen what the agent should remember. Now choose what a search should treat as similar. These pictures explain the intuition; they are optional deeper reading after the memory foundations.

## Different information needs different representations

An enterprise holds words, photographs, recordings, maps, and readings over time. Turning all of them into short text summaries is convenient, but can lose precisely what a later question needs: a visual feature, a sequence of events, a surface pattern, or a changing signal.

The illustrations are **conceptual maps, not measured embeddings**. Start with text, then look at what changes for other forms of information.

## Text: find related meaning

**Figure: Text: find related meaning.** Text similarity helps locate a passage. It does not establish whether that passage is current or applicable.

**What the image shows:** Text encoder maps two differently worded pump-pressure passages near each other and a leave-policy passage elsewhere. A query retrieves nearby passages while retaining the original source, version, and permissions.

Image: https\://www\.agenticarchitectureskills.com/images/memory/text-space-v1.webp

An embedding represents selected features as numbers so a search can find useful similarities. Picture a space in which related examples lie near each other. What counts as related depends on the model and its training. Actual spaces have many dimensions; a two-dimensional illustration cannot show every relationship.

A representation is not the whole memory. Keep the original sources, exact records, dates, and access rules alongside it. Start with the kind of question the agent will ask.

“Pump pressure is falling” and “low discharge pressure” may belong near each other even though their words differ. This helps find relevant procedures or earlier incidents. An exact asset number, policy version, or quantity still needs an exact check.

[Explore this memory type](https://www.agenticarchitectureskills.com/memory/text-embeddings).

## Images: find visual resemblance

**Figure: Images: find visual resemblance.** Inspect the original image, date, and asset. Visual resemblance is not a diagnosis.

**What the image shows:** Two inspection photographs of corroded pipe joints map to nearby points while clean-valve images form a different group. An aligned text-image model can connect a phrase to visual results. Each result links back to the original image.

Image: https\://www\.agenticarchitectureskills.com/images/memory/image-space-v1.webp

A model can place visually related inspection images near each other, making it possible to look for earlier examples of corrosion or damage. With a suitably aligned text-image model, a written query can also find images. What counts as similar depends on training.

[Explore this memory type](https://www.agenticarchitectureskills.com/memory/image-embeddings).

## Video: find a similar event

**Figure: Video: find a similar event.** Keep timestamps and original clips. A vector is not a directly readable event chronology.

**What the image shows:** A timestamped CCTV clip becomes a representation of an event interval. Similar filmstrips are grouped together; a retrieved result opens the original clip with its camera, start and end time, and surrounding context.

Image: https\://www\.agenticarchitectureskills.com/images/memory/video-space-v1.webp

A video contains change: a person approaches a loading zone, a vehicle moves, or an inspection unfolds. A suitable representation can help search for similar clips or events. Finding a related video is different from locating the exact interval that supports a claim.

[Explore this memory type](https://www.agenticarchitectureskills.com/memory/video-embeddings).

## Audio: find a similar sound

**Figure: Audio: find a similar sound.** Listen to the original and check operating conditions. Similar sounds need not have the same cause.

**What the image shows:** Pump recordings with rattling patterns are grouped separately from a steady hum. Each match opens a recording with equipment and interval metadata. A speech transcript is shown as a separate representation.

Image: https\://www\.agenticarchitectureskills.com/images/memory/audio-space-v1.webp

A pump rattle and a spoken maintenance instruction need different kinds of information. Sound representations can help find acoustic resemblance; a transcript can help find words. Choose the form that preserves what the question asks about.

[Explore this memory type](https://www.agenticarchitectureskills.com/memory/audio-embeddings).

## Geospatial data: find similar places or change

**Figure: Geospatial data: find similar places or change.** Nearby in the representation does not mean nearby on Earth. Annual patterns do not identify an exact event date.

**What the image shows:** Earth patches containing forest, water, fields, and mining ground map into groups by learned surface characteristics rather than physical distance. Yearly representations can be compared, while coordinates, observation intervals, and source observations remain attached.

Image: https\://www\.agenticarchitectureskills.com/images/memory/geospatial-space-v1.webp

A place can be represented by learned surface characteristics and, in some models, behavior over a period. Distant areas may be similar in that space. Comparing the same location across years can guide a change investigation, while exact coordinates and dates remain explicit.

[Explore this memory type](https://www.agenticarchitectureskills.com/memory/location-and-satellite-data).

## Time-series data: find similar behavior

**Figure: Time-series data: find similar behavior.** A similar operating pattern suggests an investigation. It does not establish the same underlying cause.

**What the image shows:** Operating windows with growing oscillations and a spike form a different group from steady signals. A query finds comparable historical windows and returns original readings and confirmed outcomes, with units, duration, and operating state.

Image: https\://www\.agenticarchitectureskills.com/images/memory/time-series-space-v1.webp

The useful resemblance may be a developing oscillation, a spike, or a sequence of changes across pressure and vibration. This lets an agent ask, “What behaved like this before?” Decide whether shape, magnitude, duration, or operating state should matter.

[Explore this memory type](https://www.agenticarchitectureskills.com/memory/time-series).

## These are different spaces, not one universal memory map

Two models can produce vectors of the same length without giving those coordinates the same meaning. Search within a suitable space and combine the resulting evidence by asset, place, time, and source. A jointly trained or explicitly aligned model can support some cross-modal comparisons; do not assume every combination is aligned.

These six types describe the **form of information**. A different question is how long an agent should retain it and how it should be stored. Task context, past events, approved procedures, source records, summaries, and relationships can each use different representations. The [six memory designs](https://www.agenticarchitectureskills.com/memory/six-architectures) examine those storage choices.

**Continue the story:** [Turn media matches into inspectable events](https://www.agenticarchitectureskills.com/memory/images-video-and-audio).
