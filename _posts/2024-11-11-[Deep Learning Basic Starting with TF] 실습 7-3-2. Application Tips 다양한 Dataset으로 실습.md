---
title:  "[Deep Learning Basic Starting with TF] 실습 7-3-2. Application & Tips: 다양한 Dataset으로 실습"
excerpt: "keras로 신경망 구축하기"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 텐서플로, 케라스, 신경망]

use_math: true
toc: true
toc_sticky: true

date: 2024-11-11
last_modified_at: 2024-11-11

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
이번 강의에서는 3가지 dataset을 이용해서 신경망을 어떻게 학습시키는지를 실습하였다.
- MNIST: 손글씨 dataset
- fashion MNIST: 패션(의류) 관련 dataset
- IMDB: 영화 리뷰 dataset. 긍정적 리뷰인지 부정적 리뷰인지를 판별.

Dataset에 의미를 두어 학습하기보다는 keras를 이용해 신경망을 어떻게 구현하는지에 초점을 맞추었다.

keras를 이용해 신경망을 구축하는 코드는 다음과 같다.

```python
model = tf.keras.models.Sequential([
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(512, activation=tf.nn.relu),
    tf.keras.layers.Dropout(0.2),
    tf.keras.layers.Dense(10, activation=tf.nn.softmax)
])

model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])
```

먼저 `models.Sequential`에 사용할 layer의 종류를 차례대로 넣어준다.

다음으로는 `model.compile`에 모델에 사용할 손실 함수(`loss`), 최적화 방법(`optimizer`), 평가 지표(`metrics`)를 설정해준다.
- `optimizer`: `SGD`, `RMSprop`, `Adam` 등 최적화 알고리즘.
- `loss`: `mean_squared_error`, `binary_cross_entropy` 등.
- `metrics`: `mse`(회귀), `accuracy`, `precision`, `recall`, `f1-score` 등.

훈련과 평가 코드는 다음과 같다.

```python
model.fit(x_train, y_train, epochs=5)       # 훈련
model.evaluate(x_test, y_test)      # 평가

```

[코드 보러가기 1_MNIST](https://github.com/Hyun3246/Code-Warehouse/blob/7bbf8bc222d0c5eede062fb58486c78c6f4a65a8/Deep%20Learning%20Basic%20Starting%20with%20TF/%EC%8B%A4%EC%8A%B5_07_03_01_Application_%26_Tips_Data_%26_Learning.ipynb)
[코드 보러가기 2_Fashion MNIST & IMDB](https://github.com/Hyun3246/Code-Warehouse/blob/7bbf8bc222d0c5eede062fb58486c78c6f4a65a8/Deep%20Learning%20Basic%20Starting%20with%20TF/%EC%8B%A4%EC%8A%B5_07_03_02_Application_%26_Tips_%EB%8B%A4%EC%96%91%ED%95%9C_Dataset%EC%9C%BC%EB%A1%9C_%EC%8B%A4%EC%8A%B5.ipynb)

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*