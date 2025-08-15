---
title: "[Articles] Highly accurate protein structure prediction with AlphaFold"
excerpt: "AlphaFold, solving the grand challenge of predicting protein structure by using Deep NN."
categories:
  - Data Science & ML
tags:
  - [Machine Learning, Bioinformatics, AlphaFold, Deep Learning]
use_math: true
toc: true
toc_sticky: true
date: 2025-08-15
last_modified_at: 2025-08-15
header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---

## About this Article
- **Authors**: John Jumper, Richard Evans, Alexander Pritzel et al.
- **Journal**: Nature
- **Year**: 2021
- **Official Citation**: Jumper, J., Evans, R., Pritzel, A. et al. Highly accurate protein structure prediction with AlphaFold. Nature 596, 583-589 (2021).

<br/>

## Accomplishments
- AlphaFold, solving the grand challenge of predicting protein structure by using Deep NN.

<br/>

## Key Points

### 1. Overview
- AlphaFold combines three theme to predict a protein structure.
    - Neural Network
    - Training procedure based on the evolutionary
    - Physical and geometric constraints
- There are seven key technologies in AlphaFold.
    - Jointly embed Multiple Sequence Alignment (MSA, information about evolution) and pairwise features (information about amino acid pairs).
    - A new output representation and associated loss.
    - A new equivariant(change of input (e.g. rotation) is also applied to the output, without additional computations) attention architecture.
    - Intermediate loss to achieve iterative refinement.
    - Masked MSA loss.
    - Learning from unlabelled protein sequences.
    - Self-estimation of accuracy.

### 2. Architecture
- The following figure is a full architecture of AlphaFold. AlphaFold consists of two parts: Evoformer → Structural Module.

#### 1. Evoformer
- Combine MSA and Pair representation to make a reasoning based on spatial and evolutionary relationships.
- Steps: Below three steps are conducted not once, but continuously.
    (1) Update pair representation matrix by using MSA information. (element-wise outer product)
    (2) Within pair representation, update it in terms of triangles of edges involving three different nodes. By using triangles, you can apply various constraints (e.g. triangular inequality) to figure out unknown information (edge).
    (3) Apply updated pair representation to MSA.

#### 2. Structure Module
- Steps:
    (1) Handle each amino acid separately (residue gas). They start with overlapped state in origin(0, 0, 0), and no rotation.
    (2) Apply Invariant Point Attention(IPA). This adds 3D information of amino acids to Q(query), K(key), V(value) of attention mechanism, without changing their own positions. This process allows to focus on near amino acids, just like the attention mechanism in a sentence. This step 2 is the core of equivariant, which means no need for additional computations when the input is rotated.
    (3) The formation of correct peptide bond geometry, which connects the protein backbone, is encouraged by a violation loss term.
    (4) Side-chain χ angles, pLDDT, PTM scores are calculated.
    (5) Compute the final loss by using Frame-Aligned Point Error(FAPE). In other words, fix one amino acid and calculate the distance difference of the others.
    (6) After prediction, apply Amber force field to get a better structure image.

### 3. Figures & Table Explanation

#### 1. Figure 1: Results on CASP14 datasets, which was a blind test.
- (a): y-axis shows the error between the actual and the predicted one (Median Ca r.m.s.d.95). AlphaFold shows the lowest error.
- (b): Structure comparison between the result of AlphaFold (blue), and of experiment (green).
- (c): Side chain comparison between the result of AlphaFold (blue), and of experiment (green).
- (d): Large protein structure comparison between the result of AlphaFold (blue), and of experiment (green).
- (e): Model structure of AlphaFold.

#### 2. Figure 2: Accuracy of AlphaFold on a large sample of PDB.
- Not only on CASP14 dataset, authors extended to a large PDB dataset.
- (a): Distribution(histogram) of error.
- (b): Correlation between backbone accuracy and side chain accuracy. If backbone prediction is accurate, the prediction of side chain also become accurate.
- (c): Correlation between the actual structural accuracy of prediction (IDDT-Ca) and the accuracy that AlphaFold computed (pLDDT). High correlation shows that the accuracy score of AlphaFold itself is reliable.
- (d): Correlation between the actual fold accuracy of prediction (TM-score) and the accuracy that AlphaFold computed (pTM). High correlation shows that the accuracy score of AlphaFold itself is reliable.

#### 3. Figure 4: Interpreting the NN.
- (a): The result of ablation study for each element of AlphaFold. Self-distillation(student-teacher model) improved the accuracy of AlphaFold. No IPA version was the worst, demonstrating its importance. Although not shown in the graph, BERT style masking also removed the demand of hard coding a particular correlation statistic.
- (b): AlphaFold incrementally improves protein structure as it progresses through each step of the network. In the case of difficult sample such as T1064, AlphaFold searches and rearranges secondary structures.


## Limitations & Possibility for Further Research
1. If MSA is less than 30 sequence, accuracy drops dramatically. MSA is needed to find the correct structure in the aearly stage. However, for MSAs with over 100 sequences, the improvement in accuracy becomes marginal.
2. Low accuracy when (# heterotypic contacts > # intra-chain or homotypic contacts). As AlphaFold uses only one chain as an input, proteins whose structures are determined by the interaction with others could not be predicted accurately. However, there are also exceptions (Figure 5b).
3. Possible to apply in larger scale, such as human genome.