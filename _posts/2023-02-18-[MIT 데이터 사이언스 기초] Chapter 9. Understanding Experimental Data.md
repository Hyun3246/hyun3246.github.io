---
title:  "[MIT 데이터 사이언스 기초] Chapter 9. Understanding Experimental Data"
excerpt: "선형회귀와 적합성 판단"

categories:
  - Data Science
tags:
  - [Data Science, 시뮬레이션, 선형회귀, 결정계수]

use_math: true
toc: true
toc_sticky: true
 
date: 2023-02-18
last_modified_at: 2023-02-19
---

## 선형회귀
실험을 통해 얻은 데이터를 이용해 계산을 설계해야 할 때가 있다. 예를 들어, 용수철의 용수철 상수 k의 값을 알아내기 위해 무게를 늘려가며 용수철이 늘어나는 길이를 재는 실험을 생각해볼 수 있다.
> cf. 용수철에 힘을 주어 변형을 가하면 아래와 같은 '훅의 법칙'을 따른다.      
$ F = - kd $        
여기서 F는 힘(뉴턴), d는 변화한 길이, k는 용수철 상수를 의미한다. 음수 부호가 붙은 이유는 힘이 용수철을 변형한 방향 반대로 작용하기 때문이다.

무게에 따른 변형 길이를 아래처럼 2차원 평면에 표현할 수 있다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/용수철 실험 결과.png"
       style="width: 100%; height: auto; margin:10px">
</figure>
<br/>

실험 결과가 훅의 법칙처럼 선형적인 관계를 나타낼 수 없다는 것을 알 수 있다. 따라서 우리는 이 결과들을 가장 잘 표현하는 직선(혹은 곡선)을 찾아야 한다. 이 경우에는 찾으려는 직선이 각 점까지의 거리를 최소로 만들면 된다.

그런데 어떤 거리를 써야할까? x축 방향 거리가 최소여야 할까? 아니면 y축? 그것도 아니라면 점과 직선 사이의 최단거리?

이 경우에는 y축 방향의 거리를 사용하는 것이 좋다. 실험 결과가 나타나 있는(종속변수) 축이 y축이기 때문이다.

'최소제곱 목적 함수'는 이 거리를 공식화하고 있다. 아래 공식의 값이 최소가 될 때, 그 직선이 데이터를 대변하는 데 가장 적합하다고 할 수 있다.

$\displaystyle\sum_{i=0}^{len(observed) - 1}{(observed[i] - predicted[i])^2}$

제곱을 하는 이유는 여러 가지가 있다. 부호를 제거할 수도 있고, 위 공식을 최솟값을 가지는 함수로 기능하게 할 수도 있다 (이차함수를 떠올리면 쉽다).    

위 식을 사용하기 위해서는 일단 곡선을 찾아야 한다. 예측 모델의 다항식 표현을 찾기 위해 '선형회귀'를 사용한다.

선형회귀를 설명하기 위해 일차 다항식 $y=ax+b$를 예를 들어 보자. 이 다항식을 사용해 모든 x값에 대해 y값을 계산하고 최소제곱 목적 함수에 대입한다. a와 b의 값을 바꾸어가면서 목적 함수의 값이 가장 최소가 되는 a, b를 찾으면 그 것이 바로 가장 잘 들어맞는 직선인 것이다.

운이 좋게도, 파이썬에서는 일일이 이를 계산할 필요가 없다. `pylab`의 `polyfit`을 사용하면 원하는 차수에 대해 가장 잘 들어맞는 다항식을 찾아준다.     
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/용수철 피팅.png"
       style="width: 100%; height: auto; margin:10px">
</figure>
<br/>

<br/>

## 적합한 회귀 찾기
아래와 같은 데이터를 1차 다항식으로 피팅한다고 하자.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/의미없는 1차 다항식 피팅.png"
       style="width: 100%; height: auto; margin:10px">
</figure>
<br/>

매우 부적절한 직선이 생성되었다. 전혀 쓸모가 없는 피팅이다. 2차원 피팅은 어떨까?
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/좀 더 나은 2차 피팅.png"
       style="width: 100%; height: auto; margin:10px">
</figure>
<br/>

그나마 1차보다는 나아보인다. 그러나 눈대중으로 보는 것 말고, 진짜 더 나은 피팅인지 테스트할 방법은 없을까?

먼저 상대적인 관점에서 분석해보자. 2차가 1차보다 더 나은지를 살펴보는 것이다. 이미 살펴본 공식으로 충분하다. 제곱 오차의 값을 비교하면 되는 것이다.

그러나 우리는 절대적인 적합도를 판단하고 싶다. 두 개 중에 더 나은지가 아니라, 전체적인 회귀 곡선 중에서 얼마나 정확한지를 말이다. 절대적인 적합도를 판단할 때는 결정계수($R^2$)를 사용한다.

$R^2 = 1- \frac{\sum_{i}^{}{(y_i - p_i)^2}}{\sum_{i}^{}{(y_i - \mu)^2}}$

$y_i$는 측정 값, $p_i$는 추정 값, $\mu$는 측정 값을 평균을 의미한다. 추정 오차를 측정 데이터의 변이성(편차)으로 나누는 과정으로, 데이터 변이성의 비율을 알려준다.       

결정계수가 1이면, 완벽한 모델이라고 할 수 있다. 오차가 0이라는 뜻이기 때문이다. 결정계수가 0이면 최악의 모델이다. 오차와 편차의 비율이 1이라는 뜻이기 때문이다. 결정계수가 0.5이면 모델의 데이터의 변이성 중 절반을 설명한다.

아래 그림은 다양한 차수로 피팅한 뒤 결정계수를 구한 것이다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/다양한 차수 결정계수.png"
       style="width: 100%; height: auto; margin:10px">
</figure>
<br/>

<br/> 

[관련코드 보러가기](https://github.com/Hyun3246/Code-Warehouse/tree/main/MIT%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%82%AC%EC%9D%B4%EC%96%B8%EC%8A%A4%20%EA%B8%B0%EC%B4%88)

<br/>
<br/>

*포스트에 사용된 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*