---
title:  "[Deep Learning Basic Starting with TF] 실습 7-2-1. Application & Tips: 오버피팅(Overfitting) & Solutions"
excerpt: "과대적합과 과소적합"

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
## Overfitting과 Underfitting
모델이 너무 training set에만 특화되어 있어서 test set과 실제 데이터를 제대로 반영하지 못하는 경우를 overfit(high variance)이라고 한다.

반대로 모델이 너무 단순해서 train set조차 제대로 대변하지 못하는 경우를 underfit(high bias)라고 한다.

자세한 사항은 아래 링크를 참고하자.

[Python for ML](https://hyun3246.github.io/data%20science%20&%20ml/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D%EC%9D%84-%EC%9C%84%ED%95%9C-%ED%8C%8C%EC%9D%B4%EC%8D%AC-16.-Linear-Regression-5/#%EA%B3%BC%EB%8C%80%EC%A0%81%ED%95%A9%EA%B3%BC-%EA%B7%9C%EC%A0%9C)

[Deep Learing Specialization](https://hyun3246.github.io/data%20science%20&%20ml/Deep-Learning-Specialization-2%EB%8B%A8%EA%B3%84-1.-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%EC%96%B4%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0/#%ED%8E%B8%ED%96%A5bias%EA%B3%BC-%EB%B6%84%EC%82%B0variance)


Overfitting을 해결하는 방법
1. 더 많은 training data 모으기
2. 특성 줄이기 (e.g. PCA)
3. 규제 설정하기

Underfitting을 해결하는 방법
1. 더 많은 특성 추가하기

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*