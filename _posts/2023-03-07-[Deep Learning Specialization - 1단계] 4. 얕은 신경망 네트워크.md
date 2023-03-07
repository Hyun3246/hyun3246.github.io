---
title:  "[Deep Learning Specialization - 1단계] 4. 얕은 신경망 네트워크"
excerpt: "얕은 신경망에 벡터화를 이용한 계산 적용하기"

categories:
  - Machine Learning
tags:
  - [머신러닝, 신경망, 로지스틱 회귀, 벡터화]

use_math: true
toc: true
toc_sticky: true
 
date: 2023-03-07
last_modified_at: 2023-03-07

header:
  overlay_image: /image/overlay image/andrew ng 1.png
---
## 신경망의 표현
신경망은 앞선 강의들에서 보았던 연산을 수행하는 여러 층으로 나누어져 있다고 이해하면 된다. 데이터 x들이 입력되면 신경층(Layer)을 거쳐 결과를 도출한다. 이전 신경츨에서 계산된 결과가 다음 신경층을 계산하는 입력으로 사용된다.

신경망의 기본적인 구조는 아래와 같다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/신경망 기본 구조.jpg"
       style="width: 70%; height: auto; margin:10px">
</figure>
<br/>

가장 왼쪽에 위치하는 x들은 입력층(Input Layer)이다. 행렬로 X라고 쓰기도 하지만, 0번째 신경층이라는 의미로 $a^{[0]}$ 이라고 표현하기도 한다. **보통 대괄호를 이용해서 신경층을 표현하고, 소괄호를 이용해서 몇 번쨰 훈련 데이터인지를 나타낸다. 아래첨자는 몇 번쨰 노드인지를 가리킨다.**

다음 층은 은닉층(Hidden Layer)이다. 은닉층은 훈련 데이터와 결과에는 나타나지 않는다. 중간 계산 과정인 것이다. $a^{[1]}$ 로 표현한다. 첫번째 은닉층에서 사용되는 매개변수 W(행렬)와 b 역시 위 첨자를 이용해서 $W^{[1]}, b^{[1]}$ 로 나타내기도 한다. 위 예시에서 W는 (4, 3), b는 (4, 1)의 모양이다. 앞은 은닉층 노드의 개수, 뒤는 입력층 노드의 개수이다.

결과층(Output Layer)는 하나의 노드로 이루어져 있다. 여기 역시 계산에 사용되는 $W^{[2]}, b^{[2]}$ 가 있으며, 각각 (1, 4), (1, 1)의 형태이다.

위 예시는 **2개의 층으로 구성된 신경망**으로 표현한다. 입력층은 층을 셀 때 포함하지 않는 것이다.

<br/>

## 신경망 결과 계산하기
하나의 노드는 다음과 같이 나타낼 수 있다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/신경망 하나의 노드.jpg"
       style="width: 50%; height: auto; margin:10px">
</figure>
<br/>

먼저 선형회귀를 계산하고, 그 다음에 시그모이드 함수에 대입하는 과정으로 나눈 것이다. 이러한 노드들이 여러개 모인 것이 하나의 신경층이다. 즉, 첫 번쨰 노드와 두 번째 노드에서는 다음과 같은 계산이 진행된다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/첫 번째 노드 계산.jpg"
       style="width: 50%; height: auto; margin:10px">
</figure>
<br/>
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/두 번째 노드 계산.jpg"
       style="width: 50%; height: auto; margin:10px">
</figure>
<br/>

만약 이 과정을 프로그래밍 한다면 반복문을 사용하는 것이 가장 단순한 방법일 것이다. 그러나 우리는 앞에서 **벡터화**의 유용성을 보았다. 4개의 노드에서 진행되는 다음과 같은 계산 과정을 벡터화 할 것이다.

$$z_1^{[1]} = w_1^{[1]T}x + b_1^{[1]}, \; a_1^{[1]} = \sigma(z_1^{[1]})$$

$$z_2^{[1]} = w_2^{[1]T}x + b_2^{[1]}, \; a_2^{[1]} = \sigma(z_2^{[1]})$$

$$z_3^{[1]} = w_3^{[1]T}x + b_3^{[1]}, \; a_3^{[1]} = \sigma(z_3^{[1]})$$

$$z_4^{[1]} = w_4^{[1]T}x + b_4^{[1]}, \; a_4^{[1]} = \sigma(z_4^{[1]})$$

방법은 앞선 강에서 본 것과 동일하다. w를 행렬 W로, x를 벡터로 묶으면 된다.

$$ z^{[1]} = \begin{bmatrix} - & w_1^{[1]T} & - \\ - & w_2^{[1]T} & -\\- & w_3^{[1]T} & - \\ - & w_4^{[1]T} & - \end{bmatrix} \begin{bmatrix}x_1\\x_2\\x_3\end{bmatrix} + \begin{bmatrix}b_1^{[1]}\\b_2^{[1]}\\b_3^{[1]}\\b_4^{[1]}\end{bmatrix} = \begin{bmatrix} w_1^{[1]T}x + b_1^{[1]}\\ w_2^{[1]T}x + b_2^{[1]}\\w_3^{[1]T}x + b_3^{[1]}\\ w_4^{[1]T}x + b_4^{[1]} \end{bmatrix} = \begin{bmatrix}z_1^{[1]}\\z_2^{[1]}\\z_3^{[1]}\\z_4^{[1]}\end{bmatrix}$$

