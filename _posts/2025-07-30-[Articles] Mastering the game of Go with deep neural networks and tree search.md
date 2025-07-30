---
title: "[Articles] Mastering the game of Go with deep neural networks and tree search"
excerpt: "Introduced AlphaGo, which showed the power of Al to humanity."
categories:
  - Data Science & ML
tags:
  - [Machine Learning, Reinforcement Learning, MCTS, CNN, AlphaGo]
use_math: true
toc: true
toc_sticky: true
date: 2025-07-30
last_modified_at: 2025-07-30
header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay%20image/Research%20Paper.png
---

## About this Article
- **Authors**: David Silver, Aja Huang, Demis Hassabis, et al. (Google DeepMind)
- **Journal**: Nature
- **Year**: 2016
- **Official Citation**: Silver, D., Huang, A., Maddison, C. J., et al. Mastering the game of Go with deep neural networks and tree search. Nature 529, 484-489 (2016).

<br/>

## Accomplishments
- Introduced AlphaGo, which showed the power of Al to humanity.

<br/>

## Key Points

### 1. Monte Carlo tree search (MCTS)
Monte Carlo tree search(MCTS) uses Monte Carlo rollouts to estimate the value of each state in a search tree. The more the simulations are executed, the more accurate the values are.


### 2. Pipeline (Architecture)

#### 1. Supervised Learning(SL) policy network $(p_{\sigma})$ 
- **Purpose**: Predict the moves of Go experts.
- **Steps**:
  - (1) Prepare 13 layers of deep CNN and 30 millions of data.
  - (2) Train the network by assuming the input data as 19 by 19 image.
  - (3) Update parameters to maximize(gradient ascent) the probability $p_{\sigma}(a \vert s)$, where s is a given state, and a in an answer movement.
- **Achieved** prediction accuracy of 57.0%, which is the highest number of the time.

#### 2. Rollout policy $(p_{\pi})$
- **Purpose**: Fast simulation.
- Used linear softmax policy.
- Low accuracy than SL policy network, but faster.

#### 3. Reinforcement Learning(RL) policy network $(p_{\rho})$
- **Purpose**: Winning the game of Go.
- **Steps**:
  - (1) Copy the weights of SL policy network $p_{\sigma}$.
  - (2) Self play Go with one of the randomly chosen previous versions (to prevent overfitting).
  - (3) No reward until the game is over.
  - (4) If the game is over, weighs are updated as a following formula for each time step t.
    $\Delta\rho\propto\frac{\partial log~p_{\rho}(a_{t}|s_{t})}{\partial\rho}z_{t}$ where $z_{t}=1$ for winning, -1 for losing.
- A movement with low probability at time t, $log~p_{\rho}(a_{t} \vert s_{t})$, can have a high gradient because of log function. It's natural for the network to learn that suspicious moves have a high probability of winning.
- **Won** more than 80% of games against SL policy network.
- **Won** 85% against the most powerful open source Go program Pachi.

#### 4. Value network $(v_{\theta})$
- **Purpose**: Position evaluation(predicting the winning probability) based on a certain state s.
- **Steps**:
  - (1) Take the strongest policy, RL policy network $p_{\rho}$.
  - (2) Starting from the current state s, use $p_{\rho}$ to continue the game.
  - (3) Compute a single prediction between $win(+1)$ or $lose(-1)$ (not a probability distribution).
  - (4) Update the network by using MSE between actual results and predictions.
  - (5) To mitigate overfitting problem of memorizing the results, use self play results.
- **Achieved** powerful accuracy whose one evaluation is similar to thousands of rollout simulations.


### 3. Deciding the Best Move (MCTS Integration)
(To understand this mechanism, it is important to understand the four steps below in an integrated manner, not a step by step separately.)

#### 1. Selection
Starting from the root, traverse the tree by simulation. At each time step t, an action(route or edge) $a_{t}$ is selected from state s,

$$a_{t}=argmax_{a}(Q(s_{t},a)+u(s_{t},a))$$

- $Q(s,a)$: Action value, which shows the average odds (probability) of winning. It is initialized as 0 and updated in step 4.
- $u(s,a)$: A bonus, proportional to the prior probability $P(s,a)$ and decays with repeated (conventional) visits. $u(s,a)\propto\frac{P(s,a)}{1+N(s,a)}$

#### 2. Expansion
When reaches the leaf node of a tree, expand the tree (record possible next moves) by using SL policy $p_{\sigma}.$ SL policy is better than value network $v_{\theta}$ at this step because humans try to seek for as many possibilities at a certain stage.
Prior probability of new nodes are initialized by using the output of $p_{\sigma},$ $P(s,a)=p_{\sigma}(a|s)$.

#### 3. Evaluation
After expanding the tree, evaluate the each leaf node. For evaluation, two elements are used, the results from value network $v_{\theta}(s_{L})$ and random rollout $z_{L}$. Two of them are linearly combined by the ratio λ.

$$V(s_{L})=(1-\lambda)v_{\theta}(s_{L})+\lambda z_{L}$$

#### 4. Backup
At the end of the simulation, we will update the two things.
- Visit counts of all edges $N(s,a)=\sum_{i=1}^{n}1(s,a,i)$
- Action value of all edges $Q(s,a)=\frac{1}{N(s,a)}\sum_{i=1}^{n}1(s,a,i)V(s_{L}^{i})$

How do we select the best move? We choose the most visited edge from the root, not a highest action value.
Why the most visited? Because it decreases the impact of outliers, low visits with only one great scenario.
As mentioned above, the updated action value is used in step 1.


### 4. Experiments & Ablation Studies

- AlphaGo is stronger than any other existing program, even given a handicap.
- AlphaGo is better when distributed in multiple computers.
- AlphaGo is complete when rollout and value network are combined.

<br/>

## Impact of research
- Developed the first effective movement selection and evaluation function for Go. Based on deep NN.
- Introduced a new search algorithm that combines NN and MCTS.
- By combining the two, developed AlphaGo with high-performance tree search engine.
- (After research) AlphaGo defeated two of the best human Go players, Lee Sedol and Ke Jie.
- (After research) More improvements underwent, through
  - AlphaGo Zero (2017): Only trained with self play.
  - AlphaZero (2017): Not only Go, also applied to other games.
  - MuZero(2020): Trained even without the information of rules.
