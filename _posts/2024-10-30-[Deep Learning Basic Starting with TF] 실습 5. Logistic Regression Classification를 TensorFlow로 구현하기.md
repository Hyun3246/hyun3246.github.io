---
title:  "[Deep Learning Basic Starting with TF] 실습 5. Logistic Regression/Classification를 TensorFlow로 구현하기"
excerpt: "텐서플로를 이용한 로지스틱 회귀 구현"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 로지스틱 회귀, 비용함수]

use_math: true
toc: true
toc_sticky: true

date: 2024-10-30
last_modified_at: 2024-10-30

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## 로지스틱 함수 구현
로지스틱 함수는 텐서플로를 사용해서 다음과 같이 구현한다.

```python
def logistic_regression(features):
    hypothesis = tf.divide(1., 1. + tf.exp(tf.matmul(features, W) + b))
    return hypothesis
```

<br/>

## 로지스틱 회귀 비용함수 구현
로지스틱 회귀에서의 비용함수는 다음과 같이 구현할 수 있다.

```python
def loss_fn(hypothesis, features, labels):
    cost = -tf.reduce_mean(labels * tf.math.log(logistic_regression(features)) + (1 - labels) * tf.math.log(1 - hypothesis))
    return cost

```

여기서 `hypothesis`는 가설함수 자체를 의미하며, 따라서 가설함수는 미리 설졍되어 있어야 한다. 여기서는 앞서 코딩한 `logistic_regresison()`함수가 가설함수가 된다. `features`는 x값을, `labels`는 정답인 y를 의미한다.

<br/>

## 분류 및 분류 정확도 측정
특정한 기준을 설정해서 분류하고 이를 평가하는 코드는 다음과 같다.

```python
def accuracy_fn(hypothesis, labels):
    predicted = tf.cast(hypothesis > 0.5, dtype=tf.float32)
    accuracy = tf.reduce_mean(tf.cast(tf.equal(predicted, labels), dtype=tf.int32))
    return accuracy
```

`tf.cast()`는 결과 값을 다른 형태로 바꾸는(캐스팅) 역할을 한다. `tf.equal()` 함수는 두 값이 같으면 True, 같지 않다면 False를 출력한다.

[코드 보러가기](https://github.com/Hyun3246/Code-Warehouse/blob/457b94e3fe8bfb3e0ffceffafed0ec0bb199febc/Deep%20Learning%20Basic%20Starting%20with%20TF/%EC%8B%A4%EC%8A%B5_5_Logistic_Regression_Classification%EB%A5%BC_TensorFlow%EB%A1%9C_%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0.ipynb)

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*