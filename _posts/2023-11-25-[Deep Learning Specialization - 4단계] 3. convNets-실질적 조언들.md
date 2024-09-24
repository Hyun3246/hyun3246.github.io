---
title:  "[Deep Learning Specialization - 4단계] 3. convNets-실질적 조언들"
excerpt: "컴퓨터 비전에서의 전이학습과 데이터 증가"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 신경망, 합성곱, 컴퓨터 비전]

use_math: true
toc: true
toc_sticky: true
 
date: 2023-11-25
last_modified_at: 2023-11-25

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/andrew ng 4.jpg
---
## 전이학습 활용하기
다른 문제를 해결하기 위해 만들어진 신경망을 그대로 가져와 우리가 해결을 원하는 문제에 적용하는 것을 전이학습이라고 배웠었다.

[전이학습 복습하기](https://hyun3246.github.io/machine%20learning/Deep-Learning-Specialization-3%EB%8B%A8%EA%B3%84-6.-%EB%8B%A4%EC%96%91%ED%95%9C-%EB%AC%B8%EC%A0%9C%EB%A1%9C%EB%B6%80%ED%84%B0-%ED%95%99%EC%8A%B5%EC%8B%9C%ED%82%A4%EA%B8%B0/#%EC%A0%84%EC%9D%B4%ED%95%99%EC%8A%B5)

컴퓨터 비전 문제에서는 전이학습을 매우 유용하게 활용할 수 있고, 또 활용하는 것이 강조된다. 특히 <span style="color:#F5F5F7">우리가 신경망 구축에 사용할 수 있는 사진의 개수가 턱없이 부족해서 training set을 제대로 만들기 어려울 때 전이학습을 이용</span>하면 그나마 수월하다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/컴퓨터 비전에서의 전이학습.png"
       style="width: 70%; height: auto; margin:10px">
  <figcaption style="text-align:center; font-size:14px; color:#808080">
    가장 위에서부터 예시가 매우 부족할 때, 적당히 부족할 때, 어느 정도 있을 때의 상황이다.
  </figcaption>
</figure>
<br/>

학습을 위한 예시가 턱없이 부족할 때는 맨 위의 경우처럼 마지막 softmax를 제외한 모든 부분을 그대로 가져와 사용할 수 있다. 이를 동결(freeze)시킨다고 표현한다. 예시가 아주 부족하지는 않은 상황에서는 가져온 신경망의 일부만 동결하고 나머지는 직접 학습할 수 있다. 마지막으로 예시가 어느 정도 확보되었을 때는 신경망 전체를 직접 학습시켜도 된다.

<br/>

## 데이터 증가
앞서 컴퓨터 비전에서 더 많은 데이터를 확보하는 방법 중에 몇 가지로 이미지를 뒤집거나 일부를 자르는 방법을 살펴보았다.

두 가지 방법 외에도 컬러 이미지인 점을 활용해볼 수 있다. R, G, B 각각의 채널에 특정 숫자들을 더해주어 색조를 살짝 바꾸어주는 것이다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/색조 변화로 데이터 증가.png"
       style="width: 50%; height: auto; margin:10px">
</figure>
<br/>

하나만 빠르게 살펴보자. 첫 번째 경우에서는 R과 B에 20을 더하고, G에서 20을 빼었다. 그 결과, 보라색이 더 짙은 사진이 탄생했다.

이미지에 더해줄 값은 'PCA color augmentation'을 통해 결정할 수 있다. 말 그대로 주성분 분석을 이용하는 것인데, 이미지의 전체적인 색조를 분석해 이를 유지하는 방향으로 색을 변경한다.

데이터의 변형은 주로 CPU 스레드를 통해서 데이터를 불러옴과 동시에 변형을 시켜 미니 배치를 만들어준다.

<br/>

## 컴퓨터 비전에 대한 몇 가지 조언
아래 그림은 해결하고자 하는 문제와 데이터의 양에 대한 상관관계이다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/해결하고자 하는 문제와 데이터의 양에 대한 상관관계.png"
       style="width: 70%; height: auto; margin:10px">
</figure>
<br/>

음성 인식은 대표적으로 데이터를 많이 확보할 수 있는 문제이다. 반면, 이미지 인식이나 물체 인식은 데이터의 수가 부족한 문제들이다.

> 이미지 인식 vs 물체 인식 <br/>
이미지 인식: 주어진 이미지가 우리가 원하는 이미지인지 아닌지만 판단. 예를 들어 고양이 인식 프로그램. <br/>
물체 인식: 주어진 이미지에서 사물들을 인식하여 그 사물이 무엇인지를 판단. 예를 들어, 경계용 CCTV나 자율주행에서 사용하는 프로그램.

데이터가 많은 문제들은 더 간단한 알고리즘으로 해결할 수 있고, 실제 직접 구현해야하는 부분이 적다. 그러나 데이터가 적은 문제들은 복잡한 알고리즘을 사용해야 하며, 직접 구현해야하는 부분도 늘어난다. 또, 문제에 특화된 방법을 사용해야 더 좋은 성능을 낼 수 있다.

이러한 문제점을 가진 컴퓨터 비전 신경망을 만들 때는 <span style="color:#F5F5F7">이미 구현된 오픈소스 코드를 참고하는 것이 매우 유용</span>하다. 이 코드들은 개발자들이 벌써 수많은 이미지들을 이용해 학습을 마친 것들이고, 따라서 매개변수나 가중치들이 상당히 쓸만하다. 초매개변수 역시 마찬가지다.

<br/>

## 컴퓨터 비전 개발 경쟁에서 승리하기 위한 팁
컴퓨터 비전 알고리즘 개발이나 대회에서 승리하기 위한 작은 팁으로는 크게 두 가지가 있다.

1. 앙상블(Ensembling): 3개 ~ 15개의 신경망을 독립적으로 학습하고 결과를 평균 내기
2. 다중 크로핑: 하나의 이미지를 여러 번 크로핑(자르기)하여 평균 내기

그러나 이 방법들을 <span style="color:#F5F5F7">실사용을 위한 신경망 개발에 사용하면 아주 곤란</span>하다.

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*