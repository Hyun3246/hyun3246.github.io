---
title:  "[Deep Learning Basic Starting with TF] 5-1. Logistic Regression/Classification 의 소개"
excerpt: "이항 분류와 로지스틱 회귀"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 이항 분류, 로지스틱 회귀, 시그모이드 함수]

use_math: true
toc: true
toc_sticky: true

date: 2024-10-30
last_modified_at: 2024-10-30

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## 이항 분류
이항 분류(Binary Classification)는 요소를 두 그룹 중 하나로 분류하는 것을 말한다. 예를 들어 합격, 불합격 판별, 스팸 메일 여부의 판별, 어떤 얼굴의 실제 여부의 판별 등이 있다. 머신러닝에서 이항 분류는 결과 값을 0 또는 1로 만들게 된다.

<br/>

## 로지스틱 회귀
선형 회귀에서는 연속적인 값으로 결과 값을 추측했지만, 이항 분류에서는 결과 값이 0, 1 둘 중 하나다. 따라서 이항 분류를 위해서는 새로운 함수가 필요한데, 로지스틱 함수가 그 역할을 할 수 있다. 로지스틱 함수는 <span style="color:#F5F5F7">예측의 결과 값을 0과 1사이의 값으로 바꾸어주는 역할</span>을 한다.

로지스틱 함수에 의해 값이 0과 1사이로 제한되었다면 이제 특정한 기준(e.g. 0.5)을 정해서 요소가 0에 속하는지 1에 속하는지를 판단하면 된다.

대략적인 로지스틱 회귀의 과정은 다음과 같다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/로지스틱 회귀의 대략적인 과정.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

가장 많이 사용하는 로지스틱 함수는 다음과 같은 시그모이드 함수(sigmoid function)이다.

$$g(z) = \frac{e^z}{(e^z + 1)} = \frac{1}{(1 + e^{-z})}$$


<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*