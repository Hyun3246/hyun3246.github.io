---
title:  "[Deep Learning Specialization - 1단계] 1. 딥러닝 소개"
excerpt: "신경망이란 무엇인가, 신경망의 종류와 활용"

categories:
  - Machine Learning
tags:
  - [머신러닝, 신경망]

use_math: true
toc: true
toc_sticky: true
 
date: 2023-02-27
last_modified_at: 2023-02-28

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/andrew ng 1.png
---

## 강의 개요
- 강의명: Deep Learning Specialization - 1단계: 신경망과 딥러닝
- 교수: Andrew Ng
- 제작: DeepLearning.AI, 네이버 부스트코스

<br/>

## 신경망(Neural Network)란 무엇인가?
집의 크기에 따라서 가격이 정해진다고 가정해보자. 여러 개의 사례들을 바탕으로 추세선을 그려서 함수를 만들면 아래처럼 나타낼 수 있을 것이다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/집 크기에 따른 가격 함수.jpg"
       style="width: 100%; height: auto; margin:10px">
</figure>
<br/>

(이렇게 처음에는 0이었다가 점점 증가하는 모양의 함수를 ReLU(Rectified Linear Unit)라고 한다.)

이 예시에서 신경망(Neural Network, NN)의 기본적인 구조에 대해 알 수 있다. 처음에 크기와 관련된 값(x)을 집어 넣으면, 신경(neuron)을 거쳐, 가격(y)이 도출되는 구조를 가진다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/신경망의 기본 구조.jpg"
       style="width: 50%; height: auto; margin:10px">
</figure>
<br/>

더 복잡한 신경망을 생각해볼 수도 있다. 방의 개수, 주소(우편번호), 부(wealth)에 의해 가족 크기, 걸어다닐 수 있는 정도, 학군 등이 결정되고, 다시 그 요소들이 모여 집의 가격이 결정되는 것처럼 말이다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/다양한 요소들에 의해 집 가격 결정.jpg"
       style="width: 100%; height: auto; margin:10px">
</figure>
<br/>

좀 더 체계적으로 그릴 수도 있다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/집 가격 결정 신경망.jpg"
       style="width: 100%; height: auto; margin:10px">
</figure>
<br/>

가장 왼쪽에 있는 요소들을 '입력특성'이라고 하고, 중간에 보이지는 않는 또다른 요소들을 '은닉유닛'이라고 한다. 여러 개의 입력특성이 모여 은닉유닛을 구성하고, 이들이 다시 결과를 결정한다.

<br/>

## 지도학습과 신경망
신경망을 사용하여 지도학습을 하는 예시는 매우 많다. 사용자의 정보를 이용해 맞춤형 광고를 제공하는 프로그램, 피사체가 무엇인지 구별하는 프로그램, 번역기 등은 모두 지도학습을 이용한다.

신경망에는 대표적으로 세 가지가 있다.

첫 번째는 Standard NN이다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/Standard NN.jpg"
       style="width: 70%; height: auto; margin:10px">
</figure>
<br/>

Standard NN은 앞서 살펴본 집의 가격을 예측하는 함수나 맞춤형 광고를 제공할 때 주로 쓰인다.

두 번째는 Convolutional NN(CNN)이다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/Convolutional NN.jpg"
       style="width: 70%; height: auto; margin:10px">
</figure>
<br/>

이미지를 입력받아 사물을 구별하는 프로그램이 CNN을 활용하는 대표적인 예시이다.

마지막으로 Recurrent NN(RNN)이 있다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/Recurrent NN.jpg"
       style="width: 70%; height: auto; margin:10px">
</figure>
<br/>

연속적인 배열을 입력받아 처리할 때 유용하게 사용된다. 연속적인 소리의 배열인 오디오를 입력받아 문자로 변환하거나, 연속적인 단어의 배열인 문장을 입력받아 번역하는 번역기 등이 RNN을 사용한다.

지도학습에서 사용하는 데이터로는 구조화(Structured) 데이터와 비구조화(Unstructured) 데이터가 있다. 구조화된 데이터는 데이터베이스처럼 행과 열로 잘 정리된 데이터를 말한다. 비구조화 데이터는 음성이나 사진, 문자 등 정리되지 않은 데이터를 의미한다.        

비구조화 데이터는 구조화된 데이터에 비해 컴퓨터로 처리하기 어렵다는 단점이 있다. 그러나 최근에는 딥러닝 기술의 발전으로 단점이 많이 보완되었다.

비구조화 데이터로 지도학습을 수행하는 것은 매우 간지나지만, 금전적인 수익을 발생시키는 것은 구조화 데이터이다. 많은 기업들에서는 고객의 정보를 구조화하여 관리하고, 이를 맞춤형 광고 등에 이용해서 수익을 낸다.

<br/>

## 딥러닝 기술이 왜 이슈가 되는가
딥러닝, 머신러닝 기술은 오래전부터 고안되고 개발되어온 분야이다. 그런데 왜 최근에야 각광받을까?

<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/딥러닝 기술 발전 그래프.jpg"
       style="width: 100%; height: auto; margin:10px">
  <figcaption style="text-align:center; font-size:14px; color:#808080">
    가로 축은 '레이블이 있는' 데이터의 크기를 말한다. m은 training set의 크기라고 약속한다.
  </figcaption>
</figure>
<br/>

전통적인 학습 알고리즘은 데이터의 양이 일정량 이상이 되었을 때 성능의 한계에 도달한다. 그리고 그 성능의 한계를 넘어서지 못한다. 이로 인해 과거에는 아무리 많은 데이터를 모아도(그렇게 많은 데이터를 모을 수도 없었지만) 효과적으로 처리하고 분석할 방법이 없었다.

그러나 신경망을 이용한 기술은 데이터의 양이 늘어나도 효율적으로 처리할 수 있다. 심지어는 스스로 학습하며 성능을 증가시키기도 한다. 이는 데이터의 양이 작을 때는 두드러지지 않지만, 데이터의 양이 매우 증가하면 두드러지게 된다.

현대에는 데이터의 양이 기하급수적으로 늘어나고, 이를 처리할 신경망 연구가 활발해짐과 동시에 CPU, GPU 등 연산을 실질적으로 처리해줄 기술적 진보도 뒷받침되었다. 

그 중 알고리즘의 발전은 계산을 더욱 효과적으로 수행할 수 있게 해주었는데, 대표적인 것이 시그모이드 함수를 ReLU 함수로 바꾸는 것에 관한 것이다. 시그모이드 함수 양쪽의 기울기가 0에 수렴하는 부분은 머신러닝에서 시그모이드 함수를 처리하는 것을 매우 어렵게했는데, ReLU가 이를 해결해주었기 때문이다.

어쨌든 아이디어를 코드로 구현하고, 이를 실행하여 검증한 뒤, 다시 아이디어를 수정하는 일련의 과정에 소요되는 시간이 점점 짧아짐으로써, 딥러닝 분야는 빠르게 발전하고 있다.

<br/>
<br/>

*포스트에 사용된 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*