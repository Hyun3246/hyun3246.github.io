---
title: "[Articles] Robust deep learning-based protein sequence design using ProteinMPNN"
excerpt: "ProteinMPNN, a powerful deep learning tool for protein designing."
categories:
  - Data Science & ML
tags:
  - [Machine Learning, Bioinformatics, Protein Design, ProteinMPNN, Deep Learning]
use_math: true
toc: true
toc_sticky: true
date: 2025-08-20
last_modified_at: 2025-08-20
header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---

## About this Article
- **Authors**: J. Dauparas, I. Anishchenko, N. Bennett, et al.
- **Journal**: Science
- **Year**: 2022
- **Official Citation**: Dauparas, J., Anishchenko, I., Bennett, N., Bai, H., Ragotte, R. J., Milles, L. F., ... & Baker, D. (2022). Robust deep learning-based protein sequence design using ProteinMPNN. Science, 378(6615), 49-56.

<br/>

## Accomplishments
- ProteinMPNN, a powerful deep learning tool for protein designing.

<br/>

## Key Points

### 1. Architecture
Authors used message-passing neural network(MPNN) with three encoder and three decoder layers.

#### Steps:
(1) Input: 3D coordinates of backbone.
(2) Encoder (MPNN): Build information of position of amino acids(nodes), and relationships(edges).
(3) Decoder: Predict the probability of all amino acid for each positions one by one.
(4) Output: Samples from the probability distributions to generate the final amino acid sequence.

### 2. Differentiating points of the model

#### 1. Random Decoding
- Random decoding (in experiment 4) allowed the model to consider context of the following fixed sequence.
- This enables to design protein binder, whose the middle of the sequence is fixed.

#### 2. Multichain Design Problem
- Multichain means that one protein is composed of multiple number of chains.
- Two aspects allowed the difficult 'multichain design problem' possible.
    - Per chain relative positional encoding (Separate encoding for each chain).
    - A binary feature indicating whether the interacting pair of residues are from the same or different chain.

#### 3. Homodimer (Symmetric) Backbone Problem
- **Steps:**
    (1) For each backbone A and B, predict amino-acid probabilities for each position (A1, A2,..., B1, B2 ...) respectively.
    (2) Average these probabilities to create a single, combined probability distribution.
    (3) Sample a single amino acid from this combined distribution and assign it to both positions (A1 and B1).

#### 4. Multistate Design Problem
- Multistate means that one amino acid chain can have several 3D structures.
- The process is similar to that of multichain problem.
- **Steps:**
    (1) Input the structure of state 1 and compute the probability of all positions.
    (2) Input the structure of state 2 and compute the probability of all positions.
    (3) Average the results of step 1 and 2.
    (4) Choose one amino acid for each position based on the result of step 3.

### 3. Protein Designing Ability of ProteinMPNN

#### 1. Amino acid sequences for backbone from AlphaFold
- AlphaFold can generate protein backbones and amino acids sequences through AlphaFold hallucinations (creation-positive meaning). However, their manifestations in E. coli. was terrible.
- By generating amino acid sequences by using Protein MPNN on foundation of backbone from AlphaFold, 73/96 was soluble.
- ProteinMPNN is accurate for both monomers and cyclic oligomers.
    - **Figure 3A**: ProteinMPNN showed more amounts of soluble sequences.
    - **Figure 3B**: A structure from ProteinMPNN showed better thermostability.
    - **Figure 3C**: The SEC result for ProteinMPNN shows a sharp, monodisperse peak, which indicates that the protein is well-folded into a single, stable state rather than being aggregated or misfolded.
    - **Figure 3D**: Result of X-ray crystallography. Green is actual structure and blue is designed by ProteinMPNN. Two structures are similar which means that ProteinMPNN is powerful to designing protein structures.

#### 2. Rescue failed design from Rosetta
- ProteinMPNN can rescue failed designing of Rosetta. It can even find out structures that perform specific functions.
    - **Figure 3E**: Desiged structure by using ProteinMPNN 'typing'.
    - **Figure 3F**: Protein MPNN(orange, green) successfully designed structures which Rosetta failed(blue).
    - **Figure 4A**: Process of rescuing failed structures which performs specific functions from Rosetta.
    - **Figure 4B**: Biolayer interferometry result of experiment Figure 4A. Y-axis shows the cohesion signal of target protein, which was the target of designing. From the leftmost graph, Native peptide, Rosetta, ProteinMPNN, and mutant. In mutant experiment, key residues in the successful ProteinMPNN design were mutated to disrupt the structure. The binding signal is completely abolished, which proves that the original design's success was due to the specific structural features engineered by ProteinMPNN, not random chance.

#### 3. Internal repeat + cyclic symmetry protein designing
- Internal repeat: A same unit structure is reaped in a single chain.
- Cyclic symmetry: Internal repeat assembles to form a ring.
- Finding a structure satisfying both conditions is difficult problem, but ProteinMPNN can.
    - **Figure 3G, H**: Designed model of Internal repeat & cyclic symmetry protein designing.
    - **Figure 3I, J**: Negative-stain EM results. ProteinMPNN exactly designed the desired structure.

#### 4. Nanoparticle assemblies
- ProteinMPNN can design nanoparticle assemblies. This feature is useful for designing vaccine.
    - **Figure 3K**: Designed result of nanoparticles.

<br/>

## Figures & Table Explanation

### 1. Table 1: Improvements on model performance with modifications.
- By modifying several aspects of the basic architecture, authors achieved better performance.

### 2. Figure 2:
- **(A)**: ProteinMPNN vs Rosetta (common model). In x-axis, from left to right is center of protein → surface. ProteinMPNN showed better performance.
- **(B)**: Accuracy with respect to the types of proteins.
- **(C)**: Success rate of AlphaFold prediction (y-axis) with respect to noise. A little noise is better because it ProteinMPNN focuses on overall structural characteristics rather than details.
- **(D)**: Impact of temperature when making a sequence. High temperature can increase diversity.
- **(E)**: Native Sequence vs ProteinMPNN sequence. As Protein MPNN sequence reflects structure-sequence information stronger than native sequence, AlphaFold is more accurate on ProteinMPNN.
- **(F)**: Rosetta sequence is redesigned by ProteinMPNN. AlphaFold showed better performance.

<br/>

## Possible Applications
1. Broadly used for protein design
    - High rate of design success, compute efficiency, applicability to almost all protein design problem, and lack of requirement for customization.
2. Structure determination of designed protein.
    - ProteinMPNN-generated sequences have a higher tendency to crystallize.
3. Improving expression and stability of recombinantly expressed native proteins.
    - ProteinMPNN-generated sequences are fold to native protein backbones more confidently and accurately than original native sequences.