---
title:  "[Articles] ImageNet Classification with Deep Convolutional Neural Networks"
excerpt: "AlexNet, the starting point of CNN"

categories:
  - Data Science & ML
tags:
  - [Machine Learning, CNN, Architecture, AlexNet, ImageNet]

use_math: true
toc: true
toc_sticky: true

date: 2025-06-24
last_modified_at: 2025-06-24

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---
## About this Article
-   Authors: Alex Krizhevsky, Ilya Sutskever, Geoffrey E. Hinton 
-   Journal: Advances in Neural Information Processing Systems 
-   Year: 2012 
-   Citation: Krizhevsky, Alex, Ilya Sutskever, and Geoffrey E. Hinton. "Imagenet classification with deep convolutional neural networks.". Advances in neural information processing systems 25 (2012). 

<br/>

## Accomplishments
* Used a Convolutional Neural Network (CNN) to train an image classifier. 
* Devised a publicly available GPU implementation of 2D convolution. 

## Key Points

### 1. CNN Architecture (AlexNet)
The architecture consists of five convolutional layers and three fully-connected layers. 

| Layer | 1st | 2nd | 3rd | 4th | 5th | Fully-Connected Layer (3) |
|---|---|---|---|---|---|---|
| **Input Size** | $224\times224\times3$ | $27\times27$ | $13\times13$ | $13\times13$ | $13\times13$ | |
| **Kernel Size** | $11\times11\times3$ | $5\times5\times48$ | $3\times3\times256$ | $3\times3\times192$ | $3\times3\times192$ | |
| **Kernel Num** | 96 | 256 | 384 | 384 | 256 | 4096 neurons each |
| **Stride** | 4 | | | | | |
| **Connection** | | only same GPU | all maps of 2nd layer | only same GPU | only same GPU | all neurons in the previous layer|
| **LRN** | O | O | X | X | X | X |
| **Max Pooling**| O | O | X | X | O | X |
| **ReLU**| O | O | O | O | O | O |
| **Others** | - | - | - | - | - | Dropout is applied for the first two layers. <br/> Last layer is 1000-way softmax. |

<br/>

### 2. Key Features of the Architecture
(In order of importance as stated in the paper)

1.  ReLU Nonlinearity
    * Instead of sigmoid or tanh functions, the authors used ReLU ($f(x)=max(0,x)$). 
    * Enables faster training than tanh. 
    * It's unnecessary to have input normalization to prevent saturation, but AlexNet used LRN for better generalization. 

2.  Training on Multiple GPUs
    * The authors spread the network across two GPUs (GPU parallelization). 
    * The GPUs only communicate in certain layers to precisely tune the amount of communication. 
    * This reduces top-1 and top-5 error rates by 1.7% and 1.2%, respectively. 

3.  Local Response Normalization (LRN)
    * Used to normalize the output of ReLU neurons, as they can become too large. 
    * It creates competition among neighboring neurons, which improves generalization performance.
    * $$b_{x,y}^{i}=a_{x,y}^{i}/(k+\alpha\sum_{j=max(0,i-n/2)}^{min(N-1,i+n/2)}(a_{x,y}^{j})^{2})^{\beta}$$

4.  Overlapping Pooling
    * Unlike traditional non-overlapping pooling, the authors used overlapping pooling where the stride is less than the kernel size (s=2, z=3). 
    * This scheme helps to reduce overfitting slightly. 

### 3. Reducing Overfitting

1.  Data Augmentation
    * The authors used two forms of data augmentation. 
    * Generating image translations and horizontal reflections**: Random $224\times224$ patches and their reflections were extracted for training. For testing, five specific patches and their reflections were used. 
    * Altering the intensities of the RGB channels: Performed PCA on the RGB pixel values and added multiples of the principal components to each training image, making the model invariant to changes in illumination. 
    * $$[p_{1},p_{2},p_{3}][\alpha_{1}\lambda_{1},\alpha_{2}\lambda_{2},\alpha_{3}\lambda_{3}]^{T}$$ 

2.  Dropout
    * Reduces complex co-adaptations of neurons by setting the output of each hidden neuron to zero with a probability of 0.5. 

### 4. Results
*ILSVRC-2010: Achieved a top-1 error rate of 37.5% and a top-5 error rate of 17.0%, significantly outperforming the previous state-of-the-art (47.1% and 28.2%). 
* ILSVRC-2012: An ensemble of seven CNNs achieved a top-5 error rate of 15.3%, winning the competition. The previous best was 26.2%. 
* Fall 2009 Dataset: Achieved 67.4% (top-1) and 40.9% (top-5) error rates, compared to the previous best of 78.1% and 60.9%. 

### 5. Qualitative Evaluation
* The two GPUs specialized spontaneously: one learned color-agnostic features, while the other learned color-specific features. 
* The network successfully recognized off-center objects. 
* Images that were semantically similar but different at the pixel level were considered similar by the network's feature vectors. 

### 6. Limitations & Further Research
* Depth is crucial: removing any single convolutional layer resulted in a significant loss of performance. 
* The authors did not use unsupervised pre-training, suggesting there is still room for improvement. 
* The ultimate goal is to use very large and deep CNNs on video sequences. 

<br/>

## Full Article

[Visit here](https://proceedings.neurips.cc/paper/2012/hash/c399862d3b9d6b76c8436e924a68c45b-Abstract.html)