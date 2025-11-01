---
title: "[Articles] AIVariant: a deep learning-based somatic variant detector for highly contaminated tumor samples"
excerpt: "Developed AIVariant, a deep learning model which can detect single nucleotide variant (potential tumor) even in low sequence depth."
categories:
  - Data Science & ML
tags:
  - [Machine Learning, Deep Learning, Bioinformatics]
use_math: false
toc: true
toc_sticky: true
date: 2025-11-01
last_modified_at: 2025-11-01
header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---

## About this Article
* **Authors**: Hyeonseong Jeon, Junhak Ahn, Byunggook Na, Soona Hong, Lee Sael, Sun Kim, Sungroh Yoon, and Daehyun Baek
* **Journal**: Experimental & Molecular Medicine
* **Year**: 2023
* **Official Citation**: Jeon, H., Ahn, J., Na, B. et al. AIVariant: a deep learning-based somatic variant detector for highly contaminated tumor samples. Exp Mol Med 55, 1734-1742 (2023).

<br/>

## Accomplishments
- Developed AIVariant, a deep learning model which can detect single nucleotide variant (potential tumor) even in low sequence depth.

<br/>

## Key Points

### 1. Three problems of somatic DNA variant analysis
Somatic DNA variants can be used as a detector of tumors. However, there are three difficulties in detecting somatic variants.
- Low tumor purity: Some tumor types needs variant detection even in low purity.
- Low sequencing depth: It is hard to detect variant if the number of reading is low.
- Sequencer specific error
  
To solve this problem authors developed AIVariant, a deep learning model that can overcome the difficulties and detect variants.

### 2. Generating dataset eWGS
1) Actual Positive (Variant) Data <br/>
  Steps: <br/>
      (1) Prepare normal cells and tumor cells of cancer patients (about 100 purity). <br/>
      (2) Discover variants only in the tumor cells. <br/>
      (3) Use the variants as an actual positive (AP).

3) Actual Negative (Sequencer-specific error) Data <br/>
  Steps: <br/>
      (1) Prepare two data from different machine(sequencer). <br/>
      (2) Compare the sequence. <br/>
      (3) If a variant showed up in only one machine, it is a sequencer-specific error.

5) Generating eWGS dataset <br/>

  Steps: <br/>
      (1) Prepare 200x(depth) WGS sequences. <br/>
      (2) Split the dataset into two sets with 30x, one if for normal and the other is for tumor sequence. <br/>
      (3) For the tumor sequence, spike(plant) AP and AN variant. Therefore, 100% true positive data is generated. <br/>
      (4) Mix normal and tumor WGS data in certain ratios, to regulate the purity. The depth of the results are conserved in 30x. <br/>
      (5) Randomly select sequences of the results of step 4, to reproduce various sequence depths.

<br/>

## Figures & Table Explanation

### 1. Figure 2: AIVariant is better than other detectors.
PR-AUC of AIVariant is larger than any other detectors and showed good performance even in low TPs and SD(Sequence Depth)s.
AIVariant was also better than others across all cancer tissue types (Supplementary Figure 3).

### 2. Figure 3: Results on public datasets, which are not used during training.
AIVariant outperformed other detectors on public datasets, which was not used during training.
It was not a top performer in some cases, but the difference was negligible (the cause was the characteristic of the dataset, too high AP ratio).

### 3. Figure 4: Impacts of three components, TPs, SDs, and sequencer-specific errors.
To figure out the impact of TPs, SDs, and sequencer-specific errors, authors deleted one at a time in training set.

- TP: Various-TP model was better than low-TP model in low purity(TP) experiments. In high purity experiments, there was marginal difference.
- SD: Various-SD model was better than low-SD model in low depth(SD) experiments. In deep depth experiments, there was marginal difference.
- Sequencer-specific error (AN): Model with AN outperformed in all experiments.
  
The three components are all important.

<br/>

## Impact of research and Possibility for Further Research
1. Low cost and high accuracy for tumor detection.
Even with low sequence depth, the accuracy of variant detection was high.

2. Expand AIVariant beyond single nucleotide variants.
