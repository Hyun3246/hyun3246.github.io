---
title:  "[Deep Learning Specialization - 4단계] 2. 케이스 스터디 - 1"
excerpt: "합성곱 층을 사용하는 다양한 신경망"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 신경망, 합성곱, 컴퓨터 비전]

use_math: true
toc: true
toc_sticky: true
 
date: 2023-11-11
last_modified_at: 2023-11-25

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/andrew ng 4.jpg
---
이번 강의에서는 다양한 컴퓨터 비전 신경망에 대해 알아본다.

## LeNet - 5
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/Lenet-5.png"
       style="width: 70%; height: auto; margin:10px">
  <figcaption style="text-align:center; font-size:14px; color:#808080">
    출처: 네이버 부스트코스
  </figcaption>
</figure>
<br/>

LeNet - 5 신경망은 90년대에 고안된 역사가 깊은 컴퓨터 비전 신경망이다. 흑백 이미지를 판별하는 데 주로 사용되었으며, 처음 고안되었을 때는 최대 풀링 대신 평균 풀링이 주로 사용되었다. 위 그림에서 볼 수 있듯이 합성곱 층, 풀링 층을 번갈아가며 사용한다. 그리고 마지막에 완전 연결 층을 사용하고 결과를 도출한다. 왼쪽에서 오른쪽으로 이동하면서 높이와 너비는 감소하는 한편, 채널의 개수는 증가하는 것을 관찰할 수 있다.

위 LeNet - 5 신경망에서는 60,000개의 매개변수들이 사용되었다.

<br/>

## AlexNet
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/AlexNet.png"
       style="width: 70%; height: auto; margin:10px">
  <figcaption style="text-align:center; font-size:14px; color:#808080">
    출처: 네이버 부스트코스
  </figcaption>
</figure>
<br/>

AlexNet 신경망은 LeNet 신경망과 유사하다. 그러나 훨씬 크다는 특징(매개변수가 60,000,000개)을 가지고 있다.

일단, AlexNet 신경망은 컬러 이미지를 인식할 수 있다. 그리고 최대 풀링을 사용한다. 또한, LeNet과는 다르게 활성 함수로 ReLU를 사용한다.

<br/>

## VGG - 16
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/VGG-16.png"
       style="width: 70%; height: auto; margin:10px">
  <figcaption style="text-align:center; font-size:14px; color:#808080">
    출처: 네이버 부스트코스
  </figcaption>
</figure>
<br/>

VGG - 16 신경망에서는 합성곱 층과 최대 풀링 층의 규칙을 고정해놓고 시작한다. 합성곱 층에서는 (3 x 3)의 필터(스트라이드 1)을 이용해 패딩으로 너비를 보존하는 동일 합성곱을 진행한다. 최대 풀링 층에서는 (2 x 2)의 필터를 사용한다.

첫번째 단계의 '[CONV 64] x 2'는 64개의 필터를 이용해 합성곱을 2번 한다는 의미이다. 그 결과 채널이 64개 형성되었다. 이후에도 합성곱 층과 풀링 층을 번갈아가며 진행한다.

VGG - 16의 특징이라면 높이와 너비가 합성곱 층을 지날 때마다 계속해서 절반으로 줄어드는 반면, 채널은 2배로 증가한다는 점이다. VGG - 16는 매개변수가 많아 네트워크의 크기가 커지는 단점이 있다.

<br/>

## Residual 신경망
우리가 지금까지 봤던 신경망은 보통 아래의 계산 과정을 거쳤다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/신경망 main path.png"
       style="width: 50%; height: auto; margin:10px">
  <figcaption style="text-align:center; font-size:14px; color:#808080">
    출처: 네이버 부스트코스
  </figcaption>
</figure>
<br/>

Residual 신경망(ResNets)에서는 $a^{[l]}$을 뒤로 이동시켜 $z^{[l+2]}$에 비선형성을 적용해주기 전에 $a^{[l]}$을 더한다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/Residual block.png"
       style="width: 50%; height: auto; margin:10px">
  <figcaption style="text-align:center; font-size:14px; color:#808080">
    출처: 네이버 부스트코스
  </figcaption>
</figure>
<br/>

위 그림에서 표현된 단편적인 과정을 Residual block이라고 한다. 또한, $a^{[l]}$을 뒤로 이동시키는 과정을 'short cut' 혹은 'skip connection'이라고 부른다.

ResNets의 개발자들은 아래의 신경망을 'Plain network'라고 표현한다. 여러 개의 Residual block을 연속적으로 배치한 형태이다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/Plain network.png"
       style="width: 70%; height: auto; margin:10px">
</figure>
<br/>

우리가 지금까지 봤던 일반적인 신경망들은 일정 개수 이상으로 층이 증가하면 (이론과는 달리) 학습 오류가 증가하였다. 그러나 ResNets은 층의 개수가 증가할수록 학습 오류가 계속해서 감소한다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/Plain과 ResNets 학습 오류 비교.png"
       style="width: 50%; height: auto; margin:10px">
</figure>
<br/>

## ResNets이 작동하는 이유
ResNet의 핵심 연산 과정을 다시 보자. (활성 함수는 ReLU이다.)

$a^{[l+2]} = g(z^{[l+2]} + a^{[l]})$

$ = g(W^{[l+2]}a^{[l+1]} + b^{[l+2]} + a^{[l]})$

위 식에서 $W^{[l+2]}$, $b^{[l+2]}$가 0이라고 해보자. 그럼 $a^{[l+2]} = g(a^{[l]}) = a^{[l]}$ 가 되어 항등식이 된다. 이 항등식의 의미는 신경망으로 하여금 스킵 연결을 통해 두 층이 없는 더 간단한 항등식을 학습하여, 두 층 없이도 더 좋은 성능을 낼 수 있게 만든다는 것이다.

다만, $z^{[l+2]}$와 $a^{[l]}$이 같은 차원을 가져야 한다. 따라서 동일 합성곱을 하거나 차원을 같게 만들어주는 행렬 $W_s$를 Residual block 앞에 곱해준다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/Plain과 ResNets 형태 비교.png"
       style="width: 70%; height: auto; margin:10px">
</figure>
<br/>

> ResNets 추가 설명 <figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Specialization/ResNets 추가 설명.png"
       style="width: 50%; height: auto; margin:10px"></figure>
Input 값(x)은 그대로 가져오고, 나머지 잔여 정보인 F(x)만을 추가적으로 더해주는 단순한 형태로 만들어 준다. 즉, 잔여효과(추가적인 정보)인 F(x)만 학습을 하면 된다. 따라서 전체를 학습하는 것보다 학습이 오히려 쉬워지고, 수렴을 더 잘 할 수 있게 된다.

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*

*& Special Thanks to park paul's blog*
