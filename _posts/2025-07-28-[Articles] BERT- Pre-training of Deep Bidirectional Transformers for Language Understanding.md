---
title: "[Articles] BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding"
excerpt: "Introducint BERT, bidirectional pre=training with Transformer"
categories:
  - Data Science & ML
tags:
  - [Machine Learning, Architecture, NLP, Transformer, BERT, Bidirectional]
use_math: true
toc: true
toc_sticky: true
date: 2025-07-28
last_modified_at: 2025-07-28
header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---

## About this Article
- **Authors**: Jacob Devlin, Ming-Wei Chang, Kenton Lee, Kristina Toutanova
- **Journal**: NAACL-HLT (Proceedings of the 2019 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies)
- **Year**: 2019
- **Official Citation**: Devlin, J., Chang, M. W., Lee, K., & Toutanova, K. (2019). BERT: Pre-training of deep bidirectional transformers for language understanding. NAACL-HLT 2019.

<br/>

## Accomplishments
- Achieved true deep bidirectionality by introducing novel pre-training objectives: the Masked Language Model (MLM) and Next Sentence Prediction (NSP).

<br/>

## Key Points

### 1. Why Bidirectional?
Models like GPT (2018) or Transformer (2017) are all unidirectional models. A unidirectional model limits the choice of architectures and restricts the power of the pre-trained representations. This is the reason why authors devised BERT (Bidirectional Encoder Representations from Transformers).

---

### 2. Architecture

#### 1. Frameworks Overview
The framework consists of two parts: pre-training and fine-tuning.
- **Pre-training**: Trained on unlabeled data over different tasks.
- **Fine-Tuning**: First initialized with the pre-trained parameters, and fine-tuned with downstream tasks.

#### 2. Input and Output
Input representations are the sum of three embeddings:
- **Token Embeddings**: A token (word) is transformed into a unique vector.
- **Segment Embeddings**: BERT can get input with two sentences (Q & A, or inferring the relationship between two sentences). Segment embedding shows in which sentence the word is included.
- **Position Embedding**: Shows the position of each token.

Special tokens `[CLS]` and `[SEP]` are also added.
- **[CLS]**: Added in the beginning of a sentence. It represents the meaning of the entire sentence.
- **[SEP]**: Added between the two sentences.

By using the output, two types of analysis are possible:
- **Classification** (e.g., Positive or Negative, Sentence Relationship): Simply use the output vector C of the `[CLS]` token, which contains the meaning of the entire sentence.
- **Token-level tasks** (e.g., Q & A): Use the output vector of the entire tokens.

#### 3. Pre-training Framework
In pre-training, authors used two tasks:
- **Masked LM**: To prevent the 'see itself' (cheating answer tokens) problem of a bidirectional model, authors randomly masked 15% of tokens into `[masked]` (80%), random other words (10%), and itself (10%).
- **Next Sentence Prediction (NSP)**: The key point of Q & A and inference is to figure out the relationship between two sentences. To do this, authors simply conducted binary NSP tasks using `[CLS]` tokens.

#### 4. Fine-Tuning Framework
Fine-tuning is more simple (and inexpensive). Just plug in (add) input and output layers which are appropriate to downstream tasks.

---

### 3. Implementations

#### 1. General Language Understanding Evaluation (GLUE)
Introduced new weight parameters W during fine-tuning and used loss: $log(softmax(CW^{T}))$.

#### 2. Standard Question Answering Dataset (SQUAD 1.1)
Introduced two vectors S (start) and E (end) during fine-tuning. The probability of word i being the start of the answer span is computed as a dot product (similarity) between $T_{i}$ (contextual meaning of word i) and S (trained parameters containing characteristics of the answer word), $P_{i}=\frac{e^{S\cdot T_{i}}}{\sum_{j}e^{S\cdot T_{j}}}$. To determine the answer sentence, use the maximum score from position i to j, $S\cdot T_{i}+E\cdot T_{j}$.

#### 3. Standard Question Answering Dataset (SQUAD 2.0)
SQUAD 2.0 contains 'no answer' cases. To deal with this, 'no answer' cases are processed as `[CLS]` tokens only. To consider the no answer cases, authors used an additional scoring $s_{null}=S\cdot C+E\cdot C$ and compared it to the scoring method $(\hat{s}_{i,j})$ of SQUAD 1.1.

#### 4. Situations With Adversarial Generations (SWAG)
SWAG tasks is to choose the best following sentence (among four) when one sentence is given. To do this, authors made four sets of (A, B) pairs and used the output vector C of the `[CLS]` token. To transform the vector into a scalar value, authors introduced a new vector only for this task. After the dot product with C, applied softmax to compute the final score.

---

### 4. Ablation Studies

- **Effect of Pre-training (Bidirectional) Tasks**: BERT is better than No NSP and LTR (Left To Right).
- **Effect of Model Size**: Larger models are better than smaller models, not only for the large tasks (e.g. machine translation) but also for the small tasks.
- **Feature-based Approach with BERT**: BERT can be used as a feature extractor without fine-tuning.
    1. Train BERT without fine-tuning.
    2. Extract the activations (outputs) from BERT layers without modification.
    3. Use the activations as inputs for another layer (in the article, BiLSTM).
    
BERT is also an effective feature extractor.

<br/>

## Impact of research
- Introduced deep bidirectional architectures.