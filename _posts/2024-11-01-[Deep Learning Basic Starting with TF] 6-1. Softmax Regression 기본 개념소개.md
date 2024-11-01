---
title:  "[Deep Learning Basic Starting with TF] 6-1. Softmax Regression: 기본 개념소개"
excerpt: "이항 분류로 다항 분류하기"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 로지스틱 회귀, 이항 분류]

use_math: true
toc: true
toc_sticky: true

date: 2024-11-01
last_modified_at: 2024-11-01

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## 이항 분류와 다항 분류
이항 분류를 여러 번 하는 방식으로 다항 분류를 할 수 있다. 예를 들어, 다음과 같이 세 종류의 성적을 분류하는 과정을 생각할 수 있다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/이항 분류 여러 번으로 다항 분류 예시.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

그럼 다음과 같이 총 세 번의 계산 과정을 거쳐야 한다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/이항 분류 여러 번으로 다항 분류 계산 과정.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

하지만 계산을 세 번이나 하면 너무 복잡하기 때문에, 하나의 matirx로 합쳐서 계산하기로 한다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/이항 분류 여러 번으로 다항 분류 계산 과정 간소화.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

결과 vector의 각 요소들은 가설함수의 계산 결과가 될 것이다.

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*