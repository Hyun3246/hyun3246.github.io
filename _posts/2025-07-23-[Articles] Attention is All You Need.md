---
title:  "[Articles] Attention is All You Need"
excerpt: "The foundational paper for modern NLP models, replacing RNNs with a self-attention mechanism."

categories:
  - Data Science & ML
tags:
  - [Machine Learning, Architecture, Transformer, Attention]

use_math: true
toc: true
toc_sticky: true

date: 2025-07-23
last_modified_at: 2025-07-23

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---

## About this Article
- **Authors**: Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Łukasz Kaiser, Illia Polosukhin
- **Journal**: Advances in Neural Information Processing Systems (NIPS 2017)
- **Year**: 2017
- **Official Citation**: Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., ... & Polosukhin, I. (2017). Attention is all you need. In *Advances in neural information processing systems* (pp. 5998-6008).

<br/>

## Accomplishments
Ended the era of sequential models like RNNs by demonstrating that superior performance could be achieved with an attention-only architecture, setting a new standard for modern AI.

<br/>

## Key Points

### 1. Building Blocks
1. Scaled Dot-Product Attention
- **Purpose**: To generate a new vector which reflects the context information between words in a sentence.
- **Terms**:
    - **Query(Q)**: Information to find out. A word which is under processing.
    - **Key(K)**: Index or keyword of other words.
    - **Value(V)**: Ultimate actual information to figure out.
- **Formula**: 
    $Attention(Q,K,V)=softmax(\frac{QK^{T}}{\sqrt{d_{k}}})V$
- **Steps**: Find the appropriate key first, and use the information to figure out the appropriate value.
    1. Compute similarity of query(Q) and key(K) $(QK^{T})$.
    2. Divide by $\sqrt{d_{k}}$ to avoid the problem of small gradients.
    3. Apply softmax to get the final attention weights.
    4. Compute the final vector by multiplying the weights by value (V).

**2. Multi-Head Attention**
- **Purpose**: To perform scaled dot-product attention in parallel, allowing the model to jointly attend to information from different representation subspaces at different positions.
- **Formula**:
    $MultiHead(Q,K,V)=Concat(head_{1},...,head_{h})W^{O}$
    where $head_{i}=Attention(QW_{i}^{Q},KW_{i}^{K},VW_{i}^{V})$
- **Steps**:
    1. Divide Q, K, V into h fragments using different, learned linear projections.
    2. For each fragment, use different weight matrices in order to have different perspectives.
    3. Perform scaled dot-product attention independently and in parallel.
    4. Concatenate the results of all heads.
    5. Make a final vector by multiplying the concatenated result by another weight matrix.


### 2. Full Architecture

**1. Encoder (left)**
- Transforms a sentence into a representation (vector) that reflects the context and meaning.
- Composed of a stack of 6 identical layers.
- Each layer has two sub-layers: Multi-Head Attention and a simple Feed Forward Network.
- Employs residual connections around each of the two sub-layers, followed by layer normalization.

**2. Decoder (right)**
- Generates an output sentence based on the representation from the encoder.
- Composed of a stack of 6 identical layers.
- Each layer has three sub-layers: Masked Multi-Head Attention, Encoder-Decoder Attention, and a Feed Forward Network.
- The **Masked Multi-Head Attention** ensures that the predictions for a position can depend only on the known outputs at positions less than it.
- The **Encoder-Decoder Attention** is where the output of the encoder (K, V) and the output of the previous decoder layer (Q) meet.
- Employs residual connections and layer normalization.

**3. Positional Encoding**
- As the model contains no recurrence or convolution, positional encodings are added to give the model information about the relative or absolute position of the tokens in the sequence.
- Authors used sine and cosine functions of different frequencies.



### 3. Advantages of Self-Attention
Self-Attention was evaluated on three criteria compared to Recurrent and Convolutional layers:
- **Computational complexity per layer**: Self-Attention is faster than Recurrent layers when the sequence length `n` is smaller than the representation dimension `d`.
- **Sequential operations**: Self-Attention has an O(1) number of sequential operations, allowing for much more parallelization than the O(n) of Recurrent layers.
- **Maximum path length**: Self-Attention offers a constant O(1) path length between any two tokens, making it easier to learn long-range dependencies compared to the O(n) path length in Recurrent layers.

These advantages are why the Transformer is a predominant architecture, suitable for long sentences, massive GPU parallelization, and fast training. Additionally, self-attention allows for more interpretable models by inspecting attention distributions.

<br/>

## Possibility for Further Research
- **Apply to other types of data**: Authors anticipated applying the model to other types of data, such as images, audio, and video.
- **Making generation less sequential**: Investigating ways to make the auto-regressive generation process more parallel.