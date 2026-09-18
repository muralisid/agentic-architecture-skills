# Represent how equipment behaves over time

Find similar operating periods without discarding units, duration, or context.

Author: Murali Sid (https://linkedin.com/in/muralisid)
Source: https://www.agenticarchitectureskills.com/memory/time-series (Markdown: https://www.agenticarchitectureskills.com/memory/time-series.md)
Updated: 2026-09-18
Licence: CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/)

## An average can hide the event you are looking for

Two operating periods can have a similar average vibration level while one contains a brief spike and the other a growing oscillation. Storing only the average makes those periods hard to distinguish. Comparing raw readings point by point can also miss a useful resemblance when equipment runs at different scales.

The aim is to make the relevant behavior searchable while retaining the units and duration that affect its meaning. Decide what should count as similar before choosing an encoder.

**Figure: Time-series data: find similar behavior.** A similar operating pattern suggests an investigation. It does not establish the same underlying cause.

**What the image shows:** Operating windows with growing oscillations and a spike form a different group from steady signals. A query finds comparable historical windows and returns original readings and confirmed outcomes, with units, duration, and operating state.

Image: https\://www\.agenticarchitectureskills.com/images/memory/time-series-space-v1.webp

## Define the observation window

“Find periods like this pump’s last 30 minutes” is different from “Find a pump with the same average pressure”. Keep the sampling interval, missing readings, channels, and operating conditions with the window.

## Decide what similar should mean

Two signals may have the same shape at different magnitudes. Normalization can make them look alike while hiding an operationally important difference. A short spike and a sustained excursion should not become interchangeable merely because they share a peak.

## Learn and test the representation

TS2Vec learns timestamp-level contextual representations and can aggregate them over a subsequence. That provides a concrete example of time-series representation learning. It does not prove usefulness on a particular utility or mining dataset.

## Separate retrieval from forecasting

A model trained to forecast future values may contain useful internal representations, but forecasting accuracy is not evidence that nearest-neighbor retrieval finds the right historical episodes. Evaluate the proposed search task directly.

## Keep the outcome in view

Retrieve the original readings and the subsequent confirmed event, not just an embedding score. Compare with thresholds, simple features, and existing operator practice. Include periods that look similar but have different causes.

Follow the proposed [water-operations investigation](https://www.agenticarchitectureskills.com/use-cases/water-operations).

## External sources

* [TS2Vec: representation learning for time series](https://arxiv.org/abs/2106.10466). Accessed 17 September 2026.
