---
title:  "[Deep Learning Specialization - 1단계] 3. 파이썬과 벡터화"
excerpt: "벡터화를 통한 반복문 없애기"

categories:
  - Data Science
tags:
  - [Data Science, 머신러닝, 로지스틱 회귀, 경사하강법, 벡터화, Python]

use_math: true
toc: true
toc_sticky: true
 
date: 2023-03-03
last_modified_at: 2023-03-06

header:
  overlay_image: /image/overlay image/andrew ng 1.png
---

## 벡터화
벡터화는 '벡터로 만든다'는 말이다. 데이터를 벡터로 만들면 반복문을 돌면서 계산할 필요 없이 행렬곱, 벡터곱 등을 이용해 편하게 계산할 수 있다. 예를 들어 $z=w^Tx+b \, (w \in R^{n_x}, x \in R^{n_x})$ 와 같은 선형회귀 식을 반복문을 이용해 계산하면 다음과 같다.

```
# Non-vectorized
z = 0
for i in range(n_x):
    z += w[i] * x[i]
z += b
```

그러나 w와 x를 벡터로 만든다면 벡터곱(내적) 한 번으로 계산이 끝난다. (파이썬에서는 `numpy`를 이용해 벡터, 행렬과 관련된 각종 연산을 쉽게 수행할 수 있다.)

```
# Vectorized
z = np.dot(w, x) + b
```
`np.dot(w, x)` 부분이 $w^Tx$ 를 계산하는 부분이다.

SIMD(Single Instruction Multiple Data)는 하나의 명령어로 여러 개의 계산을 병렬적으로 수행하는 것을 의미한다. 파이썬의 `numpy`는 GPU와 CPU 모두에서 이러한 계산을 가능하게 하며, 대부분의 경우 단순 반복문보다 훨씬 빠르다.

<br/>

## 벡터화의 다른 예시들
벡터화는 반복문의 사용을 피할 때 유용하게 활용될 수 있다.

행렬과 벡터의 곱을 계산하는 과정을 생각해보자. 

$$u = Av$$

A는 행렬이고 u, v는 벡터이다. 행렬의 곱 공식은 다음과 같다.

$$ \displaystyle u_i = \sum_{i}^{}{}\sum_{j}^{}{A_{ij}v_j}$$

파이썬 반복문 공부를 처음 시작하면 행렬의 곱 예제를 많이 경험하게 된다. 보통은 다음과 같은 방식으로 구한다.
```
# 반복문을 사용한 행렬의 곱
u = np.zeros((n, 1))
for i ...
    for j ...
        u[i] += A[i][j] *v[j]
```
먼저 비어있는 결과 행렬 `u`를 만들고, 계산 결과가 나오면 `u`의 요소들을 하나씩 바꾸는 과정이다. 이중 반복문을 사용해야하는 매우 복잡한 과정이지만, 벡터화를 사용하면 한 줄로 끝난다.
```
# 벡터화를 사용한 행렬의 곱
u = np.dot(A, v)
```
계산은 컴퓨터가 하신다.


다른 예시로는 거듭제곱을 구하는 것이 있다. 다음과 같은 v를 이용해 u를 구하고 싶다고 해보자.

$$v = \begin{bmatrix}v_1\\v_2\\...\\v_n \end{bmatrix}$$

$$u = \begin{bmatrix}e^{v_1}\\e^{v_2}\\...\\e^{v_n} \end{bmatrix}$$

벡터화 사용 여부로 코드를 비교해보자.
```
# 반복문을 사용한 거듭제곱
u = np.zeros((n, 1))
for i in range(n):
    u[i] = math.exp(v[i])
```
```
# 벡터화를 사용한 거듭제곱
u = np.exp(v)
```

이외에도 `numpy`는 매우 유용한 기능을 많이 제공한다. 속도도 매우 빠르다!

이제 로지스틱 회귀에서 경사하강법을 사용하기 위해 미분계수를 구하는 과정으로 넘어가자. 우리는 지난 강의에서 아래와 같은 코드를 보았다.
```
J = 0; dw1 = 0; dw2 = 0; db = 0

for i = 1 to m
    z(i) = w^T * x(i) + b
    a(i) = sigmoid(z(i))
    J += -[y(i)log(a(i)) + (1 - y(i))log(1-a(i))]
    dz(i) = a(i) - y(i)

    # n개의 특성에 대해 다시 반복해야하는 부분
    dw1 += x1(i)dz(i)
    dw2 += x2(i)dz(i)
    db += dz(i)

    J /= m
    dw1 /= m
    dw2 /= m
    db /= m
```

dw를 벡터화하면 두 번째 반복 부분을 간소화할 수 있다. 

