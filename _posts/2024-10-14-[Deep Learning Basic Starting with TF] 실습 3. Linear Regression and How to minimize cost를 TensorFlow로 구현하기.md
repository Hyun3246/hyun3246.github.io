---
title:  "[Deep Learning Basic Starting with TF] 실습 3. Linear Regression and How to minimize cost를 TensorFlow로 구현하기"
excerpt: "numpy와 tensorlow를 이용한 경사 하강법 구현"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 선형 회귀, 비용함수, 경사 하강법, numpy, tensorflow]

use_math: true
toc: true
toc_sticky: true

date: 2024-10-14
last_modified_at: 2024-10-14

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## 비용함수(Tensorflow 미사용)
Tensorflow를 사용하지 않고 비용함수를 구현해보자.

```python
X = np.array([1, 2, 3])
Y = np.array([1, 2, 3])

def cost_func(W, X, Y):
    c = 0
    for i in range(len(X)):
        c += (W * X[i] - Y[i]) ** 2
    return c / len(X)
```

매우 간단하다. 다음 코드로 W 값에 따른 비용함수 값을 구할 수 있다.

```python
for feed_W in np.linspace(-3, 5, num=15):
    curr_cost = cost_func(feed_W, X, Y)
```

<br/>

## 경사하강법(Tensorflow 사용)
Tensorflow에서 경사하강법을 구현한 방식은 다음과 같이 정리할 수 있다.

1. 가설함수 정의
2. 비용함수 정의
3. 학습률 정의
4. 경사(Gradient) 구하기
5. 하강(Descent) 구하기
6. W 업데이트

```python
for step in range(1000):
    hypothesis = W * X      # 1
    cost = tf.reduce_mean(tf.square(hypothesis - Y))        # 2

    alpha = 0.01        # 3
    gradient = tf.reduce_mean(tf.math.multiply(tf.math.multiply(W, X) - Y, X))      # 4
    descent = W - tf.math.multiply(alpha, gradient)     # 5
    W.assign(descent)       # 6
```

`tf.math.multiply`를 사용하면 vector의 elementwise 계산을 수행한다.

[코드 보러가기](https://github.com/Hyun3246/Code-Warehouse/blob/457b94e3fe8bfb3e0ffceffafed0ec0bb199febc/Deep%20Learning%20Basic%20Starting%20with%20TF/%EC%8B%A4%EC%8A%B5_3_Linear_Regression_and_How_to_minimize_cost%EB%A5%BC_TensorFlow%EB%A1%9C_%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0.ipynb)

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*
