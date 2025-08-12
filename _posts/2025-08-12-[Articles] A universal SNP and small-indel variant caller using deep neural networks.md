---
title: "[Articles] A universal SNP and small-indel variant caller using deep neural networks"
excerpt: "Introducing Deep Variant, powerful AI tool for finding variation on genome."
categories:
  - Data Science & ML
tags:
  - [Machine Learning, Bioinformatics, Genomics, DeepVariant, Deep Learning]
use_math: true
toc: true
toc_sticky: true
date: 2025-08-12
last_modified_at: 2025-08-12
header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---

## About this Article
- **Authors**: Ryan Poplin, Pi-Chuan Chang, David Alexander, Scott Schwartz, et al.
- **Journal**: Nature Biotechnology
- **Year**: 2018
- **Official Citation**: Poplin, R., Chang, PC., Alexander, D. et al. A universal SNP and small-indel variant caller using deep neural networks. Nat Biotechnol 36, 983-987 (2018).

<br/>

## Accomplishments
- Introducing Deep Variant, powerful AI tool for finding variation on genome.

<br/>

## Key Points

### 1. Pipeline (Architecture)
- Step 1: By scanning BAM(text file), figure out suspicious spots of variations.
- Step 2: By using the information from step 1, make pileup image. Pileup image is an image that reads from Next Generation Sequencing are aligned along the reference sequence.
- Step 3: Train Deep CNN by using true genotype and pileup images. Now, preparation for a new prediction is complete.
- Step 4: Enter a new pileup image as an input.
- Step 5: Deep Variant returns the variation likelihood of the genotype.

<br/>

### 2. Advantages of Deep Variant

#### 1. Powerful than GATK (SOTA model based on probabilistic theory)
- Better performance.
- Greater consistency.

#### 2. Powerful than all other methods
- Won 'highest performance' award for SNP in FDA-sponsored Truth Challenge 2016 (evaluated on sample NA24385).
- This blind test result shows that Deep Variant is also powerful to unseen dataset.
- Powerful than all other methods with more than 50% fewer errors per genome (sample NA24385). (Table 1)
- Outperformed all other methods even in artificially synthesized sample CHM1-CHM13 (Table 2).

#### 3. Versatility and expandability
- Robust to changes in sequencing depth. Performed well on other version of genome without additional training.
- Can applied to other mammalian species (e.g. mouse).
- No further performance loss in other instrument types, preparation protocols.
- If retraining is conducted in parallel, Deep Variant can be applied to exome data (gene on exon) which is hard because of shortage of data.

<br/>

## Limitations & Possibility for Further Research
1. Changing to RGB image is not always optimal.
2. Rely on sensitivity of candidate callset (created by step 1).
3. The process (finding candidates -> making images -> apply CNN) is applicable to other fields.