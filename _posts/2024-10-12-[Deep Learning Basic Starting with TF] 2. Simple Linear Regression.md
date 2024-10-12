---
title:  "[Deep Learning Basic Starting with TF] 2. Simple Linear Regression"
excerpt: "선형 회귀와 비용함수"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 선형 회귀, 비용함수]

use_math: true
toc: true
toc_sticky: true

date: 2024-10-12
last_modified_at: 2024-10-12

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## 선형 회귀
선형 회귀(Linear Regression)는 데이터를 가장 잘 대변하는 직선을 찾는 것을 의미한다.

우리가 찾은 선형 회귀 식을 '가설(hypothesis)'이라고도 하며, 가설 중에서 가장 적절한 것을 선택하는 것이 우리의 목표라고 할 수 있다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/다양한 선형 회귀 가설 그래프.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

가장 적절한 것을 선택할 때는 비용함수를 이용한다. 비용함수는 가설과 실제 데이터의 차이를 의미한다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/비용 함수를 시각화한 그래프.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

좀 더 수학적으로는 <span style="color:#F5F5F7">'오차 제곱의 평균'</span>이다.

$$\displaystyle cost(W, b) = \frac{1}{m} \sum_{i=1}^{m}{(H(x_i) - y_i)^2}$$

우리의 목표는 <span style="color:#F5F5F7">비용함수를 최소화하는 W와 b를 찾는 것</span>이다.
