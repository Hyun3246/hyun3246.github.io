---
title:  "[Deep Learning Basic Starting with TF] 5-2. Logistic Regression/Classification의 cost 함수, 최소화"
excerpt: "로지스틱 회귀의 비용함수"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 이항 분류, 로지스틱 회귀, 시그모이드 함수, 비용함수]

use_math: true
toc: true
toc_sticky: true

date: 2024-10-30
last_modified_at: 2024-10-30

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## 비용 함수
로지스틱 회귀에서 비용함수는 다음과 같이 정의한다.

$$cost(h_{\theta}, y) = -y \log{(h_{\theta}(x))} - (1 - y) \log{(1-h_{\theta}(x))}$$

식을 이해해보자.

먼저, 정답이 1인 경우(y=1)를 생각해보자. 비용함수의 식은 $-\log{(h_{\theta}(x))}$ 가 된다. 즉, 가설함수의 값이 1에 가까울 수록 함수의 결과 값이 0에 가까워진다. 반대로, y=0인 경우애는 비용함수가 $-\log{(1-h_{\theta}(x))}$ 이며, 가설함수의 값이 0에 가까울수록 비용이 줄어드는 형태가 된다. 
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/로지스틱 회귀 비용함수 그래프.png"
       style="width: 40%; height: auto; margin:10px">
  <figcaption style="text-align:center; font-size:14px; color:#808080">
    왼쪽이 y=1일 때, 오른쪽이 y=0일 때의 비용함수 그래프.
  </figcaption>
</figure>
<br/>

비용함수를 최소화하는 방법은 경사하강법을 사용하면 된다.

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*