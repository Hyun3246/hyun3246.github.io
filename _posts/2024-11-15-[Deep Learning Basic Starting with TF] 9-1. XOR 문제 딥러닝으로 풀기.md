---
title:  "[Deep Learning Basic Starting with TF] 9-1. XOR 문제 딥러닝으로 풀기"
excerpt: "XOR 문제의 해결 방법"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 텐서플로]

use_math: true
toc: true
toc_sticky: true

date: 2024-11-15
last_modified_at: 2024-11-15

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## XOR 문제를 신경망으로 풀기
XOR 문제의 정의는 다음과 같다.

|x1|x2|XOR|
|:--:|:--:|:--:|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/XOR 문제.png"
       style="width: 20%; height: auto; margin:10px">
</figure>
<br/>

3개의 뉴런을 이용해서 XOR 문제를 해결하는 과정을 보자. 앞 2개 뉴런의 결과 $y_1$, $y_2$ 가 뒷 뉴런의 입력으로 사용되어 최종 결과 $y_1$, $y_2$ 가 만들게 된다.

<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/XOR 문제 해결하는 뉴런 3개.png"
       style="width: 30%; height: auto; margin:10px">
</figure>
<br/>

계산의 예시를 하나 살펴보자. 일단 입력 값을 넣어 계산한 후, 그 결과를 활성 함수인 sigmoid 함수에 넣어서 $y_1$, $y_2$ 를 구한다. 그리고 $y_1$, $y_2$ 가 다시 뒷 뉴런에 들어가서 계산되고, sigmoid 함수를 거쳐 최종 결과 $y_1$, $y_2$ 를 만든다.

위 그림의 뉴런으로 계산한 최종 결과는 다음과 같다.

|x1 x2|y1 y2|$\hat{y}$|XOR|
|:--:|:--:|:--:|:---:|
|0 0|0 1|0|0|
|0 1|0 0|1|1|
|1 0|0 0|1|1|
|1 1|1 0|0|0|


앞서 처리한 2개의 뉴런은 벡터화를 통해 하나로 합해서 처리할 수 있다.

그럼 W와 b는 저 값 외에는 존재하지 않을까? W와 b를 학습하는 방법이 없을까? 바로 backpropagation을 이용하면 된다.

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*