```
J = 0; dw = np.zeros(n_x, 1); db = 0

for i = 1 to m
    z(i) = w^T * x(i) + b
    a(i) = sigmoid(z(i))
    J += -[y(i)log(a(i)) + (1 - y(i))log(1-a(i))]

    dz(i) = a(i) - y(i)
    dw += x(i)dz(i)
    db += dz(i)

    J /= m
    dw1 /= m
    dw2 /= m
    db /= m
```
x와 dz의 연산을 벡터의 곱으로 한 번에 처리하는 것이다.

<br/>

## 로지스틱 회귀의 벡터화
로지스틱 회귀를 완전히 벡터화해보자. 벡터화를 위해 행렬을 준비해야 한다.
$$X = \begin{bmatrix}
| & | & & |\\ 
x^{(1)} & x^{(2)} & \cdots & x^{(m)}\\
| & | & & |
\end{bmatrix}$$

행렬 X는 $(n_x, m)$ 의 모양을 가지고 있다. 이 행렬을 $w^T$와 곱하고, b로 이루어진 $(1, m)$ 형태의 벡터와 더한다.

$$Z = \begin{bmatrix}z^{(1)} & z^{(2)} & \cdots & z^{(m)} \end{bmatrix} = w^TX + \begin{bmatrix}b & b & \cdots & b \end{bmatrix}$$

위 과정을 파이썬 코드로 나타내면 다음과 같다.
```
Z = np.dot(w.T,x) + b       # w.T는 w의 transpose
```
위 코드에서 b는 하나의 수이다. 그러나 계산 과정에서는 벡터로 바뀌어 계산되어야 한다. 파이썬은 계산과정에서 숫자 b를 자동으로 벡터로 변환하는 broadcasting을 지원한다.

위에서 구한 Z를 시그모이드 함수에 대입하면 최종적으로 원하는 결과인 A를 구할 수 있다.

<br/>

## 경사하강법의 벡터화
벡터화를 적용한 경사하강법 코드를 완성해보자.

$dz = a - y$ 였으므로, $dZ = A - Y = \begin{bmatrix}a^{(1)} - y^{(1)} & a^{(2)} - y^{(2)} & \cdots \end{bmatrix}$ 로 나타낼 수 있다.

손실함수에서 db는 dz였고, 비용함수에서는 이를 m으로 나눈 것이었다. 

$$\displaystyle db = \frac{1}{m}\sum_{i=1}^{m}{dz^{(i)}}$$

코드로 구현하면 다음과 같다.
```
db = 1/m * np.sum(dZ)
```

dw는 X와 dZ를 곱해 m으로 나눈 것이다. 계산 과정은 다음과 같다.

$$dw = \frac{1}{m} \begin{bmatrix}x^{(1)}dz^{(1)} + \cdots + x^{(m)}dz^{(m)}\end{bmatrix} \\
= \frac{1}{m} \begin{bmatrix}| & | & & |\\ x^{(1)} & x^{(2)} & \cdots & x^{(m)}\\| & | & & |\end{bmatrix} \begin{bmatrix}dz^{(1)}\\\vdots\\dv^{(m)} \end{bmatrix} \\
= \frac{1}{m} X dZ^T$$

이제 경사하강법의 한 단계를 반복문을 사용하지 않고도 나타낼 수 있다!
```
Z = np.dot(w.T, X) + b          # w.T는 w의 transpose
A = sigmoid(Z)
dZ = A - Y
dw = 1/m * X dZ.T               # dZ.T는 dZ의 transpose
db = 1/m * np.sum(dZ)

w = w - learning_rate * dw
b = b - learning_rate * db
```
`numpy`를 이용한 계산은 반복문보다 5배 정도 빠르다. 1초와 5초의 차이라면 얼마 안된다고 느낄 수도 있지만, 1시간이 걸릴 계산이 5시간, 1개월이 걸릴 계산이 5개월 걸린다면 그 차이는 어마어마할 것이다.

<br/>

## 파이썬의 broadcasting
앞서 broadcasting을 언급하였다. 여기서는 broadcasting에 대해 더 깊이 알아본다.

다음과 같은 행렬이 있다고 하자.
$$A = \begin{bmatrix}
56.0 & 0.0 & 4.4 & 68.0\\ 
1.2 & 104.0 & 52.0 & 8.0\\
1.8 & 135.0 & 99.0 & 0.9
\end{bmatrix}$$

우리가 원하는 것은 각 열마다 요소들이 차지하는 비율을 계산하는 것이다. 먼저 각 열별로 총합을 구한 뒤, 이를 요소별로 나누는 것을 생각해볼 수 있다.

```python
cal = A.sum(axis = 0)
percentage = 100 * A / cal.reshape(1, 4)
```

(사실 `cal`은 그 자체로 (1, 4)의 형태이기 때문에 다시 `reshape`을 할 필요가 없다. 그러나 돌다리도 두들겨 보고 건너는 것 태도가 중요하다.)

