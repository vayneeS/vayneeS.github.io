---
layout: single
title: "Personalizing Motor Learning with Machine Learning"
excerpt: "How a multi-armed bandit algorithm can adapt motor skill training in real time — producing smoother, more expert-like movements than random practice."
header:
  overlay_color: "#dde3ea"
  toc: true
  toc_label: "Contents"
tags:
  - Python
  - Reinforcement Learning
  - HCI
  - Rehabilitation
  - Statistical Analysis
---
An overview of my first PhD study, supervised by [Baptiste Caramiaux](https://baptistecaramiaux.com/). I explored how machine learning can personalize motor skill training to improve outcomes, in particular, how to tailor practice schedules to individual learners.

---
## The Challenge

Every day, millions of people work to master physical skills — stroke survivors relearning to write, athletes perfecting their technique, surgeons training for precision procedures. Yet traditional training follows a **one-size-fits-all approach** that ignores a fundamental truth: *everyone learns differently*.

What if we could give every learner their own adaptive coach — one that monitors movements and adjusts training instantly?

---

## Approach: Machine Learning Meets Motor Learning

Random practice has been shown to be effective for learning motor skills, but does not consider the skill level of the learner. During my PhD, I set out to answer a critical question: **can machine learning personalize motor skill training more effectively than a random practice schedule?**

### The Experiment

My team and I designed a controlled study where participants learned to trace curved paths using an infrared marker — a task that mirrors real-world motor challenges in rehabilitation (regaining hand control) and professional training (surgical precision).

By varying the channel width, we controlled difficulty: *narrow channels = harder, wide channels = easier*. Instead of following a fixed training sequence, an **Machine Learning algorithm decided which difficulty to present next**, based on each learner's real-time performance.

![Experiment setup](/assets/images/experiment1.png)
*Simplified illustration of the experiment setup, with an infrared marker on a stick tracing paths inside a channel whose width was changed dynamically by the algorithm.*

### The Machine Learning Strategy

We used a **multi-armed bandit algorithm** — a technique that balances trying new challenges (exploration) with reinforcing what works (exploitation). The system continuously analyzed two key metrics:

- **Accuracy** — can the learner stay within the path?
- **Movement smoothness (jerk)** — how expert-like are their movements?

Based on these signals, the AI selected the next exercise to maximize learning progress — just like an expert therapist would, but at scale.

---

## What We Discovered

Compared to traditional random practice and semi-adaptive methods, the AI-personalized training produced two key results:

**Superior movement quality**
Learners achieved smoother, more expert-like movements — the hallmark of true motor mastery. In rehabilitation, this means safer, more natural motion. In professional training, it translates to efficiency and precision.

**Better skill transfer**
Skills learned with AI guidance transferred better to new situations. This is critical: stroke patients must adapt skills to daily life, athletes face ever-changing conditions, trainees encounter scenarios beyond their practice.

### Why Movement Smoothness Matters

While accuracy is important, **smoothness is the hidden marker of expertise**. Surgeons with smoother hand motions make fewer errors. Athletes with fluid movements use energy more efficiently and reduce injury risk. Rehabilitation patients with smoother motion regain functional independence faster.

Our AI did not just help people complete the task — it helped them develop *higher-quality motor skills* that matter in the real world.

---

## Real-World Applications

- **Rehabilitation technology** — adaptive therapy apps that adjust exercises for stroke recovery, motor impairment, or injury rehabilitation
- **EdTech platforms** — intelligent tutoring systems for music, sports, craftsmanship, or any skill requiring physical mastery
- **Professional training** — surgical simulation, precision manufacturing, and technical skills where movement quality determines success
- **Accessible coaching** — bringing personalized training to underserved populations who lack access to expert therapists or coaches

---

## The Takeaway

With traditional motor learning, human experts may adapt exercises, but only for a small number of people at a time. With AI, this kind of personalized support becomes accessible to many more learners.

One promising direction for more complex movements e.g. sports: combining the expertise of a coach with the reliability of technology by allowing the expert to guide the AI's adaptations — for example, using *ontologies* to encode expert knowledge about skill progression, which the AI can leverage to make more informed decisions.

---

## References


[Interactive curriculum learning increases and homogenizes motor smoothness](https://www.nature.com/articles/s41598-024-53253-3)

*Published in Scientific Reports 2024. Co-authored with Baptiste Caramiaux, Antoine Loriette and Olivier Sigaud.*