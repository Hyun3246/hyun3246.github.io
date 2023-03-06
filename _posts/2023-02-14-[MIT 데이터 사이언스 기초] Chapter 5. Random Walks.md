---
title:  "[MIT 데이터 사이언스 기초] Chapter 5. Random Walks"
excerpt: "랜덤워크를 이용해서 시뮬레이션 모델 검증하고 변형하기"

categories:
  - Data Science
tags:
  - [Data Science, 랜덤워크, 시뮬레이션, 위생검사]

use_math: true
toc: true
toc_sticky: true
 
date: 2023-02-14
last_modified_at: 2023-03-01

header:
  overlay_image: /image/overlay image/mit data science.png
  overlay_filter: 0.5
---
이번 강의는 이론적인 내용보다는 코딩을 이해하는 것에 초점이 맞추어져 있다. ~~그래서 이론 글이 별로 길지 않다.~~
<br/>

## 랜덤워크
랜덤워크는 말 그대로 랜덤하게 걸아다니는 것을 말한다. 시뮬레이션을 어떻게 사용하는지에 대한 좋은 실례를 제공한다.   

<br/>

## 랜덤워크 구현하기
주정뱅이(Drunk)가 좌표평면의 원점에서 시작하여 랜덤하게 걸어간다. 주정뱅이로 설정한 이유는 아무런 의도 없이 랜덤하게 걸어가는 것을 표현하기 위해서이다.     
10000걸음 뒤에 예상되는 주정뱅이의 위치는 어디일까? 코드로 구현하였다.

[관련 코드 보러가기](https://github.com/Hyun3246/Code-Warehouse/tree/main/MIT%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%82%AC%EC%9D%B4%EC%96%B8%EC%8A%A4%20%EA%B8%B0%EC%B4%88)

<br/>

## 위생검사
중요한 것은, 이러한 시뮬레이션을 만들었을 때, 위생검사(맞는 번역인지 모르겠다)를 실시해야 한다는 것이다. 시뮬레이선이 올바르게 작동하는지를 판단하는 일종의 유효성 검사이다.    
위생검사에는 우리가 굳이 시뮬레이션 프로그램을 사용하지 않고도 알 수 있는 간단한 값을 이용해 시뮬레이션이 이를 제대로 구하는지를 파악한다. 예를 들어, 주정뱅이가 한 걸음도 걷지 않았을 때의 거리(0), 한 걸음만 걸었을 때의 거리(1) 등을 사용하는 것이다. 이 예시들은 시뮬레이션이나, 수학적으로 계산한 것이나 같은 값을 가져야 한다.       

[관련 코드 보러가기](https://github.com/Hyun3246/Code-Warehouse/tree/main/MIT%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%82%AC%EC%9D%B4%EC%96%B8%EC%8A%A4%20%EA%B8%B0%EC%B4%88)

<br/>

## 그래프로 시각화하기
이번 강의에서 교수님이 강조한 또다른 이론은 `pylab`을 이용해서 그래프를 구현하는 것이다. `pylab.plot`에는 매우 많은 인자가 있고, 이를 다 외우는 것은 불가능에 가깝다. 그냥 필요할 때 documentation을 찾아보거나 구글링하는 것이 좋다.   

관련 코드 보러가기(추후 업로드)     
<br/>

## 시뮬레이션 변형하기 1
우리가 원하는 것을 얻기 위해 시뮬레이션을 변형할 수 있다.

앞선 랜덤워크에는 모든 방향으로 동일하게 움직이는 일반적인 주정뱅이와 북쪽으로 움직일 때는 조금 더 많은 거리를 움직이는 마조히스틱 주정뱅이가 있었다. 이들의 원점으로부터의 거리를 그래프로 나타내는 다음과 같다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/MIT 데이터 사이언스 기초/주정뱅이 평균 거리.jpg"
       style="width: 80%; height: auto; margin:20px">
</figure>
<br/>
단순히 거리를 선 그래프로 나타내는 것이 아니라, 좌표를 활용해서 위치를 표현할 수도 있다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="/image/MIT 데이터 사이언스 기초/주정뱅이 산포도 거리.jpg"
       style="width: 80%; height: auto; margin:20px">
</figure>
<br/>
알 수 있는 사실은, 매조히스틱 주정뱅이는 동서방향으로는 일반적인 주정뱅이와 동일하지만 북쪽으로 좀 더 치우쳐 있다는 것이다. 생각해보면 당연할 수밖에 없다.

[관련 코드 보러가기](https://github.com/Hyun3246/Code-Warehouse/tree/main/MIT%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%82%AC%EC%9D%B4%EC%96%B8%EC%8A%A4%20%EA%B8%B0%EC%B4%88)     

<br/>

## 시뮬레이션 변형하기 2
주정뱅이를 바꾸는 것이 아니라, 필드(좌표평면)를 바꿀 수도 있다.     
순간이동을 지원하는 웜홀(Wormholes)을 곳곳에 랜덤으로 생성하고 주정뱅이의 이동에 영향을 줄 수도 있다.

[관련 코드 보러가기](https://github.com/Hyun3246/Code-Warehouse/tree/main/MIT%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%82%AC%EC%9D%B4%EC%96%B8%EC%8A%A4%20%EA%B8%B0%EC%B4%88)  

<br/>

이번 강의는 이론보다는 코딩에 초점이 조금 더 맞추어져 있었던 것 같다. 중요한 것은, 시뮬레이션은 위생검사로 검증해야 하며, 우리가 원하는 것을 얻을 수 있도록 조금씩 수정할 수 있다는 사실이다.

<br/>
<br/>

*포스트에 사용된 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*