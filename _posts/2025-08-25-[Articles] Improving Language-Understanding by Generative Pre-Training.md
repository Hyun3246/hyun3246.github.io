---
title: "[Articles] Improving Language-Understanding by Generative Pre-Training"
excerpt: "Introducing Generative Pre-Training (GPT) model."
categories:
  - Data Science & ML
tags:
  - [Machine Learning, NLP, GPT, Transformer, Pre-training, Fine-tuning]
use_math: true
toc: true
toc_sticky: true
date: 2025-08-25
last_modified_at: 2025-08-25
header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---

## About this Article
- **Authors**: Alec Radford, Karthik Narasimhan, Tim Salimans, Ilya Sutskever
- **Journal**: OpenAI
- **Year**: 2018
- **Official Citation**: Radford, A., Narasimhan, K., Salimans, T., & Sutskever, I. (2018). Improving language understanding by generative pre-training. OpenAI.

<br/>

## Accomplishments
- Introducing Generative Pre-Training (GPT) model.

<br/>

## Key Points

### 1. Architecture
The basic architecture is from Transformer architecture. However, Generative Pre-Training(GPT) model only uses decoder (decoder-only model).

### 2. Training Steps
Training consists of two parts: unsupervised pre-training and supervised fine-tuning.

#### 1. Unsupervised Pre-Training
- **Purpose**: Learning universal representation that needs little adaptation to various tasks.
- **Objective function**: Maximize the following formula, which represents the conditional likelihood of i-th token u_i, when only the previous tokens u_{i-k},...,u_{i-1} are given.
  
  $L_{1}(\mathbb{U})=\sum_{i}log~P(u_{i}|u_{i-k},...,u_{i-1};\Theta).$
  
- **Specific Steps**:
  
  $h_{0}=U~W_{e}+W_{P}$
  
  $h_{l}=\text{transformer block}(h_{l-1}) \forall i \in [1,n]$
  
  $P(u)=\text{softmax}(h_{n}W_{e}^{T})$

#### 2. Supervised Fine-Tuning
- **Purpose**: Customizing a model to specific tasks.
- **Specific Steps**: One additional layer is needed in fine-tuning.
    (1) Labeled input(dataset) goes into pre-trained model.
    (2) Output vector $h_{l}^{m}$, which contains contextual meaning of given data(sentence).
    (3) Output of step 2 goes into a layer(with parameters $W_{y}$), which is a special layer for a specific task.
    (4) Final label y is achieved.
- **Computing probability**: In fine-tuning, it is important to exactly predict the label y of a task. The probability is computed as:
  
  $P(y|x^{1},...,x^{m})=\text{softmax}(h_{l}^{m}W_{y}).$
  
- **Objective function**: Maximize the following formula, which represents the probability of label y, when the whole sentence are given.
  
  $L_{2}(\mathbb{G})=\sum_{(x,y)}log~P(y|x^{1},...,x^{m}).$
  
- **Final objective function with auxiliary objective**: To prevent the model to forget the basic knowledge gained from pre-training, adding an auxiliary objective is helpful. Therefore, the final objective is a mix(ratio λ) of the two objectives above.
  
  $L_{3}(\mathbb{G})=L_{2}(\mathbb{G})+\lambda*L_{1}(\mathbb{G})$
  
- **Task-specific input transformations**: By modifying input formats, there was no need to change the model architecture when applying to multiple types of tasks.

<br/>

## Figures & Table Explanation

### 1. Table 2: Results of 'Natural Language Inference (NLI)' experiments
- Natural Language Inference (NLI) experiments is to infer the logical relationship between two sentences.
- Finetuned Transformer LM is a GPT model.

### 2. Table 3: Results of 'Question answering and commonsense reasoning' experiments
- In question answering and commonsense reasoning, models would read English passages and solve following questions, just like middle or high school exams.
- Finetuned Transformer LM is a GPT model.

### 3. Table 4: Results of 'Semantic Similarity' and 'Classification' experiments
- Semantic Similarity: Determine that structurally different two sentences have the same meaning.
- Classification: Grammar checking and sentiment (positive or negative) analysis.
- Finetuned Transformer LM is a GPT model.

### 4. Figure 2: Analysis of GPT model
- **Left**: Effects of # of transferred layers from pre-training. The more layers are transferred, the better performance was achieved. This shows that pre-trained model learned useful functionality.
- **Right**: Zero-shot performance of GPT model. As pre-training performed, performance for specific tasks also increased.

### 5. Table 5: Ablation study results.

- Three things were targeted: Auxiliary objective, Transformer architecture, and Pre-training. All of them were important.
