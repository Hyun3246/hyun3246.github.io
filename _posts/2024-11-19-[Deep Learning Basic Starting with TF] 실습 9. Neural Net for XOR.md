---
title:  "[Deep Learning Basic Starting with TF] 실습 9. Neural Net for XOR"
excerpt: "신경망을 이용한 XOR 문제 해결, 텐서보드"

categories:
  - Data Science & ML
tags:
  - [머신러닝, 텐서플로]

use_math: true
toc: true
toc_sticky: true

date: 2024-11-19
last_modified_at: 2024-11-19

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/Deep Learning Basic Starting with TF.png
---
## Neural Network로 XOR 문제 해결
이번 실습에서는 신경망으로 이용해서 XOR 문제를 해결하는 것을 실습하였다. Logistic regression으로는 해결이 불가능하였지만, 심층 신경망을 활용하면 문제를 해결할 수 있었다.

3개 층 신경망은 다음과 같이 설계하였다.

```python
def neural_net(features):
    layer1 = tf.sigmoid(tf.matmul(features, W1) + b1)
    layer2 = tf.sigmoid(tf.matmul(features, W2) + b2)
    layer3 = tf.concat([layer1, layer2], -1)
    layer3 = tf.reshape(layer3, shape = [-1, 2])
    hypothesis = tf.sigmoid(tf.matmul(layer3, W3) + b3)
    return hypothesis
```

layer 1과 layer 2의 결과가 합쳐져 layer 3의 입력으로 사용된다.

10개의 unit를 활용하는 예제는 class로 정의해주었다. Class에는 신경망 구축부터 학습을 위한 함수까지가 정의되어있다.

<br/>

## Tensorboard
텐서보드를 구현하기 위해서는 가장 먼저 summary 값을 logs 폴더에 저장하는 과정이 필요하다.

```python
log_path = "./logs/xor"
writer = tf.summary.create_file_writer(log_path)
```

그리고 코드 중간중간 생성되는 값을 histogram으로 텐서보드에 저장해주어야 한다.

```python
def neural_net(features, step):
    layer1 = tf.sigmoid(tf.matmul(features, W1) + b1)
    layer2 = tf.sigmoid(tf.matmul(layer1, W2) + b2)
    layer3 = tf.sigmoid(tf.matmul(layer2, W3) + b3)
    hypothesis = tf.sigmoid(tf.matmul(layer3, W4) + b4)

    # 텐서보드에 저장
    with writer.as_default():
        tf.summary.histogram("weights1", W1, step=step)
        tf.summary.histogram("biases1", b1, step=step)
        tf.summary.histogram("layer1", layer1, step=step)

        tf.summary.histogram("weights2", W2, step=step)
        tf.summary.histogram("biases2", b2, step=step)
        tf.summary.histogram("layer2", layer2, step=step)

        tf.summary.histogram("weights3", W3, step=step)
        tf.summary.histogram("biases3", b3, step=step)
        tf.summary.histogram("layer3", layer3, step=step)

        tf.summary.histogram("weights4", W4, step=step)
        tf.summary.histogram("biases4", b4, step=step)
        tf.summary.histogram("hypothesis", hypothesis, step=step)
    return hypothesis

def loss_fn(hypothesis, labels):
    cost = -tf.reduce_mean(labels * tf.math.log(hypothesis) + (1 - labels) * tf.math.log(1 - hypothesis))
    # 텐서보드에 저장    
    with writer.as_default():
        tf.summary.scalar('loss', cost, step=step)
    return cost

```

위와 같이 코랩에서 코딩하고 실행하면 log 폴더에 v2 확장자 파일이 생성된다.

이를 다운로드해서 실행하는 방법은 다음과 같다.

1. 터미널(관리자) 실행
2. 텐서보드 설치

    ```bash
    pip install tensorboard
    ```
3. 경로 지정

    ```bash
    tensorboard --logdir="파일명을 제외한 파일 경로"
    ```

4. 기본 포트 http://localhost:6006/ 로 이동

<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/Deep Learning Basic Starting with TF/텐서보드 실행 결과.png"
       style="width: 60%; height: auto; margin:10px">
</figure>
<br/>




[코드 보러가기](https://github.com/deeplearningzerotoall/TensorFlow/blob/feab13059b6c5a674c50c7c2d22dc62c7e157934/tf_2.x/lab-09-4-XOR-tensorboard-eager.ipynb)

<br/>
<br/>

*별도의 출처 표시가 있는 이미지를 제외한 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*
