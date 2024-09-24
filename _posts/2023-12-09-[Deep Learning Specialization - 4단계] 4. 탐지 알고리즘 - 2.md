---
title:  "[Deep Learning Specialization - 4단계] 4. 탐지 알고리즘 - 2"
excerpt: "IOU, 비최대억제, 앵커 상자. 이를 합한 YOLO 알고리즘"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 신경망, 합성곱, 컴퓨터 비전]

use_math: true
toc: true
toc_sticky: true
 
date: 2023-12-09
last_modified_at: 2023-12-09

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/andrew ng 4.jpg
---
## 합집합 위의 교집합 (IOU)
물체 인식이 제대로 되었는지는 <span style="color:#F5F5F7">'합집합 위의 교집합(Intersection Over Union, IOU)'</span>으로 판단한다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/IOU의 이해.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

위 그림에서 녹색 영역은 정답과 예측 영역을 합한 것(합집합)이고, 노란색은 정답과 예측이 겹치는 부분(교집합)이다. IOU는 다음과 같이 정의한다.

Intersection Over Union = $ \frac{size \, of \, \cap}{size \, of \, \cup} $


보통 IOU가 0.5일 때를 기준으로, 0.5를 넘으면 어느 정도 옳게 판단한 것으로 본다.

IOU는 두 경계 상자에서 겹치는 부분의 비율을 의미하기도 한다.

<br/>

## 비최대억제
비최대억제는 한 가지 물체에 대해 여러 개의 경계 상자가 그려졌을 때, 가장 적합한 것을 선택하는 알고리즘이다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/비최대억제 알고리즘 이해.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

위 그림처럼 하나의 물체에 대해 다양한 경계 상자가 그려질 수 있으며, 각각은 감지 확률을 가지고 있다. 비최대억제 알고리즘은 다음과 같은 순서로 진행된다.

1. 감지 확률 구하기
2. 감지 확률이 0.6 이하인 상자 삭제
3. 상자가 남아있는 동안(`while`), (1) <u>가장 큰 확률을 가지는 상자 선택</u>, (2) <u>그 상자와의 IOU가 0.5 이상인 상자 삭제</u>

<br/>

## 앵커 상자
하나의 격자 안에 두 가지 물체의 중심점이 있는 경우에는 어떻게 할까? <span style="color:#F5F5F7">앵커상자</span>를 이용하면 된다.

경계 상자를 사용하는 대신 미리 정해진 앵커 상자를 여러 개 사용하는 방식이다. 예를 들어, 보행자와 자동차를 동시에 예측하고 싶다면 미리 아래와 같은 앵커 상자를 정해 놓는다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/보행자, 자동차 앵커 상자.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

아래 그림에서 적용해보자.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/앵커 상자 적용 예시.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

앵커 상자를 사용하면 각각의 물체들은 중심점이 존재하는 동시에 앵커 상자와 가장 높은 IOU를 가지는 격자에 할당된다. 위 그림에서는 가운데 가장 아래 격자에 보행자와 자동차가 동시에 있다. 이 격자의 벡터를 표현하면 다음과 같다.

$$y = \begin{bmatrix} p_c\\ b_x \\ b_y \\ b_h \\ b_w \\ c_1 \\ c_2 \\ c_3 \\ p_c\\ b_x \\ b_y \\ b_h \\ b_w \\ c_1 \\ c_2 \\ c_3\end{bmatrix} = \begin{bmatrix} 1\\ b_x \\ b_y \\ b_h \\ b_w \\ 1 \\ 0 \\ 0 \\ 1\\ b_x \\ b_y \\ b_h \\ b_w \\ 0 \\ 1 \\ 0\end{bmatrix}$$

위쪽은 앵커 상자1(보행자)에 관한 요소들이고, 아래쪽은 상자2(자동차)에 관한 것이다. 이처럼 앵커 상자를 사용하면 벡터의 차원이 늘어나게 된다.

<br/>

## YOLO 알고리즘
앞서 살펴본 내용을 모두 합한 것이 <span style="color:#F5F5F7">'YOLO 알고리즘'</span>이다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/YOLO 알고리즘 이해.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

YOLO 알고리즘은 다음과 같이 실행된다.
1. 앵커 상자를 이용하면 각각의 격자에 대해 2개의 경계 상자가 만들어진다.
2. 이들 중에서 낮을 확률을 가진 것들을 제거.
3.  각 클래스(보행자, 자동차, 오토바이 등)에 대해 비최대억제 적용.

이 과정을 통해 예측값을 도출할 수 있다.

<br/>

## 지역 제안 알고리즘
<span style="color:#F5F5F7">지역 제안 알고리즘(Region Proposal)</span>은 합성곱 분류기를 실행할 지역을 미리 고른 뒤, 그 지역에 대해서만 경계 상자를 만드는 것을 의미한다.

슬라이딩 윈도우를 적용하는 과정에서 우리는 굳이 합성곱 분류기를 적용할 필요가 없는 부분까지 학습하느라 많은 시간을 소모했다. 지역 제안 알고리즘에서는 분류 알고리즘으로 미리 불필요한 지역을 삭제(이를 '지역 제안'이라고 함)하여 속도를 향상시킨다.

<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/지역 제안 알고리즘 지역 분류 예시.png"
       style="width: 40%; height: auto; margin:10px">
  <figcaption style="text-align:center; font-size:14px; color:#808080">
    지역 분류를 실행한 사진의 모습. 하늘색이나 파란색 부분과 같이 물체가 있을 것으로 예상되는 지역만 합성곱 분류기를 적용한다.
  </figcaption>
</figure>
<br/>

그러나 지역 제안 알고리즘을 적용한 합성곱(R-CNN)은 여전히 느리다. 이를 개선하기 위해 Fast R-CNN이 개발되었다. R-CNN 알고리즘에서 합성곱 슬라이딩 윈도 구현을 더한 것인데, 분류 속도는 빨라졌으나 지역 제안을 하기 위한 단계가 여전히 느리다.

다음으로 등장한 Faster R-CNN은 지역 제안 과정에서 합성곱 신경망을 사용하여 더 속도를 향상시켰다.

<span style="color:#F5F5F7">그러나 Faster R-CNN마저 YOLO 알고리즘에 비해서는 느리다...</span>

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*