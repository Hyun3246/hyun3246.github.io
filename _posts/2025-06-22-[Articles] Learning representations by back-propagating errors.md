---
title:  "[Articles] Learning representations by back-propagating errors"
excerpt: "Backpropagation"

categories:
  - Data Science & ML
tags:
  - [Machine Learning, Architecture, Backpropagation]

use_math: true
toc: true
toc_sticky: true

date: 2025-06-22
last_modified_at: 2025-06-22

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Research Paper.png
---
## About this Article
- Authors: David E. Rumelhart, Geoffrey E. Hinton & Ronald J. Williams 
- Journals: Nature
- Year: 1986
- Citation: Rumelhart, D., Hinton, G. & Williams, R. Learning representations by back-propagating errors. Nature 323, 533–536 (1986).

<br/>


## Accomplishments
Introducing backpropagation, simple and powerful method to train neural network.

## Key Points
1. Forward Pass
    - total input: $x_j = \sum_{i}{y_iw_{ji}}$
    - output $y_j = \frac{1}{1+e^{-x_j}}$ (use non linear function)

2. Backpropagation
    1) Define Error <br/>
        $y$: actual state, $d$: desired state

        $E = \frac{1}{2}\sum_{c} \sum_{j}{(y_{j, c} - d_{j, c})^2}$ (c is an index over cases, j is an index over output units)
    2) Compute derivatives

        Our goal is to compute $\frac{\partial E}{\partial w_{ji}}$, which shows 'how much should we change the parameters to get a good fit?'

        First, from error equation, we can simply compute $\frac{\partial E}{\partial y_j}$.

        $$\frac{\partial E}{\partial y_j} = y_j - d_j$$

        Then, apply chain rule to compute $\frac{\partial E}{\partial x_j}$. To compute $\frac{dy_j}{dx_j}$, use the non linear function formula of forward pass.

        $$\frac{\partial E}{\partial x_j} = \frac{\partial E}{\partial y_j} \cdot \frac{dy_j}{dx_j} = \frac{\partial E}{\partial y_j} \cdot y_j(1 - y_j)$$

        By using the terms above, we can compute $\frac{\partial E}{\partial w_{ji}}$. You can get the term $\frac{\partial x_j}{\partial w_{ji}}$ from the first formula of forward pass.

        $$\frac{\partial E}{\partial w_{ji}} = \frac{\partial E}{\partial x_j} \cdot \frac{\partial x_j}{\partial w_{ji}} = \frac{\partial E}{\partial x_j} \cdot y_i$$

        Calculation for one layer is finished. You have to repeat the above process to calculate derivatives of all layers. To make an information for the previous layer, use the following formula.

        $$\frac{\partial E}{\partial y_i} = \sum_j \frac{\partial E}{\partial x_j} w_{ji}$$

        And the same process continues until reaching the first layer.

    3) Update Parameters

        Authors suggested two ways to update parameters. ($\epsilon$: learning rate)

        a) Simple Version
        Does not converge rapidly than using second derivatives.

        $$\Delta w = - \epsilon \frac{\partial E}{\partial w}$$

        b) Improved Version (Momentum)
        By using an acceleration method in which the current gradient is used to modify the velocity of the point in weight space instead of its position ($t$ is a step size). In other words, the following formula considers not only the current position, but also the rate of previous step ($\Delta w(t-1)$). Therefore, the gradient descent step can follow the steepest direction more reliably.

        $$\Delta w(t) = - \epsilon \frac{\partial E}{\partial w(t)} + \alpha \Delta w(t-1)$$


<br/>

## Full Article

[Visit here](https://www.nature.com/articles/323533a0)