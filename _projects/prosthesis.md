---
layout: single
title: "Adaptive Training for Prosthetic Control"
excerpt: ""
header:
  teaser: /assets/images/prosthesis_hand.JPG
  overlay_color: "#dde3ea"
# toc: true
# toc_label: "Contents"
classes: wide project-page


---
<div class="project-content" markdown="1">
*The second study in my PhD focused on optimizing prosthetic control to explore performance and human agency in human-machine interaction.*

[View Code](https://github.com/vayneeS/prosthesis-strategies-with-ml)

---

## The Problem

Prosthetic arm users struggle to maintain reliable control of their devices. Training strategies directly impact how quickly users learn to translate muscle signals (EMG) into accurate prosthetic movements — but most systems use random, one-size-fits-all approaches that ignore individual learning needs.

**Question:** Can an adaptive training strategy — one that personalizes gesture selection based on real-time performance — help users learn faster and achieve better long-term control?

---

## Approach

To test the adaptive training strategy, I ran a user study comparing it to two other strategies across 50+ participants:

- **Random** — gestures presented in random order (baseline)
- **User-Choice** — users select gestures based on perceived difficulty
- **Adaptive** — selects gestures based on classifier performance, focusing practice where it matters most

<figure style="width: 50%; margin: 0 auto;">
 <img src="/assets/images/experiment.png" alt="Experiment setup">
  <figcaption>Participants wore a Myo armband and performed gestures following one of three training strategies</figcaption>
</figure>

---

## Data Pipeline Design

**The Challenge:** Raw EMG signals from wearable sensors are produced from muscle contractions, which can change with sensor placement or user fatigue, confusing classification models.

I designed and implemented a data pipeline to turn raw, noisy sensor signals into reliable, actionable data:

1. **Signal cleaning** — removing electrical interference while preserving meaningful muscle activity
2. **Normalization** — standardizing the 8 sensor channels so each contributed equally, similar to balancing audio inputs so no single signal dominates
3. **Aggregation** — consolidating high-frequency predictions (every 200ms) into one performance score per trial, enabling consistent tracking across 120 training rounds per user

**Why it matters:** Without proper preprocessing, models risk learning noise instead of real movement patterns. This pipeline improved data quality, ensured fair comparisons across 50+ users with different physiologies and sensor placements, and made performance metrics robust enough for large-scale analysis.

---

## Machine Learning: How the System Recognizes Gestures

**The Model:** I implemented Linear Discriminant Analysis (LDA) to classify gestures from sensor data. LDA identifies the clearest boundaries between gesture categories by maximizing the separation between them — rather than memorizing individual samples, it learns the core signal patterns that distinguish one gesture from another.

**Why this approach?** The dataset was relatively small (120 training rounds) and the signals were inherently noisy. LDA performs efficiently with limited data and low-dimensional inputs (8 sensor features per gesture). Its simplicity reduces the risk of overfitting and keeps the model stable and interpretable.

**The Adaptive Layer:** After each training round, the system analyzes classification errors to identify which gesture pairs are most frequently confused. These gestures are then prioritized in the next round — instead of random repetition, the training loop focuses on the user's specific weak points.

---

## Statistical Analysis: Validating Impact

**The Objective:** Observing different learning curves was not enough — we needed to validate that the performance gaps between training strategies were statistically meaningful, not random variation.

**Learning Speed:** I quantified each participant's improvement rate over time and compared groups using ANOVA. The adaptive strategy produced significantly faster improvement than the other groups — the likelihood that this difference occurred by chance was less than 0.1%, indicating a strong and reliable effect.

**Skill Transfer:** I evaluated whether participants could apply what they learned to reproduce gestures likely to be recognised by the trained classifier — an indicator of true skill acquisition rather than memorization. Because performance scores were not normally distributed, I used a non-parametric test (Kruskal-Wallis). The adaptive group outperformed the user-choice group, with only a 3% probability that this result was due to chance.

**Effect Size:** Beyond statistical significance, effect size quantifies the magnitude of impact — metrics such as η² (eta squared) for ANOVA and Cohen's d for pairwise comparisons were computed to ensure results were not only statistically significant but also practically meaningful.

---

## Key Results

### 1. Adaptive training reduces time-to-competency
<!-- 
![Learning rates by strategy](/assets/images/Learning_rates_by_strategy.png) -->
*Users exposed to adaptive gesture selection improved significantly faster than those using random or self-directed practice. In practical terms: the adaptive system increases learning speed.*

### 2. Faster learning — without sacrificing final performance

<!-- ![Accuracy across trials](/assets/images/accuracy_across_trials_by_strategy.png) -->
*All groups reached similar peak accuracy by the end of training. The difference lies in speed: users trained with the adaptive strategy achieved proficiency earlier — an efficiency gain with no trade-off in quality.*

### 3. Stronger skill transfer and system understanding

<!-- ![Test accuracy](/assets/images/TPR.png) -->
*When tested on new movement sequences, users trained using the adaptive strategy performed significantly better than users of the user-choice strategy — indicating deeper skill acquisition and better generalization.*

---

## Key Insights

**Faster onboarding**  
Adaptive training reduces time-to-competency by focusing practice on gestures the classifier struggles with. This creates steeper learning curves without requiring more total practice time.  
*Impact: shorter training sessions, lower user frustration, faster clinical deployment.*

**Better user understanding**  
Users trained adaptively developed stronger mental models — they understood why the system responded the way it did, not just how to trigger specific actions.  
*Impact: improved long-term adherence, reduced support load, higher user confidence.*

**Practical implementation**  
The adaptive strategy is simple: select gestures with lowest classifier separability.  
*Impact: easy to integrate into existing prosthetic training systems.*

---

## Recommendations

**For product teams:** Make adaptive training the default onboarding path. Use random/user-choice only as second option for users who already have a clear understanding of how the system works or for those who prefer more control.

**For UX designers:** Insist on the logic behind gesture selection — show users why they're practicing specific movements. This transparency builds trust and strengthens mental models.

**For researchers:** Test this approach beyond prosthetics — any human-ML system where users learn to generate signals (BCIs, rehabilitation tech, surgical training) could benefit from adaptive training.

---

## Reference

[Comparing Teaching Strategies of a Machine Learning-based Prosthetic Arm — HAL Archive](https://amu.hal.science/ISIR_ACIDE/hal-04527854v1)

*Published at IUI 2024. Co-authored with Baptiste Caramiaux, [Nathanaël Jarrassé](https://www.n-jarrasse.fr/), [Téo Sanchez](https://teo-sanchez.github.io/).*

</div>