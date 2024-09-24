---
title:  "[Deep Learning Specialization - 2단계] 8. 프로그래밍 프레임워크 소개"
excerpt: "딥러닝 프레임워크와 Tensorflow 구현"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 경사하강법, 프레임워크, Python, Tensorflow]

use_math: true
toc: true
toc_sticky: true
 
date: 2023-07-23
last_modified_at: 2023-08-05

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/andrew ng 2.png
---
## 딥러닝 프레임워크
딥러닝을 직접 코드로 구현할 때는 딥러닝 프레임워크를 사용하면 유용하다. <font color='#F5F5F7'>정방향 전파만 잘 구현해놓으면 역방향 전파를 별도의 계산 없이 바로 알 수 있기 때문</font>이다. 이외에도 딥러닝 프레임워크에는 유용한 기능이 많다.

대표적인 딥러닝 프레임워크는 다음과 같다.

- Caffe/Caffe2
- CNTK
- DL4J
- Keras
- Lasagne
- mxnet
- PaddlePaddle
- Tensorflow
- Theano
- Torch

이처럼 많은 프레임워크 중에 좋은 것은 다음과 같은 기준을 만족해야 한다.

1. 프로그래밍이 쉬워야 한다.
2. 빠르게 구동되어야 한다.
3. 장기적으로 오픈소스여야 한다. (회사가 성장하고 이용자가 늘어도.)

<br/>

## Tensorflow 사용해보기
$$J(w) = w^2 -10w + 25$$

위와 같은 간단한 비용함수를 Tensorflow로 구현해보자.

```python
import numpy as np
import tensorflow as tf

coefficients = np.array([[1], [-10], [25]])

w = tf.Variable([0], dtype = tf.float32)
x = tf.placeholder(tf.float32, [3, 1])
cost = x[0][0]*w**2 + x[1][0]*w + x[2][0]
train = tf.train.GradientDescentOptimizer(0.01).minimize(cost)

init = tf.global_variables_initializer()
session = tf.Session()
session.run(init)
print(session.run(w))

for i in range(1000):
    session.run(train, feed_dict={x:coefficients})

print(session.run(w))
```

코드를 분해해보자.

`w`는 최적화하고자 하는 매개변수이다. `cost`는 비용함수를 정의한 것이다.

```python
train = tf.train.GradientDescentOptimizer(0.01).minimize(cost)
```

위 코드는 경사하강법을 구현한 것이다. 학습속도를 0.01로 하고, 비용함수를 최소화하겠다는 뜻이다.

```python
init = tf.global_variables_initializer()
session = tf.Session()
session.run(init)
print(session.run(w))
```

이 부분은 학습 알고리즘을 실행하는 관용적인 부분이다. 여기까지는 경사하강법을 아직 반복 진행하지 않았기 때문에, w의 값이 초기 값(0)이 도출된다.

```python
for i in range(1000):
    session.run(train, feed_dict={x:coefficients})

print(session.run(w))
```

위 과정은 경사하강법은 1000회 반복하는 과정이다. 이 과정을 거치면 w가 비용함수를 최소화하도록 조정된다.

추가적으로 `x`는 학습 데이터이다. `placeholder`는 변수를 선언하기는 하지만, <font color='#F5F5F7'>그 값은 나중에 전달한다</font>는 의미이다. 여기서는 `coefficients`가 학습 데이터가 되는 셈이며, `for` 반복문의 `feed_dict`에서 `x`에 학습 데이터가 전달되는 것을 확인할 수 있다.

참고로, 관용적이라고 언급했던 코드 4줄은 다음과 같이 쓸 수도 있다.
```python
with tf.Session() as session:
    session.run(init)
    print(session.run(w))
```