결과로 얻은 z를 시그모이드 함수에 적용하면 $a^{[1]}$을 얻을 수 있다.

따라서 다음과 같은 신경망에 벡터화를 적용하면 반복문이 필요하지 않다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/신경망 예시.jpg"
       style="width: 70%; height: auto; margin:10px">
</figure>
<br/>

계산 과정:
$$z^{[1]} = W^{[1]}a^{[0]} + b^{[1]} \\ a^{[1]} = \sigma(z^{[1]}) \\ z^{[2]} = W^{[2]}a^{[1]} + b^{[2]} \\ a^{[2]} = \sigma(z^{[2]})$$


<br/>

## 여러 개의 훈련데이터에 벡터화
훈련데이터가 m개라면 어떻게 할까? 아직 벡터화가 익숙치 않다면 다시 위에서 본 마지막 과정을 m번 반복할 생각을 하고 있을 것이다.~~인간은 쉽게 바뀌지 않는다~~ 다시 말하지만, **벡터화**가 유용하다.

매우 쉽다. x를 벡터로 묶었다면 이번에는 행렬로 묶으면 된다. 다음처럼 말이다.
$$X = \begin{bmatrix}| & | & & |\\ x^{(1)} & x^{(2)} & \cdots & x^{(m)}\\| & | & & |\end{bmatrix}$$

위 식에 똑같이 넣고 계산하면 다음과 같은 결과들이 나온다.

$$Z^{[1]} = \begin{bmatrix}| & | & & |\\ z^{[1](1)} & z^{[1](2)} & \cdots & z^{[1](m)}\\| & | & & |\end{bmatrix}$$

$$A^{[1]} = \begin{bmatrix}| & | & & |\\ a^{[1](1)} & a^{[1](2)} & \cdots & a^{[1](m)}\\| & | & & |\end{bmatrix}$$

가로 개수는 훈련 데이터의 개수, 세로는 은닉층 노드의 개수를 뜻한다.

<br/>

m개의 훈련데이터에 대한 벡터화를 이용한 계산 과정을 살펴보자.

$$Z^{[1]} = W^{[1]}A^{[0]} + b^{[1]} \\ A^{[1]} = \sigma(Z^{[1]}) \\ Z^{[2]} = W^{[2]}A^{[1]} + b^{[2]} \\ A^{[2]} = \sigma(Z^{[2]})$$

<br/>

## 여러가지 활성화 함수
지금까지는 계산의 마지막에 시그모이드 함수를 사용했지만 사실 교수님은 시그모이드 함수를 거의 사용하지 않는다고 한다. ~~뭐지~~

시그모이드 함수 대신 사용하는 함수는 **tanh** 함수이다. tanh 함수 다음과 같다.
$$a = \tanh{z} = \frac{e^z - e^{-z}}{e^z + e^{-z}}$$

tanh 함수는 원점을 중심으로 대칭이며, 원점을 지난다. 따라서 0.5를 기준으로 대칭이었던 시그모이드 함수와는 다르게 데이터들의 평균값을 0에 가깝게 조정할 수 있다는 장점이 있다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/tanh 함수.jpg"
       style="width: 50%; height: auto; margin:10px">
</figure>
<br/>

보편적으로는 시그모이드 함수 대신 tanh 함수를 더 많이 사용한다. 그러나 마지막 결과층을 도출할 때 한해서 시그모이드 함수를 주로 사용하는데, $y$가 0 또는 1 인 경우 $\hat{y}$ 역시 0과 1 사이인 것이 계산에 용이하기 때문이다.

그러나 시그모이드 함수와 tanh 함수 모두 단점이 있다. 바로 z값이 매우 크거나 매우 작으면 그 지점에서의 기울기가 감소하고, 이로 인해 경사하강법이 느려진다는 것이다. 이를 보완하기 위해 **ReLU 함수**를 사용한다.

ReLU 함수는 다음과 같이 생겼다. 
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/ReLU 함수.jpg"
       style="width: 50%; height: auto; margin:10px">
</figure>
<br/>

표기는 $a = max(0, z)$ 이다. 0과 z 중에 더 큰 값을 함숫값으로 한다는 뜻이다.

ReLU 함수는 원점에서 미분이 불가능하다. 따라서 원점에서는 경사하강법을 적용할 수 없다. 그러나 z가 0이 되는 경우는 극히 드물기 때문에 큰 문제 없이 널리 사용된다. 0보다 작은 구간에서 도함수가 0인 것을 보완하기 위한 **Leaky ReLU**($a = max(0.01z, z)$) 함수도 있다.

<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/Deep Learning Specialization/Leaky ReLU 함수.jpg"
       style="width: 50%; height: auto; margin:10px">
</figure>
<br/>

<br/>
<br/>

*별도의 출처가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*