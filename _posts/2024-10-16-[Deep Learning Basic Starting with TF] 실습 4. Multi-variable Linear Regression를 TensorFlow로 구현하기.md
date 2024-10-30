---
title:  "[Deep Learning Basic Starting with TF] 실습 4. Multi-variable Linear Regression를 TensorFlow로 구현하기"
excerpt: "Matrix를 사용하여 선형 회귀 구현하기"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 선형 회귀, 텐서플로]

use_math: true
toc: true
toc_sticky: true

date: 2024-10-16
last_modified_at: 2024-10-16

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## Matrix 미사용 코드
Matrix를 사용하지 않은 코드는 이전과 크게 다르지 않다.

```python
x1 = [ 73.,  93.,  89.,  96.,  73.]
x2 = [ 80.,  88.,  91.,  98.,  66.]
x3 = [ 75.,  93.,  90., 100.,  70.]
Y  = [152., 185., 180., 196., 142.]

w1 = tf.Variable(tf.random.normal([1]))
w2 = tf.Variable(tf.random.normal([1]))
w3 = tf.Variable(tf.random.normal([1]))
b  = tf.Variable(tf.random.normal([1]))

learning_rate = 0.000001

for i in range(1000 + 1):
    with tf.GradientTape() as tape:
        hypothesis = w1 * x1 + w2 * x2 + w3 * x3 + b
        cost = tf.reduce_mean(tf.square(hypothesis - Y))

    w1_grad, w2_grad, w3_grad, b_grad = tape.gradient(cost, [w1, w2, w3, b])

    w1.assign_sub(learning_rate * w1_grad)
    w2.assign_sub(learning_rate * w2_grad)
    w3.assign_sub(learning_rate * w3_grad)
    b.assign_sub(learning_rate * b_grad)

    if i % 50 == 0:
        print("{:5} | {:12.4f}".format(i, cost.numpy()))

```

<br/>

## Matrix 사용 코드
Matrix를 사용한 코드에서 눈여겨 볼(비교해 볼) 포인트는 다음과 같다.

1. 데이터를 작성하는 방식이 matrix로 변경되었다. 이에 따라 X와 y를 표현하는 방식도 바뀌었다.
2. W와 b를 최초 지정하는 방식이 간단해졌다.
3. 가설함수를 설정하는 과정에서 행렬 곱 `tf.matmul()`이 사용되었다.
4. W와 b를 업데이트 하는 방식이 간단해졌다.

```python
import numpy as np

data = np.array([
    # X1,   X2,    X3,   y
    [ 73.,  80.,  75., 152. ],
    [ 93.,  88.,  93., 185. ],
    [ 89.,  91.,  90., 180. ],
    [ 96.,  98., 100., 196. ],
    [ 73.,  66.,  70., 142. ]
], dtype=np.float32)

X = data[:, :-1]
y = data[:, [-1]]

W = tf.Variable(tf.random.normal([3, 1]))
b = tf.Variable(tf.random.normal([1]))

learning_rate = 0.000001

def predict(X):
    return tf.matmul(X, W) + b

n_epochs = 2000

for i in range(n_epochs + 1):
    with tf.GradientTape() as tape:
        cost = tf.reduce_mean((tf.square(predict(X) - y)))

    W_grad, b_grad = tape.gradient(cost, [W, b])

    W.assign_sub(learning_rate * W_grad)
    b.assign_sub(learning_rate * b_grad)

    if i % 100 == 0:
        print("{:5} | {:10.4f}".format(i, cost.numpy()))
     
```

[코드 보러가기](https://github.com/Hyun3246/Code-Warehouse/blob/457b94e3fe8bfb3e0ffceffafed0ec0bb199febc/Deep%20Learning%20Basic%20Starting%20with%20TF/%EC%8B%A4%EC%8A%B5_4_Multi_variable_Linear_Regression%EB%A5%BC_TensorFlow%EB%A1%9C_%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0.ipynb)

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*
