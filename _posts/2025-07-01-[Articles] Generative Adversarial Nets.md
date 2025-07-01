---
title:  "[Articles] Generative Adversarial Nets"
excerpt: "GAN"

categories:
  - Data Science & ML
tags:
  - [Machine Learning, Deep Learning, Architecture, GAN, Generative AI]

use_math: true
toc: true
toc_sticky: true

date: 2025-07-01
last_modified_at: 2025-07-01

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Research Paper.png
---
## About this Article
- Authors: Ian J. Goodfellow, Jean Pouget-Abadie, Mehdi Mirza, Bing Xu, David Warde-Farley, Sherjil Ozair, Aaron Courville, Yoshua Bengio
- Journals: arXiv (later, Advances in neural information processing systems)
- Year: 2014
- Citation: Goodfellow, Ian J., et al. "Generative adversarial nets." Advances in neural information processing systems 27 (2014).

<br/>

## Accomplishments
- Developed Generative Adversarial Nets (GAN), an architecture for generating data.

<br/>

## Key Points

### 1. Idea
The basic idea of GAN is to compete two distinct models(networks), one is a Generator(G) and the other is a Discriminator(D). The purpose of two networks are as follows.
- **G**: Make data which is difficult to discriminate from the real data.
- **D**: Distinguish whether given data is fake or real.

G and D will progressively compete like a police(D) and a fraud(G). The final goal is to make G perfect that D prints 1/2 for any input data.

### 2. Value Function

**1. Basic Notations**
- $p_g$: generator's distribution.
- $G(z)$: data produced by generator G from noise z.
- $D(x)$: the probability that data x came from the data rather than $p_g$. (In other words, from actual data.)
- $D(G(z)))$: the probability that D determines fake data $G(z)$ as an actual data.
- $(1-D(G(z)))$: the probability that D determines a fake data as a fake data.

**2. Basic sketch**
We train D and G:
- D to maximize the probability of assigning correct label to both training examples and samples from G.
- G to minimize $log(1-D(G(z)))$.

**3. Value function**
The value(objective) function $V(D,G)$ is
$$ \min_{G} \max_{D} V(D,G) = \mathbb{E}_{x \sim p_{\text{data}}(x)}[\log D(x)] + \mathbb{E}_{z \sim p_{z}(z)}[\log(1-D(G(z)))] $$

**4. In the viewpoint of D**
D should discriminate real data as real data. Therefore, D has to maximize the probability $D(x)$ close to 1.

**5. In the viewpoint of G**
The goal of G is to cheat D. Therefore, G has to minimize $log(1-D(G(z)))$.

**6. In early training**
In early training, $log(1-D(G(z)))$ saturates (vanishing gradient). To solve this problem, authors used maximizing $log(D(G(z)))$ instead.

### 3. Algorithm
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/Warehouse@master/Papers/GAN algorithm.png"
       style="width: 80%; height: auto; margin:10px">
</figure>
<br/>
Authors alternatively trained D (k steps) and G (1 step).
1.  **Training D**: Extract m noise data and m real data. Update D by using a gradient of value function. Add (ascending) the gradient because the purpose of D is maximization.
2.  **Training G**: Extract m noise data. Update G by using a gradient of value function. Subtract (descending) the gradient because the purpose of G is minimization.

### 4. Theoretical Guarantees
There are two mathematical theorems that guarantee the validity of GAN.
- **Global Optimality of $p_g = p_{\text{data}}$**: This shows that GAN works as we intended. Authors also suggest that the global optimum of value function is $-log~4$.
- **Convergence of Algorithm**: This shows that GAN training algorithm works.

### 5. Advantages and Disadvantages

**1. Advantages**
- Markov chains are never needed, only backprop is needed.
- No inference is needed.
- A wide variety of functions can be incorporated into the model.
- Components of inputs are not copied directly into the generator's parameters.

**2. Disadvantages**
- No explicit representation of $p_g(x)$.
- Training speed of G and D should be well-synchronized.
- The Helvetica scenario: Mode collapse can happen. If G is trained too much without updating D, G can find and make only one perfect sample that can deceive D, for any input noise distribution z.

<br/>

## Further Research
1.  **Conditional Generative Model**: By conditioning input, we can control a model to generate certain types of data. (This idea leads to cGAN.)
2.  **Learned Approximate Inference**: GAN in this article learned 'input noise z -> output x' direction. We can introduce another auxiliary network to infer the reverse direction, from output to input noise. (This idea leads to BiGAN, ALI.)
3.  **Modeling Conditionals**: By training conditional models that share the same parameters, we can make a model to predict the rest part of data when only part of it is given. (Think image refining tools, 'AI eraser' of Galaxy or 'Clean up' of iOS.)
4.  **Semi-supervised Learning**: If labeled data is limited, features from the discriminator D can be used to improve performance of classifiers.
5.  **Efficiency improvements**: Training can be accelerated by devising better methods for coordinating G and D. It can also be improved by a better noise distribution z.

<br/>

## Full Article

[Visit here](https://arxiv.org/abs/1406.2661)