행렬 A는 (3, 4)이고, `cal`은 (1, 4)이기 때문에 원래대로라면 위와 같은 계싼은 불가능하다. 하지만 파이썬은 broadcasting 개념을 사용해 `cal`의 행을 3개로 복제하여 나눗셈을 수행한다.

이처럼 모자라는 행이나 열을 복제하여 행렬 사이의 연산이 가능하도록 해주는 것을 boradcasting이라고 한다. 일반화를 하면, (m, n) 행렬과 (1, n) 행렬을 연산할 때는 (1, n) 행렬의 행이 복제되어 (m, n) 행렬로 바뀌고, 연산을 진행한다. 반대로 (m, n) 행렬과 (m, 1) 행렬을 연산할 때는 (m, 1) 행렬의 열이 복제되어 (m, n) 행렬로 바뀌고 연산된다.

몇 가지 예시를 더 살펴보자. 다음은 broadcasting이 이루어질 떄의 연산이다.

$$\begin{bmatrix}1\\ 2\\3\\4\end{bmatrix} + 100 \rightarrow \begin{bmatrix}1\\ 2\\3\\4\end{bmatrix} + \begin{bmatrix}100\\ 100\\100\\100\end{bmatrix} = \begin{bmatrix}101\\ 102\\103\\104\end{bmatrix}$$

$$\begin{bmatrix}1 & 2 & 3\\ 4 & 5 & 6\end{bmatrix} + \begin{bmatrix}100 & 200 & 300\end{bmatrix} \rightarrow \begin{bmatrix}1 & 2 & 3\\ 4 & 5 & 6\end{bmatrix} + \begin{bmatrix}100 & 200 & 300\\100 & 200 & 300\end{bmatrix} = \begin{bmatrix}101 & 202 & 303\\104 & 205 & 306\end{bmatrix}$$

$$\begin{bmatrix}1 & 2 & 3\\ 4 & 5 & 6\end{bmatrix} + \begin{bmatrix}100\\200\end{bmatrix} \rightarrow \begin{bmatrix}1 & 2 & 3\\ 4 & 5 & 6\end{bmatrix} + \begin{bmatrix}100 & 100 & 100\\200 & 200 & 200\end{bmatrix} = \begin{bmatrix}101 & 102 & 103\\204 & 205 & 206\end{bmatrix}$$

> 파이썬으로 코딩할 떄의 TIP            
    1. Rank 1 array를 사용하지 말 것. 오류가 많이 발생함. 생성할 때는 (n, )가 아닌 (n, 1)로 생성.          
    2. `reshape`을 적극 사용할 것. 명시적인 행렬도 반드시 모양을 확실히 하라.       


<br/>

## 로지스틱 회귀와 비용함수 추가 설명
여기서는 로지스틱 회귀에서 사용되는 손실함수와 비용함수의 유도과정을 설명한다.

우리는 앞선 강의에서 로지스틱 회귀가 다음과 같은 조건부확률의 결과를 찾는 것이라고 하였다.

$$ \hat{y} = P(y=1|x)$$

이진분류이므로 y는 0이나 1의 값을 가질 수 있다.

If, $y = 1: P(y|x) = \hat{y}$            
If, $y = 0: P(y|x) = 1- \hat{y}$

이 두 가지 식은 하나로 합칠 수 있다.

$$ P(y|x) = \hat{y}^y(1-\hat{y})^{(1-y)}$$

위 식에 0과 1을 대입하면 앞선 두 가지 식이 완벽하게 도출되는 것을 확인할 수 있다.

합친 식에 $\log$를 취해서 정리할 수 있다. $\log$는 단조 증가 함수이므로, 양상을 파악하기에 용이하다.

$$ \log{P(y|x)} = \log{\hat{y}^y(1-\hat{y})^{(1-y)}} = y\log{\hat{y}} + (1-y)\log{(1-\hat{y})} = -L(\hat{y}, y)$$

손실함수에 음수를 취한 식이 도출된다. 손실함수를 최대한 작게하고 싶으면 $\log$를 최대화해야 한다는 결론에 이른다.

이제 m개의 훈련 데이터가 있을 때를 생각해보자. 각각이 독립동일분포일 때, 전체의 확률은 각 확률이 곱으로 구한다.

$$ P(labels\,in\,training\,set) = \prod_{i=1}^{m}{P(y^{(i)}|x^{(i)})}$$

여기에 또 $log$를 취해보자.

$$ \log{P(labels\,in\,training\,set)} = \sum_{i=1}^{m}{\log{P(y^{(i)}|x^{(i)})}} = -\sum_{i=1}^{m}{L(\hat{y}, y)}$$

최대 우도 추정을 적용해서 좌변을 최대화하는 값을 찾는 것이 관건이 된다.

$$ J(w, b) = \frac{1}{m}\sum_{i=1}^{m}{L(\hat{y}, y)}$$

이렇게 비용함수 식을 유도할 수 있다.