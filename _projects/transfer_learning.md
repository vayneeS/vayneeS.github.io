---
layout: single
title: "Transfer Learning — Group Research Project"
excerpt: "Investigating how domain similarity, data requirements, model size, and robustness are affected by transfer learning across three architectures and multiple datasets."
header:
  overlay_color: "#dde3ea"
  overlay_filter: 0.6
toc: true
toc_label: "Contents"
author_profile: false
tags:
  - Deep Learning
  - Transfer Learning
  - Python
  - PyTorch
  - Computer Vision
---

*Group project completed during the Neuromatch Deep Learning Academy bootcamp.*

[View Code](https://github.com/vayneeS/transfer-learning-exploration)

---

## Overview

after my PhD, as part of an endeavour to continue to grow my skills in AI and ML, I enrolled in a bootcamp on deep learning at the [Neuromatch Academy](https://portal.neuromatchacademy.org/). Neuromatch Academy is a volunteer-led organization, run by computational neuroscientist enthusiasts from all over the world. 
This project investigated four questions about transfer learning — a technique that reuses a model pretrained on one task to accelerate learning on a new, related task. Rather than training a neural network from scratch (which is computationally expensive, time-consuming, and data-hungry), transfer learning transfers the learned parameters of a pretrained network and retrains only a subset of them on the target task.

---

## Question 1 — Does domain similarity affect transfer learning performance?

**Setup:** AlexNet pretrained on ImageNet, evaluated on three target datasets of varying domain similarity:

- **MNIST** — handwritten digit images (close domain)
- **CIFAR-10** — natural images across 10 classes (moderate domain)
- **GTZAN** — audio clips from 10 music genres, converted to spectrograms (distant domain)

**Finding:** Performance dropped substantially as domain distance increased. MNIST and CIFAR-10 both achieved high test accuracy (above 85%), while GTZAN plateaued below 45% — confirming that transfer learning effectiveness depends heavily on how similar the source and target domains are.

---

## Question 2 — Does transfer learning reduce computation time and data requirements?

**Setup:** ResNet-50 pretrained on CIFAR-100, fine-tuned on CIFAR-10. Compared against training from scratch across varying amounts of training data (1%, 20%, 40%, 60%, 100%) and number of epochs.

**Finding:** Transfer learning reached baseline accuracy (91.10%) faster and with less data than training from scratch. Even with only 20% of the training data, the pretrained model approached the performance of a from-scratch model trained on the full dataset — demonstrating clear efficiency gains in both compute and data requirements.

![Computation time](/assets/images/fig1_transfer_learning.png)
*Number of epochs*

![Data needs](/assets/images/fig2_transfer_learning.png)
*Amount of data*

---

## Question 3 — Can a compact model match a complex model in transfer learning?

**Setup:** Three architectures pretrained on ImageNet, fine-tuned on CIFAR-10:

| Model | Parameters |
|---|---|
| AlexNet | 61M |
| ResNet-50 | 25.6M |
| ShuffleNet | 2.3M |

**Finding:** ShuffleNet — with 26x fewer parameters than AlexNet — achieved comparable test accuracy after sufficient training epochs. This suggests that for transfer learning on standard image classification tasks, model complexity is not the primary driver of performance. A well-pretrained compact model can match much larger architectures.

---

## Summary

| Question | Finding |
|---|---|
| Domain similarity | Closer domains produce significantly higher transfer performance |
| Compute & data | Transfer learning reaches baseline faster and with less data |
| Model size | Compact models (ShuffleNet) match complex models in TL settings |
| Robustness | TL excels on clean data; scratch + dropout is more noise-robust |

Transfer learning is most effective when the source and target domains are similar, the training budget is limited, and the test distribution is clean. 