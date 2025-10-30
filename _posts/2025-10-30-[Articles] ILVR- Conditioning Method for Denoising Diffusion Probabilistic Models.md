---
title: "[Articles] ILVR: Conditioning Method for Denoising Diffusion Probabilistic Models"
excerpt: " Devised ILVR, which can be used to guide a diffusion model to generate images based on the reference."
categories:
  - Data Science & ML
tags:
  - [Machine Learning, Deep Learning, Diffusion Models, DDPM, ILVR]
use_math: true
toc: true
toc_sticky: true
date: 2025-10-30
last_modified_at: 2025-10-30
header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---

## About this Article
- Authors: Jooyoung Choi, Sungwon Kim, Yonghyun Jeong, Youngjune Gwon, Sungroh Yoon
- Journal: ICCV 2021 (International Conference on Computer Vision)
- Year: 2021
- Official Citation: Choi, J., Kim, S., Jeong, Y., Gwon, Y., & Yoon, S. (2021). ILVR: Conditioning Method for Denoising Diffusion Probabilistic Models. In Proceedings of the IEEE/CVF International Conference on Computer Vision (ICCV) (pp. 14327-14336).

<br/>

## Accomplishments
- Devised ILVR, which can be used to guide a diffusion model to generate images based on the reference.

<br/>

## Key Points

### 1. Idea
As the stochasticity is added to the each step of the diffusion model (in this article, DDPM), it is hard to control the generating procedures.
To solve this problem, authors devised Iterative Latent Variable Refinement(ILVR), adding reference image information to each step.
By utilizing reference image, generated image can reflect users intention.
ILVR can also be used to already trained model, without further training.

### 2. Details
1. ILVR

    Our goal is to make an unconditional DDPM model generate images that shares high-level semantics from reference images.
    Therefore, the goal can be represented as a below.

    $$p_{\theta}(x_{0}|c)=\int p_{\theta}(x_{0:T}|c)dx_{1:T}$$

    $$p_{\theta}(x_{0;T}|c)=p(x_{T})\prod_{l=1}^{T}p_{\theta}(x_{l-1}|x_{l},c)$$

    - $p_{\theta}(x_{0}|c)$ Probability distribution of image $x_{0}$ is generated when condition c is given.
    - $p_{\theta}(x_{0:T}|c)$: Probability distribution of a specific route $x_{0}...x_{T}$ when condition c is given.
    - $p(x_{T})$ Probability of the starting point T. It is a fixed value because the probability distribution of noise is given (normal distribution).
    - $p_{\theta}(x_{t-1}|x_{r},c)$ Probability of each step.

    By integrating all possible routes, $p_{\theta}(x_{0}|c)$ can be obtained. $p_{\theta}(x_{0:T}|c)$ can be calculated by multiplying all steps.

    However, it is hard to get $p_{\theta}(x_{0}|c)$ directly. Therefore, authors used an approximation.

    $$p_{\theta}(x_{t-1}|x_{t},c)\approx p_{\theta}(x_{t-1}|x_{t},\phi_{N}(x_{t-1})=\phi_{N}(y_{t-1}))$$

    - $\phi_{N}(\cdot);$ A linear low-pass filtering operation. This can pass low-frequency components (basic outlines) and block high-frequency components (details).
    The process is same as a sequence of downsampling and upsampling by a factor N.
    - y: A reference image.
    - $x_{0}$ A generated image.
    The formula represents that conditioning for each step by condition c is similar to conditioning y and $x_{0}$ to have similar low-frequency contents.
    To implement this, authors suggested the formula below.

    $$x_{t-1}^{\prime}\sim p_{\theta}(x_{t-1}^{\prime}|x_{t})$$

    $$x_{t-1}=\phi(y_{t-1})+(I-\phi)(x_{t-1}^{\prime}).$$

    - $x_{t-1}^{\prime}$ The unconditional proposal distribution. In other words, original images that the unconditioned model was going to create.
    - $(I-\phi)(x_{t-1}^{\prime})$ Details of $x_{t-1}^{\prime}$ Original ${x_{t-1}}^{\prime}$ was subtracted by low frequency image $\phi(x_{t-1}^{\prime}).$
    The second one is the key point of this article.
    Basic structure of reference image and the details of $x_{t-1}^{\prime}$ was added (by a matrix), and this result is the input of the next step.
    This is why authors said that the information of reference image is being used.
    The full algorithm is as a below.

2) Reference Selection

    How do we select reference images? The process of generating images with ILVR is similar to the following image.

    The directed(reference) subset can be denoted as:

    $$R_{N}(y)=\{x:\phi_{N}(x)=\phi_{N}(y)\}$$

    and when the step (b to a) information is added:

    $$R_{N,(a,b)}(y)=\{x:\phi_{N}(x_{t})=\phi_{N}(y_{t}),t\in[b,a]\}$$

    There are three properties that users can utilize.

    (1) If the low-resolution space is the same, it can be used as a reference image.

    $$Y=\{y:\phi_{N}(y)=\phi_{N}(x),x\in\mu\}$$

    There is no additional checking point that the reference image has the same space. If the result image is good, the reference image is on the same space.

    (2) Larger downsampling factor N can decrease similarity to the reference image.

    $$R_{N}\subset R_{M}\subset\mu \text{, when }N\le M$$

    This is intuitive. If downsampling factor is large, the image will lose many information. This will make the generated image be far from the reference. Authors represent this as 'sampling from a larger(lower) subset'.

    (3) Limiting the range of conditioning steps will decrease similarity to the reference image.

    $$R_{N}\subset R_{N,(T,k)}\subset\mu$$
    
    This is also intuitive. If the number of conditioning steps are small, the image will have a low opportunity to be similar to the reference.
    Authors represent the second and third as 'sampling from a larger(lower) subset'.
