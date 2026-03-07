---
layout: single
title: "Real-time Eye-tracking for Search Engine Optimization"
excerpt: ""
header:
  overlay_color: "#dde3ea"

author_profile: false
classes: wide project-page

---
<div class="project-content" markdown="1">

*This research was conducted as part of my Master's degree (M1 internship) at LIG lab (Université Grenoble Alpes)*

--- 



## The Problem

Standard search engine evaluation relies on the Cranfield paradigm — expert-defined queries assessed against fixed document collections. This approach ignores how real users actually behave: they skim snippets, read selectively, and refine their queries progressively based on what they see.

The core question this project addresses: **can a search engine automatically improve its results based on which words a user reads — without asking them to do anything?**

---

## The Hypothesis

When a user scans a Search Engine Results Page (SERP), the words they fixate on carry implicit relevance signal. Two metrics were tested:

- **Longest fixation** — the word a user spent the most time reading in a snippet, indicating deeper cognitive engagement
- **Last fixation before clicking** — the word that triggered the decision to select a result

If these terms are added to the original query automatically, the expanded query should return more relevant results — with no explicit effort from the user.

---

## System Architecture

The proof of concept was built as a standalone Java application mimicking a classic web search engine. It was structured using the Seeheim model — a reference HCI architecture that separates the user interface, dialog controller, and application backend into independent components, making each layer replaceable without affecting the others.

**Key components:**

- **User Interface** — search bar, SERP display with "Refine" button per snippet, built with Java Swing
- **Eye Tracking Analysis** — defines Areas of Interest around individual words, tracks gaze in real time via the Eye Tribe ET1000 device
- **Calculation of Indicators** — implements the fixation metrics and computes query expansion terms
- **Data Collection** — logs all gaze events, queries, and results for analysis
<!-- - **IR Backend** — Terrier V4.0 with custom Python/Perl snippets generator, returning results in XML -->

---
<figure style="width: 50%; margin: 0 auto;">
 <img src="/assets/images/fixations.png" alt="Interface">
  <figcaption>Illustration of the interface</figcaption>
</figure>

---

## User Study

**Participants:** 9 recruited, 7 retained (Eye Tribe ET1000 failed to track 2 participants)

<!-- **Setup:** Desktop computer with eye tracker mounted below screen, 60–70 cm viewing distance, calibration error between 0.37° and 0.48° (within the 0.5° threshold for reading research)

**Corpus:** TIME collection — articles from Time magazine -->

**Task:** Each participant ran 2 queries, scanned the SERP, identified the most relevant snippet, and clicked a "Refine" button to trigger implicit query expansion.

**Two experiments were run:**

**Functional test** — could the system correctly detect the specific word a user was looking at? Result: 3 out of 7 participants. Limited by the consumer-grade eye tracker's sensitivity to head movement and lighting conditions.

**Relevance test** — did query expansion improve search results? Measured using P@5, P@10, and Reciprocal Rank. Result: 4 out of 7 experiments showed improvement on at least one metric; 2 showed degradation. The third query ("Ceremonial suicides of Buddhist monks") showed improvement across all three measures after expansion.

---

## Key Results

Functional test — could the system see what you were reading?
In 3 out of 7 cases, the system correctly identified which word the user was looking at. Put simply : the eye tracker knew where your eyes were roughly half the time. When it worked, the system could pinpoint the exact word driving your interest in a result.

Relevance test — did the search actually get better?
In 4 out of 7 cases, adding the word the user had been looking at to their original query returned at least somewhat better results. In 2 cases, results got slightly worse. One case was unchanged.

---

## Limitations

The Eye Tribe ET1000 is a consumer-grade device with a small tracking box (30×40 cm) — participants who shifted position during the experiment lost gaze tracking. Some participants also clicked "Refine" before finishing reading the target word, breaking the metric logic.

The TIME collection covers historical events only, which reduced ecological validity — participants were less familiar with the topic context than they would be in a real web search.

---

## Takeaways

The project demonstrated that eye gaze enhanced relevance feedback is technically feasible and shows promising results — consistent with prior work using a professional-grade eye tracker (Tobii Pro X3-120). Extrapolating from device performance ratios, a higher-end tracker would be expected to achieve approximately 87% correct word detection, compared to 57% with the consumer device used here.

The modular architecture is designed to be extended — future work could integrate more sophisticated snippet generators, test additional fixation metrics, and evaluate the system on multi-query search sessions that better reflect real web search behavior.

## Reference

[Proof of concept and evaluation of eye gaze enhanced relevance feedback in ecological context](https://www.irit.fr/CIRCLE/wp-content/uploads/2020/06/CIRCLE20_04.pdf)

*Published at CIRCLE 2020. Co-authored with Francis Jambon and Philippe Mulhem, Université Grenoble Alpes.*

</div>