---
title: "[Articles] Denoising Diffusion Probabilistic Models"
excerpt: "Diffusion Model"
categories:
- Data Science & ML
tags:
- [Machine Learning, Deep Learning, Generative AI, Diffusion Model]

use_math: true
toc: true
toc_sticky: true

date: 2025-07-07
last_modified_at: 2025-07-07

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---

## About this Article
- Authors: Jonathan Ho, Ajay Jain, Pieter Abbeel
- Journal: Advances in Neural Information Processing Systems (NeurIPS) 33
- Year: 2020
- Official Citation: Ho, J., Jain, A., & Abbeel, P. (2020). Denoising diffusion probabilistic models. In Advances in Neural Information Processing Systems (Vol. 33, pp. 6840-6851).

<br/>

## Accomplishments
- Developed Diffusion model, which is widely used in image generation.

## Key Points
### 1. Idea
Diffusion model consists of two steps.
- **Forward process (or diffusion process):** Gradually add Gaussian noise to data (image). Doing so may corrupt the original data.
- **Reverse process:** Recover noised data to original data.
- The goal of training is to minimize the gap between the forward and reverse process in the same step.

### 2. Detailed Equations
#### 1. Forward Process
$q(x_{1:T}|x_{0}) := \prod_{t=1}^{T}q(x_{t}|x_{t-1}), \quad q(x_{t}|x_{t-1}) := \mathcal{N}(x_{t};\sqrt{1-\beta_{t}}x_{t-1},\beta_{t}I)$
- $q(x_{1:T}\vert x_{0})$ : the probability of a total scenario that one image is damaged.
- $q(x_{t}\vert x_{t-1})$: One step of forward process.

#### 2. Reverse Process
$p_{\theta}(x_{0:T}) := p(x_{T})\prod_{t=1}^{T}p_{\theta}(x_{t-1}|x_{t}), \quad p_{\theta}(x_{t-1}|x_{t}) := \mathcal{N}(x_{t-1};\mu_{\theta}(x_{t},t),\Sigma_{\theta}(x_{t},t))$
- $p_{\theta}(x_{0:T})$: the probability of a total scenario that one noisy image is recovered.
- $p_{\theta}(x_{t-1} \vert x_{t})$: the prediction of mean and variance of step by using the data of current step.

#### 3. Loss Function
$$
\mathbb{E}\left[-\log p_{\theta}(x_{0})\right] \le E_{q}\left[-\log\frac{p_{\theta}(x_{0:T})}{q(x_{1:T}|x_{0})}\right] = \mathbb{E}_{q}\left[-\log p(x_{T}) - \sum_{t \ge 1}\log\frac{p_{\theta}(x_{t-1}|x_{t})}{q(x_{t}|x_{t-1})}\right] =:L
$$

Although the equation is complex, the purpose is clear. It is to minimize the difference between the forward process $q(x_{t}|x_{t-1})$ and reverse process $p_{\theta}(x_{t-1}|x_{t})$. However, the authors used an improved version of equation (3) for computational convenience.

$$
E_{q}\left[ \underbrace{D_{KL}(q(x_T|x_0) || p(x_T))}_{L_T} + \sum_{t>1} \underbrace{D_{KL}(q(x_{t-1}|x_t, x_0) || p_{\theta}(x_{t-1}|x_t))}_{L_{t-1}} - \underbrace{\log p_{\theta}(x_0|x_1)}_{L_0} \right]
$$

- $L_T$: a constant. the difference between the last noise and the original noise.
- $L_{t-1}$: the core of training, sum of prediction(p) and answer(q) for all steps.
- $L_0$: recovery performance of the last step.

### 3. Reverse Process and L_{1:T-1}
What should the reverse process predict? Authors let $\Sigma_{\theta}$ in equation (1) as a constant. Therefore, a parameter that the model should predict is $\mu_{\theta}$ (mean). Through several loss function analysis and reparameterizing, authors figured out that mean $\mu_{\theta}$ can be represented as a following equation. The equation (11) shows that the only thing the model should predict is $\epsilon$ (a random noise vector from Gaussian distribution), because $x_t$ is given.

$$
\mu_{\theta}(x_{t},t) = \frac{1}{\sqrt{\alpha_{t}}}\left(x_{t} - \frac{\beta_{t}}{\sqrt{1-\overline{\alpha}\_{t}}} \epsilon_{\theta}(x_{t},t)\right)
$$

By further simplification, loss function can be represented as a follow.

$$
\mathbb{E}_{x_{0},\epsilon}\left[\frac{\beta_{t}^{2}}{2\sigma_{t}^{2}\alpha_{t}(1-\overline{\alpha}\_{t})} \left\| \epsilon - \epsilon_{\theta}(\sqrt{\overline{\alpha}\_{t}}x_{0}+\sqrt{1-\overline{\alpha}_{t}}\epsilon,t) \right\|^{2}\right]
$$

What reverse process should predict is, therefore, a noise $\epsilon$.

### 4. Simplified Training Objective
In equation (12), you can see the complex weight $\frac{\beta_{t}^{2}}{2\sigma_{t}^{2}\alpha_{t}(1-\overline{\alpha}\_{t})}$. When t grows, $(1-\overline{\alpha}_{t})$ grows. This can make the weight small when t is large, which is not efficient to focus much harder problem(more noisy image). Therefore, authors removed the weight and simplified the loss function.

$$
L_{simple}(\theta) := E_{t,x_{0},\epsilon}[\|\epsilon-\epsilon_{\theta}(\sqrt{\overline{\alpha}\_{t}}x_{0}+\sqrt{1-\overline{\alpha}_{t}}\epsilon,t)\|^{2}]
$$

This can make the model to focus on harder problems with much of noise (when t is large).

<br/>

## Impact of research
1. **Positive:** Useful for data compression. High resolution data can be more easily accessible even through increased global internet traffic.
2. **Negative:** Production of fake images and videos.
3. **Negative:** Reflection of bias in datasets.
