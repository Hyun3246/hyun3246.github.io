---
title:  "[Deep Learning Basic Starting with TF] 실습 7-1. Application & Tips: 학습률(Learning Rate)과 데이터 전처리(Data Preprocessing)"
excerpt: "학습 스케줄링과 특성 스케일링, 잡음 처리"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 학습률, 데이터 전처리]

use_math: true
toc: true
toc_sticky: true

date: 2024-11-07
last_modified_at: 2024-11-07

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## Learing rate decay
Learning rate decay의 개념은 아래 링크를 참고하자. 여기서는 텐서플로로 구현하는 방법만 살펴본다.

[학습 스케줄링](https://hyun3246.github.io/data%20science%20&%20ml/Hands-On-ML-4%EC%9E%A5.-%EB%AA%A8%EB%8D%B8-%ED%9B%88%EB%A0%A8-1/#%ED%99%95%EB%A5%A0%EC%A0%81-%EA%B2%BD%EC%82%AC-%ED%95%98%EA%B0%95%EB%B2%95)

```python
is_decay = True     # learning_rate decay를 사용
starter_learning_rate = 0.1     # 최초의 learning rate

# is_decay 여부에 따라 학습 스케줄링 여부가 달라짐.
if(is_decay):
    learning_rate = tf.keras.optimizers.schedules.ExponentialDecay(initial_learning_rate=starter_learning_rate,
                                                                   decay_steps=1000,
                                                                   decay_rate=0.96,
                                                                   staircase=True)
    optimizer = tf.keras.optimizers.SGD(learning_rate)

else:
    optimizer = tf.keras.optimizers.SGD(learning_rate=starter_learning_rate)     
```

`tf.keras.optimizers.schedules.ExponentialDecay()`를 사용하면 계속 같은 비율로 학습률을 감소시켜 준다. `staircase=True`로 설정하면 `decay_steps`까지는 학습률을 감소시키지 않다가, 그 이후부터 감소시키기 시작한다.

<br/>

# 특성 스케일링
아래 링크를 참고하자.

[Python for ML 1](https://hyun3246.github.io/data%20science%20&%20ml/Hands-On-ML-2%EC%9E%A5.-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%B2%98%EC%9D%8C%EB%B6%80%ED%84%B0-%EB%81%9D%EA%B9%8C%EC%A7%80-2/#%ED%8A%B9%EC%84%B1-%EC%8A%A4%EC%BC%80%EC%9D%BC%EB%A7%81)

[Python for ML 2](https://hyun3246.github.io/data%20science%20&%20ml/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D%EC%9D%84-%EC%9C%84%ED%95%9C-%ED%8C%8C%EC%9D%B4%EC%8D%AC-16.-Linear-Regression-5/#%ED%95%99%EC%8A%B5%EB%A5%A0-%EA%B0%90%EC%86%8C)

[Hands-On ML](https://hyun3246.github.io/data%20science%20&%20ml/Hands-On-ML-2%EC%9E%A5.-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%B2%98%EC%9D%8C%EB%B6%80%ED%84%B0-%EB%81%9D%EA%B9%8C%EC%A7%80-2/#%ED%8A%B9%EC%84%B1-%EC%8A%A4%EC%BC%80%EC%9D%BC%EB%A7%81)

<br/>

## 잡음 처리
잡음을 처리하면 데이터 분석을 더 효과적으로 할 수 있다. 예를 들어 다음과 같은 인물의 얼굴을 인식한다고 해보자.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/잡음 처리 전 후.png"
       style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

왼쪽의 머리 전부를 사용한다면 그만큼 효율이 떨어질 것이다. 오른쪽처럼 얼굴 부분만 확대하여 학습에 사용해야 더 효율적으로 학습을 할 수 있다.

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*
