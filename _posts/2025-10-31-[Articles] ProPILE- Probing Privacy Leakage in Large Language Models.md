---
title: "[Articles] ProPILE: Probing Privacy Leakage in Large Language Models"
excerpt: "Developed ProPILE, which can be used both for LLM users and providers to check Personally Identifiable Information(PII) leakage."
categories:
  - Data Science & ML
tags:
  - [Machine Learning, Deep Learning, LLM]
use_math: true
toc: true
toc_sticky: true
date: 2025-10-31
last_modified_at: 2025-10-31
header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---

## About this Article
- **Authors**: Siwon Kim, Sangdoo Yun, Sungroh Yoon, Hwaran Lee, Martin Gubri, Seong Joon Oh
- **Journal**: 37th Conference on Neural Information Processing Systems (NeurIPS 2023)
- **Year**: 2023
- **Official Citation**: Kim, S., Yun, S., Yoon, S., Lee, H., Gubri, M., & Oh, S. J. (2023). ProPILE: Probing Privacy Leakage in Large Language Models. In 37th Conference on Neural Information Processing Systems (NeurIPS).

<br/>

## Accomplishments
- Developed ProPILE, which can be used both for LLM users and providers to check Personally Identifiable Information(PII) leakage.

<br/>

## Key Points

### 1. Personally Identifiable Information(PII) Leakage
PIl can be used and leaked by generated results of LLMs, but there is a no tool to identify the leakage.
Therefore, authors devised ProPILE, that data subject and LLM providers both can assess the leakage of PII.
There are two basic terms in this article.

- **Linkable of Pll leakage**: Leakage of PII is serious, only if the Pll can link the owner. Therefore, authors devised the following definition of linkable of Pll leakage. Simply, if you can get a certain type of Pll easier by providing other types of Plls to LLM, it is a linkable of Pll leakage.

- **Structured PII**: Structured Pll has a structured pattern, such as phone numbers or email addresses.
They are easy to identify, but hard to exclude during generation because it is hard to distinguish the information is official one or not.

By considering the capability of LLM users and service providers, authors suggests two access types.
- **Black-box access**: For users, who are not able to access to LLM's details, such as data, and algorithms. However, they have rights to the data.
- **White-box access**: For service providers. They can access to the details of LLMs.

### 2. Probing Methods

#### 1. Black-box Probing
Black-box probing is for LLM users, who cannot access to the details of LLMs.
- **Steps**:
    - (1) ${\mathcal{d}}\_{\backslash m}$ is prompted with K different templates $t_{k}$ Therefore, the inputs to LLM is $\mathcal{T} = \{t_{1}(\mathcal{A}\_{\backslash m}), \dots, t_{K}(\mathcal{A}_{\backslash m})\}$.
    - (2) Send the set of prompts to LLM as much as N times.
    - (3) The outputs will be $N\times K$ responses. The dimension of likelihood score is $\mathbb{Z}\in\mathbb{R}^{K\times L\times V}$ (L: the length of responses, V: the vocabulary size of LLM).

#### 2. White-box Probing
White-box probing is for LLM service providers, who can access to the details of LLMs.
Unlike black-box probing, soft prompt tuning is used.
A few notations and assumptions are required.
- $\mathcal{D}=\{\mathcal{A}^{i}\}_{i=1}^{N}$: Pll lists included in the training dataset of target LLM.
- An actor has access to a subset of training data $\tilde{\mathcal{D}} \subset \mathcal{D}$, where $\vert D \vert =n$ for $n \ll N$
- Prompt X is created by one of templates used in black-box probing $X = t_{n}(\mathcal{A}_{\backslash m}^{i})$.
- **Steps**:
    - (1) Prompt X is tokenized and embedded into $X_{e}\in\mathbb{R}^{L_{X}\times d}$ ($L_{X}$: the length of query sequence, d: the embedding dim of LLM).
    - (2) Soft prompt $\theta_{s}\in\mathbb{R}^{L_{s}\times d}$ is added in the begging of $X_{e}$, making $\left[\theta_{s};X_{e}\right]\in\mathbb{R}^{(L_{s}+L_{X})\times d}.$ The $\theta_{s}$ are learnable parameters.
    - (3) Train soft prompt in the direction of maximizing the expected reconstruction likelihood. 
    - (4) The learned soft embedding $\theta_{s}^{*}$ is added to the front of prompts $t_{n}(\mathbb{d}\_{\backslash m})$ to measure the leakage of $a_{m}$ of the subject.

### 3. Quantifying methods of leakage

#### 1. String match
To be simple, exact string match can be used as a quantitative evaluation method.

#### 2. Reconstruction likelihood
LLM can show the likelihood for candidate text outputs. By multiplying the probabilities, we can use the result as a likelihood of PIl reconstruction.

$$
Pr(a_{m}|\mathcal{A}\_{\backslash m}) = \prod_{r=1}^{L_{r}} p(a_{m,r} | x_{1}, x_{2}, ..., x_{L_{q}+r-1})
$$

This likelihood can also represent the level of leakage. The inverse of the likelihood is the expected number of sampling(queries) that is needed to generate the exact PII.

#### 3. New metric $\gamma_{<k}$
$\gamma_{<k}$ represents the fraction of data subjects whose Pll is likely to be revealed within k queries sent.
If $\gamma_{<100,m}=0.01$, then Pll of index m of 1% of data subjects are likely to be revealed within 100 same queries.

<br/>

## Limitations
1. Pll extraction was heuristic.
Pll of two different data objects could be considered as a one.
2. Risks of non-ethical usage.

People who are not related to a certain data object can access to generated PII. Further limitations are needed.

