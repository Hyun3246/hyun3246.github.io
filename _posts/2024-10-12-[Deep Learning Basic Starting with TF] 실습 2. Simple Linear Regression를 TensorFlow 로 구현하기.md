---
title:  "[Deep Learning Basic Starting with TF] 실습 2. Simple Linear Regression를 TensorFlow 로 구현하기"
excerpt: "단순 선형 회귀 구현하기"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 선형 회귀, 비용함수, 경사하강법]

use_math: true
toc: true
toc_sticky: true

date: 2024-10-12
last_modified_at: 2024-10-12

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## 경사하강법 구현 과정
```python
# 학습률 정의
learning_rate = 0.01

# 본격적인 경사하강법
for i in range(1000):
    with tf.GradientTape() as tape:
        hypothesis = W * x_data + b
        cost = tf.reduce_mean(tf.square(hypothesis - y_data))

    W_grad, b_grad = tape.gradient(cost, [W, b])

    W.assign_sub(learning_rate * W_grad)    # 모델 파라미터 업데이트
    b.assign_sub(learning_rate * b_grad)    # 모델 파라미터 업데이트

    if i % 10 == 0:
        print('{:5} | {:10.4} | {:10.4} | {:10.6f}'.format(i, W.numpy(), b.numpy(), cost))
```

`tape`에 기록을 하는 개념이라고 생각하면 된다. 

`assign_sub`는 파이썬에서의 `a -= b` 연산과 동일하다.

마지막에는 중간 계산 과정을 보여주기 위해 10번마다 파라미터를 출력하도록 했다.

[코드 보러가기](https://github.com/Hyun3246/Code-Warehouse/blob/4dcf95962fd8386df835cc5f1a26618fb0423e2e/Deep%20Learning%20Basic%20Starting%20with%20TF/%EC%8B%A4%EC%8A%B5_2_Simple_Linear_Regression%EB%A5%BC_TensorFlow_%EB%A1%9C_%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0.ipynb)

