---
title:  "[Deep Learning Basic Starting with TF] 9-2. 딥넷트웍 학습 시키기 (backpropagation)"
excerpt: "Backpropagation"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 텐서플로]

use_math: true
toc: true
toc_sticky: true

date: 2024-11-15
last_modified_at: 2024-11-15

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## Backpropagation

[Deep Learning Specialization 1](https://hyun3246.github.io/data%20science%20&%20ml/Deep-Learning-Specialization-1%EB%8B%A8%EA%B3%84-4.-%EC%96%95%EC%9D%80-%EC%8B%A0%EA%B2%BD%EB%A7%9D-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/)

[Deep Learning Specialization 2](https://hyun3246.github.io/data%20science%20&%20ml/Deep-Learning-Specialization-1%EB%8B%A8%EA%B3%84-5.-%EC%8B%AC%EC%B8%B5-%EC%8B%A0%EA%B2%BD%EB%A7%9D-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/)

텐서플로에서는 텐서보드(TensorBoard)를 활용하면 forward propagation과 backpropagation의 과정을 시각적으로 확인할 수 있다.

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*