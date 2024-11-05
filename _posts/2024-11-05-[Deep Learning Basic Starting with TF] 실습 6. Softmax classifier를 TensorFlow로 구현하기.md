---
title:  "[Deep Learning Basic Starting with TF] 실습 6. Softmax classifier를 TensorFlow로 구현하기"
excerpt: "Tensorflow로 softmax 구현하기"

categories:
  - Data Science & ML
tags:
  - [머신러닝, softmax, 비용함수]

use_math: true
toc: true
toc_sticky: true

date: 2024-11-05
last_modified_at: 2024-11-05

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## Softmax 함수를 tensorflow로 구현하기
Logit 함수가 정의되어 있다고 가정할 때, tensorflow를 이용해 softmax 함수를 구현하는 것은 간단하다.

```python
def hypothesis(X):
    return tf.nn.softmax(logit_fn(X))
```

<br/>

## 비용함수 정의하기
Cross-entropy를 이용한 비용함수는 다음과 같이 코딩할 수 있다.

```python
def cost_fn(X, Y):
    logits = logit_fn(X)
    cost_i = tf.keras.losses.categorical_crossentropy(y_true=Y, y_pred=logits, from_logits=True)
    cost = tf.reduce_mean(cost_i)
    return cost
```

`tf.keras.losses.categorical_crossentropy()`만 사용하면 된다. 인자 중에 `from_logits`라는 것이 있는데, 출력 배열의 값이 문제에 맞게 normalize 되었는지 여부이다. 쉽게 생각해서, 계산 과정에 softmax를 사용하고 싶으면 `from_logits = True`로 해준다.

[from_logits에 대한 자세한 설명](https://hwiyong.tistory.com/335)

<br/>

[전체 코드 보러가기 1](https://github.com/Hyun3246/Code-Warehouse/blob/c839f3525d6bbd5e862c275ae361457828f09b50/Deep%20Learning%20Basic%20Starting%20with%20TF/%EC%8B%A4%EC%8A%B5_6_1_Softmax_classifier%EB%A5%BC_TensorFlow%EB%A1%9C_%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0.ipynb)

[전체 코드 보러가기 2](https://github.com/Hyun3246/Code-Warehouse/blob/c839f3525d6bbd5e862c275ae361457828f09b50/Deep%20Learning%20Basic%20Starting%20with%20TF/%EC%8B%A4%EC%8A%B5_6_2_Fancy_Softmax_classifier%EB%A5%BC_TensorFlow%EB%A1%9C_%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0.ipynb)

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*