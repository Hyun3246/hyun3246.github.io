---
title:  "[Deep Learning Basic Starting with TF] 8. 딥러닝의 기본 개념"
excerpt: "딥러닝 개발의 역사"

categories:
  - Data Science & ML
tags:
  - [머신러닝]

use_math: true
toc: true
toc_sticky: true

date: 2024-11-13
last_modified_at: 2024-11-13

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## 딥러닝의 시작
생물학의 뉴런에서 아이디어를 얻어 시작된 인공 뉴런은 다음과 같은 구조를 가지고 있다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/인공 뉴런의 구조.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

위 인공 뉴런을 여러 개 합쳐서 인공 신경망을 만들 수 있다. 1950년대에는 아래와 같은 기계로 가중치를 조절하여 결과를 도출하였다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/1950년대 AI 기계.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

인공 신경망에 대한 기대감이 높아지자 연구자들은 '나중에는 컴퓨터가 스스로 글을 쓰고 걷고, 심지어는 자아를 가질 수도 있다'는 말도 하였다.

<br/>

## 첫 고비 - XOR 문제
딥러닝이 첫 고비를 맞은 것은 XOR 문제를 마주했을 때다. 앞서 살펴본 신경망들은 하나의 결정 경계를 만드는 데, 이는 AND/OR 문제는 잘 해결하였지만 XOR 문제는 해결할 수 없었다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/AND OR, XOR 문제.png"
       style="width: 40%; height: auto; margin:10px">
  <figcaption style="text-align:center; font-size:14px; color:#808080">
    AND/OR 문제(왼쪽 2개)는 하나의 결정 경계만으로도 정답을 가릴 수 있다. 반면, XOR 문제(오른쪽)는 하나의 결정 경계만으로는 완벽하게 정답을 가릴 수 없다.
  </figcaption>
</figure>
<br/>

AND/OR 문제(왼쪽 2개)는 하나의 결정 경계만으로도 정답을 가릴 수 있다. 반면, <span style="color:#F5F5F7">XOR 문제(오른쪽)는 하나의 결정 경계만으로는 완벽하게 정답을 가릴 수 없다</span>.

이렇게 간단한 문제를 해결할 수 없다는 사실에 사람들이 실망했다. 여기에 더해 당대 최고의 AI 전문가 Marvin Minsky는 '지구 상의 어떤 사람도 다층 퍼셉트론을 훈련할 좋은 방법을 찾을 수 없다'라며 상당히 회의적인 시각을 드러냈다. ~~AI에게 지배당한 미래에서 온 구원자~~ 이로 인해 deep learning은 깊은 침체에 빠지게 된다.

<br/>

## 재도약 - Backpropagation
이렇게 사람들 사이에서 잊혀지던 인공 신경망이었지만, Paul Werbos(1974, 1982)가 고안해 낸 backpropagation에 의해 문제 해결의 가능성이 열리게 된다. 그리고 그의 연구는 발표 당시에는 주목받지 못했지만, Hinton이 1986에 이를 재발견해내어 세상에 알려지게 된다.

[심층 신경망과 Backpropagation](https://hyun3246.github.io/data%20science%20&%20ml/Deep-Learning-Specialization-1%EB%8B%A8%EA%B3%84-5.-%EC%8B%AC%EC%B8%B5-%EC%8B%A0%EA%B2%BD%EB%A7%9D-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/)

또한 비슷한 시기에 Convolutional Neural Network(CNN)도 고안된다. 이는 사물의 형태에 따라 활성화되는 뉴런이 다르며, 이 신호들이 나중에 조합되어 물체를 인식한다는 생명체의 신경 전달에서 힌트를 얻어 고안되었다. CNN은 그림을 부분 부분 잘라서 신경망을 학습하고, 이를 나중에 합치는 방식을 사용한다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/CNN 기본 개념.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

이를 활용하여 이미 1980년대 당시에 자율 주행 자동차를 고안하였고, 일부 테스트도 성공하였다고 한다.

<br/>

## 두 번째 고비 - 너무 깊은 신경망
이렇게 잘 발전하고 있던 딥러닝에 다시 한 번 회의적인 시각이 비치게 된다. 그 이유는 층이 많은 심층 신경망보다 비교적 간단한 SVM, RandomForest 같은 알고리즘이 더 잘 작동하였기 때문이다. <span style="color:#F5F5F7">심층 신경망의 효용성에 대한 의문</span>이 제기되었다.

<br/>

## 다시 한 번 고비를 넘기다
캐나다의 CIFAR라는 단체는 당장 돈이 되지 않더라도 인류에게 도움이 되는 연구를 지원해준다. 딥러닝 연구가 고비를 맞아 연구자들이 연구를 이어가기 어려웠을 때(Neural Network라는 단어가 들어가기만 해도 논문 기고가 안 될 정도였다고 한다), CIFAR는 딥러닝 연구자들을 지속해서 지원하였고, 결국 그 빛을 보게 된다.

2006년에 Hinton와 Bengio는 인공 신경망에서는 <span style="color:#F5F5F7">가중치들의 초깃값을 잘 주는 것이 중요하다</span>는 연구 결과를 발표하였다. 초깃값만 잘 주어도 더 효율적으로 복잡한 문제를 해결할 수 있음이 밝혀졌고, 딥러닝 연구는 다시 활발해지게 되었다. 기존의 neural network를 대체할 수 있는 새로운 용어인 'Deep Learning'도 이때 새롭게 고안되었다.

<br>

## 딥러닝 전성시대
이제 딥러닝과 AI는 완전한 전성시대를 맞았다고 봐도 과언이 아니다. 컴퓨터로 이미지를 구분하는 경연대회인 ImageNet Challenge에서, CNN은 26%에 달하던 기존 오차율을 한 번에(정말 1회 대회 만에) 15% 수준까지 낮추었고, 지금은 사람보다 더 뛰어난 분류 성능을 보이고 있다. 뿐만 아니라 50년대 연구자들이 했던 이야기 중 일부인 '직접 쓰고, 말하고, 걷는' 컴퓨터도 이미 실현되었다. 

그리고 딥러닝 연구가 고비를 맞을 때마다 딥러닝을 위기에서 구해낸 Hinton은 그 공로를 인정받아 2024년 노벨 물리학상을 수상하였다.

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*