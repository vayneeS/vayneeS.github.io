---
layout: single
title: "3D Flight Summaries"
excerpt: "Automatically generating cinematic highlight videos of electric aircraft trips using virtual camera control and optimization."
header:
  teaser: /assets/images/flight_teaser.png
  overlay_color: "#dde3ea"
tags:
  - 3D Visualization
  - Optimization
  - Urban Mobility
---

*Developed as part of the Uber-X Chair for Integrated Urban Mobility.*

---

## The Vision

As we move toward a world of urban air mobility — where electric aircraft take off vertically from city centers — passengers will want to preview or review their journeys. A full flight might be too long to watch. This research solves the challenge of how to automatically condense a long flight into a short, expressive video that looks like it was filmed by a professional camera crew.

---

## The Challenge: Virtual Camera Control

Capturing a flight in a 3D environment is not as simple as following the aircraft with a camera. To make the video engaging, the system must solve four complex problems simultaneously:

- **Viewpoint** — where should the camera be placed?
- **Planning** — how should the camera move through the city without hitting buildings?
- **Editing** — how do we cut between different shots smoothly?
- **Summarization** — which parts of the trip are the most interesting to show?

---

## How It Works: A Two-Stage Approach

The system mimics the workflow of a film director and editor.

### Stage 1 — Finding the "Wow" Moments

The system analyzes flight data to find the most salient moments — parts where the aircraft is at high altitude, moving at top speed, or performing interesting turns. It uses a mathematical approach (the Knapsack problem) to select the best highlights that fit within a target duration, such as a 30-second summary.

### Stage 2 — Cinematic Camera Work

Once highlights are chosen, the system acts as a camera operator. It follows film grammar principles — the Rule of Thirds and Motion Continuity — to ensure the aircraft is well framed at all times. Advanced optimization ensures camera movements are smooth and free of jerky motion that would be unpleasant to watch.

---

## What this looks like 

![Experiment setup](/assets/images/flight_trajectories.png)
*Trajectory simulation of a VTOL, different colors on the curve show more salient parts of the trajectory, computed using criteria such as interesting viewpoints and cinematographically sound shots*