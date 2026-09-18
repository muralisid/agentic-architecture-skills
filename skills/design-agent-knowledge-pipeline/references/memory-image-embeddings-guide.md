# Image embeddings: search by visual features

Find related inspection images while keeping the original observation available.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/memory/image-embeddings (Markdown: https://www.agenticarchitectureskills.com/memory/image-embeddings.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

A model can place visually related inspection images near each other, making it possible to look for earlier examples of corrosion or damage. With a suitably aligned text-image model, a written query can also find images. What counts as similar depends on training.

**Figure: Images: find visual resemblance.** Inspect the original image, date, and asset. Visual resemblance is not a diagnosis.

**What the image shows:** Two inspection photographs of corroded pipe joints map to nearby points while clean-valve images form a different group. An aligned text-image model can connect a phrase to visual results. Each result links back to the original image.

Image: https\://www\.agenticarchitectureskills.com/images/memory/image-space-v1.webp

## What the space represents

The image illustrates a model placing related visual features near each other. It may be useful for finding earlier inspection images that resemble a new observation. The useful features depend on training; a model may attend to background or camera style when the task needs fine surface damage.

An aligned text-image model can connect a phrase to images. CLIP provides a research example. This does not mean arbitrary text and image encoders share a comparable space.

## What to retain beside the vector

Keep the original image, asset identity, capture time, camera context, image region if one is used, source reference, permissions, and model version. A result should open the image that produced it.

## Where the first approach can fail

A generated caption can omit a small crack. Visually similar corrosion can occur on different components with different consequences. Darkness, occlusion, and viewpoint can affect what is visible. Evaluate actual inspection conditions, including cases that must not be treated as matches.

## How it serves a decision

Use resemblance to find useful comparisons. Have the decision rely on the inspected image and the applicable engineering criteria, with uncertainty recorded. [Combine images with other evidence](https://www.agenticarchitectureskills.com/memory/combining-evidence) and preserve [media event context](https://www.agenticarchitectureskills.com/memory/images-video-and-audio).

## External source

[CLIP: connecting text and images](https://openai.com/index/clip/), 2021. Reviewed 18 September 2026.
