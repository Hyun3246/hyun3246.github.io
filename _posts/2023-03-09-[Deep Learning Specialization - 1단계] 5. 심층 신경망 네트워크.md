---
title:  "[Deep Learning Specialization - 1단계] 5. 심층 신경망 네트워크"
excerpt: "심층 신경망에서의 연산"

categories:
  - Machine Learning
tags:
  - [머신러닝, 신경망, 벡터화]

use_math: true
toc: true
toc_sticky: true
 
date: 2023-03-09
last_modified_at: 2023-03-09

header:
  overlay_image: /image/overlay image/andrew ng 1.png
---

## 심층 신경망
심층 신경망은 얕은 신경망에 비해 은닉층이 더 많은 신경망을 의미한다.

<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/심층 신경망 기본 구조.jpg"
       style="width: 70%; height: auto; margin:10px">
</figure>
<br/>

심층 신경망에서 사용되는 다양한 표기법에 대해 알아보자.
- L: 층의 개수 (ex. L = 4: 층이 4개)
- $n^{[l]}$: $l$번째 층에 속한 유닛의 개수 (ex. $n^{[1]} = 5$: 첫번째 층의 유닛이 5개)
- $a^{[l]}$: $l$번째 층의 활성화 값


<br/>

## 심층 신경망에서의 정방향 전파
심층 신경망에서의 정방향 전파라고 해서 얕은 신경망과 크게 다르거나 하지 않다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/심층 신경망 기본 구조.jpg"
       style="width: 70%; height: auto; margin:10px">
</figure>
<br/>

위 신경망에서 첫 번째 층의 정방향 전파 계산 과정은 다음과 같다.

$$z^{[1]} = W^{[1]}a^{[0]} + b^{[1]}$$

$$a^{[1]} = g^{[1]}(z^{[1]})$$

두 번째 은닉층의 계산 과정은 아래와 같다.

$$z^{[2]} = W^{[2]}a^{[1]} + b^{[2]}$$

$$a^{[2]} = g^{[2]}(z^{[2]})$$

두 과정이 매우 유사하게 생긴 것을 확인할 수 있을 것이다. 따라서 이를 일반화할 수 있으며, 반복문을 최대한 피하기 위해 벡터화도 적용할 것이다.

$$Z^{[l]} = W^{[l]}a^{[l - 1]} + b^{[l]}$$

$$A^{[l]} = g^{[l]}(Z^{[l]})$$

그리고 이 과정을 여러 개의 은닉층에서 반복해야 한다. 여기서는 아쉽게도 반복문을 피할 수 없다. 따라서 위의 공식을 신경층의 개수만큼 반복해주어야 한다.

<br/>

## 행렬의 차원 확인하기
신경망을 코딩할 때 가장 버그가 많이 생기는 곳은 행렬의 차원에 관한 부분이다. 행렬의 차원을 잘못 지정하여 행렬 간 연산이 되지 않는다면 코드가 제대로 실행되지 않을 것이다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/심층 신경망 기본 구조.jpg"
       style="width: 70%; height: auto; margin:10px">
</figure>
<br/>

일단 벡터화를 하지 않았다고 생각하고 행렬의 차원을 생각해보자. 첫 번째 은닉층에서의 첫 계산은 다음과 같다.

$$z^{[1]} = W^{[1]}x + b^{[1]}$$

z는 (3, 1) 행렬, x는 (2, 1) 벡터이다. 이로부터 W가 (3, 2) 행렬이라는 것을 도출할 수 있다(행렬 간 곱셈이 가능해야하기 때문). b는 (3, 1) 행렬이 될 것이다. 조금 일반화하면 z는 $(n^{[l]}, 1)$, W는 $(n^{[l]}, n^{[0]})$, x는 $(n^{[0]}, 1)$, b는 $(n^{[1]}, 1)$ 이 될 것이다. 완전히 일반화하면 다음과 같다.

- $W^{[l]}:\,(n^{[l]}, n^{[l - 1]})$
- $b^{[l]}:\,(n^{[l]}, 1)$
- $dW^{[l]}:\,(n^{[l]}, n^{[l - 1]})$
- $db^{[l]}:\,(n^{[l]}, 1)$

dW와 db는 각각 W와 b의 차원과 동일하다.

그 다음 계산은 다음과 같다.

$$a^{[1]} = g^{[1]}(z^{[1]})$$

여기서는 a와 z가 같은 차원을 가져야 한다는 것을 알 수 있다.

이번에는 벡터화한 경우를 살펴보자. 벡터화를 하면 벡터 x가 행렬 X가 되는 것이기 때문에 W의 차원은 변하지 않는다. 또한, b의 차원 역시 그대로 두어도 broadcasting에 의해 파이썬이 알아서 계산을 잘 수행한다.

변하는 것은 계산 결과에 해당한다고 할 수 있는 a와 z이다. 모두 벡터에서 행렬이 된다. 행렬 X가 $(n^{[l-1]}, m)$ 의 형태를 띠기 때문에 $Z^{[l]}$와 $A^{[l]}$ 모두 $(n^{[l]}, m)$ 의 형태를 가진 행렬이 된다. $dA^{[l]}$, $dZ^{[l]}$ 또한 마찬가지다.

<br>

## 왜 심층 신경망이 필요할까?
심층 신경망이 필요한 이유는 간단하다. 얕은 신경망으로 할 수 없던 더 복잡한 분석을 진행할 수 있기 때문이다.

얼굴 인식 프로그램을 만든다고 생각해보자. 먼저 얼굴 그림에 있는 각종 모서리의 방향과 위치를 파악한다. 그리고 그 분석 데이터를 가지고 눈, 코와 같은 얼굴의 일부를 감지한다. 그 다음에는 다시 그 정보를 가지고 서로 다른 종류의 얼굴을 인식한다. 이처럼 심층 신경망을 이용하면 점점 복잡한 분석을 진행할 수 있다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/심층 신경망으로 얼굴 인식.jpg"
       style="width: 70%; height: auto; margin:10px">
</figure>
<br/>

음성 데이터 역시 비슷한 과정을 거친다. 먼저 낮은 수준에서 음성을 구분한 뒤, 음소, 단어, 문장 순으로 점점 복잡한 분석을 진행하는 것이다.

심층 신경망의 또다른 장점으로는 계산의 복잡도를 줄일 수 있다는 것에 있다.

비트 연산의 일종은 XOR 연산을 진행한다고 해보자. 얕은 신경망을 이용하면 비트 조합의 모든 가능성을 한 은닉층에서 열거해서 답을 도출해야 하기 때문에 $O(2^n)$ 의 복잡도를 가진다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/얕은 신경망으로 XOR.jpg"
       style="width: 50%; height: auto; margin:10px">
</figure>
<br/>

그러나 은닉층이 여러 개인 심층 신경망을 이용하면 단계적인 연산을 수행할 수 있기 때문에 복잡도가 $O(\log{n})$ 으로 개선된다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/심층 신경망으로 XOR.jpg"
       style="width: 50%; height: auto; margin:10px">
</figure>
<br/>

이처럼 심층 신경망은 강력한 장점을 가지고 있다.