---
title:  "[Articles] Deep Residual Learning for Image Recognition"
excerpt: "ResNet"

categories:
  - Data Science & ML
tags:
  - [Machine Learning, Deep Learning, Architecture, ResNet, Image Recognition]

use_math: true
toc: true
toc_sticky: true

date: 2025-06-26
last_modified_at: 2025-06-26

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Research Paper.png
---
## About this Article
- Authors: Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun
- Journals: 2016 IEEE Conference on Computer Vision and Pattern Recognition (CVPR)
- Year: 2016
- Citation: He, Kaiming, et al. "Deep residual learning for image recognition." Proceedings of the IEEE conference on computer vision and pattern recognition. 2016.

<br/>

## Accomplishments
Developed ResNet that can overcome a degradation problem of deep neural networks.

## Key Points
### 1. Degradation Problem of Deep Neural Networks
Deep Neural Networks have a degradation problem (error rate increases in training set), when the number of layers becomes too large.

### 2. The Solution: A Residual Building Block
Authors suggested ResNet as a solution of a degradation problem. The main characteristic of the building block is a shortcut with identity mapping, which adds input x to the output of stacked layers.

#### Residual Learning
Instead of approximating an underlying mapping $H(x)$, authors suggested to approximate the residual function $F(x) = H(x) - x$. The original function then becomes $H(x) = F(x) + x$. The motivation for this is that solvers might have difficulties in approximating identity mappings by multiple nonlinear layers. While an identical mapping is not optimal in reality, it can help to precondition the problem.

#### Identity Mapping by Shortcuts
Residual learning is adopted for every few stacked layers. The building block can be expressed by the formula:
$$ y = F(x, \{W_i\}) + x $$
Here, $F(x, \{W_i\})$ represents the residual mapping to be learned. For a block with two layers, $F = W_2\sigma(W_1x)$ is calculated using a ReLU activation function $\sigma$, and then $F+x$ is performed by a shortcut connection.

This simple shortcut connection has several advantages:
- It does not require extra parameters or computation complexity.
- It enables a fair comparison between plain and residual networks that have the same number of parameters, depth, width, and computational cost.

### 3. Network Architectures
#### Plain Network
The plain baselines are inspired by VGG nets, but contain fewer filters and have lower complexity.

#### Residual Network
Based on the plain network, authors inserted shortcut connections to form the residual network.

#### Deeper Bottle Neck Architecture
To create deeper networks without significantly increasing computation time, a "bottleneck" architecture was designed. This block uses a stack of three layers:
1.  A 1x1 convolution layer to reduce the dimension of the feature map.
2.  A 3x3 convolution layer that performs computation on the smaller dimension (the bottleneck).
3.  A 1x1 convolution layer to increase the dimension back to its original size.

### 4. Experimental Insights
- **Overcoming Degradation**: In experiments on ImageNet, plain networks showed the degradation problem (a 34-layer plain net had higher error than an 18-layer one). In contrast, ResNet did not show this problem; the 34-layer ResNet performed better than the 18-layer version.
- **Supporting the Hypothesis**: Authors analyzed the standard deviation of layer responses. ResNets were found to have smaller responses than their plain counterparts. This supports the hypothesis that the residual functions might be generally closer to zero, meaning the layers are learning small residual adjustments rather than entire, complicated transformations. This frees the network from high training demands and overcomes the degradation problem.

### 5. Limitations & Further Research
- **Overfitting**: It was observed that using too many layers (e.g., 1202) can lead to overfitting. This problem can be addressed by using strong regularization techniques like dropout.

<br/>

## Full Article

[Visit here](https://arxiv.org/abs/1512.03385)