---
title: "[Articles] Learning Transferable Visual Models From Natural Language Supervision"
excerpt: "CLIP, which learns transferable visual models from natural language supervision, enabling powerful zero-shot capabilities."
categories:
  - Data Science & ML
tags:
  - [Machine Learning, Computer Vision, Zero-Shot Learning, CLIP, Multimodal]
use_math: true
toc: true
toc_sticky: true
date: 2025-08-06
last_modified_at: 2025-08-06
header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---

## About this Article
- **Authors**: Alec Radford, Jong Wook Kim, Chris Hallacy, et al.
- **Journal**: Proceedings of the 38th International Conference on Machine Learning (ICML).
- **Year**: 2021
- **Official Citation**: Radford, A., Kim, J. W., Hallacy, C., Ramesh, A., Goh, G., Agarwal, S., ... & Sutskever, I. (2021). Learning transferable visual models from natural language supervision. In International conference on machine learning (pp. 8748-8763). PMLR.

<br/>

## Accomplishments
- Developed CLIP, enabling natural language supervision and zero-shot transfer in computer vision.

<br/>

## Key Points

### 1. Natural Language Supervision and Zero-Shot Transfer
CLIP start from several question, 'Wouldn't it be great if you didn't have to decide which categories to train computer vision models?' and 'Wouldn't it be great if you could use captions of images without labeling?'
- **Natural Language Supervision**: To use captions of images for training computer vision models without additional modifications.
- **Zero-Shot Transfer**: To predict a class of image, whose class is not appeared even once during training.

### 2. Contrastive Language-Image Pre-training (CLIP)

#### 1. Objective
It is computationally inefficient to make a model to predict the exact captions of images. Therefore, authors decided to change the problem into multiple-choice questions. From N pairs of (image, text), N^2 questions can be made. What the model do is to choose the most appropriate text to a image.

#### 2. Architecture of pre-training (Figure 1-1)
(1) Input text to text encoder(Transformer), image to image encoder(ResNet-50 or Vision Transformer).
(2) Make the outputs of step 1 to be in the same space of multi-modal embeddings.
(3) Train image and text encoder to maximize the cosine similarity of N real pairs, and minimize the similarity of the rest N^2 - N pairs.
Models are scaled by depth and width to strengthen the performance.

#### 3. Steps of creating dataset classifier and doing zero-shot prediction (Figure 1-2, 3)
(1) Make the list of classes (e.g. dogs, cats) to classify.
(2) Put the names of classes into a sentence template (e.g. A photo of a {class}.) to decrease the gap between 'one word caption' and 'a sentence caption'.
(3) Put the sentences into the trained text encoder and make embeddings.
(4) Prepare new images to classify and put them into the trained image encoder. Embeddings of images will be made.
(5) Compute similarity between embeddings of text and images and choose the closest pair.

<br/>

## Limitations of CLIP

1.  The performance of zero-shot CLIP is just an average, well below the overall SOTA.
    -   Solution: Increase the size of model. But this is infeasible in terms of computational efficiency.
2.  Zero-shot CLIP is weak on several kinds of tasks.
    -   Tasks such as fine-grained classification, abstract and systematic ones, and not included in pre-training dataset.
3.  Poor generalization of zero-shot CLIP on different distribution.
4.  CLIP is trained to 'choose' the best one(caption), not 'make' the best one.
    -   Solution 1: Joint training of a contrastive and generative objective.
    -   Solution 2: Perform searching at inference time over many natural language explanations of a given image.
5.  Poor data efficiency of CLIP.
    -   Solution: Combine CLIP with self-supervision and self-training.
6.  Repeatedly queried performance on val set, which is not a real-life zero-shot.
7.  Selection of evaluation datasets.
    -   Solution: Create a new benchmark of tasks to evaluate board zero-shot capabilities.
8.  Social bias of image-text pairs on online. Authors discussed this topic in Section 7.
9.  Few-shot decreases the performance of CLIP.
    -   The most significant difference between CLIP and human.