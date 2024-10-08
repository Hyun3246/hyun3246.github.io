---
title:  "[MIT 데이터 사이언스 기초] Chapter 1. Introduction and Optimization Problems"
excerpt: "간단한 OT, 계산모델, 최적화 모델, 무차별 대입 알고리즘과 탐욕 알고리즘에 대하여"

categories:
  - Data Science & ML
tags:
  - [Data Science, 최적화, Algorithm]

use_math: true
toc: true
toc_sticky: true
 
date: 2023-02-10
last_modified_at: 2023-03-01

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/mit data science.png
---
## 강의 개요
- 강의명: Introduction to Computational Thinking and Data Science (데이터 사이언스 기초 코스)
- 교수: Eric Grimson, John Guttag
- 제작: MIT, 네이버 부스트코스  
<br/>

## 계산모델
계산 모델은 말 그대로 계산하는 모델이다. 현재까지의 일을 이해하거나, 미래의 일을 예측한다. 현대 과학에서는 실험도 중요하지만 컴퓨터 없이는 아무 것도 할 수 없는 상황이 되었다.    

계산모델에는 여러가지가 있다.
- 최적화 모델   
- 통계적 모델   
- 시뮬레이션 모델   
<br/>

## 최적화 모델
목적함수: 최대화하거나 최소화해야 하는 것.  
ex. 수원에서 합천까지 걸리는 시간을 최소화 (명절에 죽음이니...)

제한조건: 반드시 지켜야 하는 rule (있을 수도 있고, 없을 수도 있다)  
ex. 연료가 제한됨.

이를 쉽게 설명한 것이 냅색(보따리) 문제이다.    

도둑이 보따리 하나에 물건을 싸서 도주할 때 어떻게 해야할까?
당연히 보따리 안에 가치있는 물건을 가득 넣어가야 한다. 여기서 정리를 해보면   
- 목적함수: 물건의 가치   
- 제한조건: 보따리 부피 or 도둑의 근력    
     
**"최적화"** 가 필요하다.

교수님이 제시한 더 친숙한 예시는 '식단 구성하기'이다.   
- 목적함수: 선호도를 가장 높이는 식단 구성    
- 제한조건: 칼로리 총량

냅색에는 '0/1 냅색 문제'와 '연속적인 냅색 문제'가 있다. 이후의 선택에도 영향을 줄 수 있는 0/1 냅색 문제가 더 복잡하다.

<br/>
위에서 제시한 냅색 문제는 공식화할 수 있다. 방법은 다음과 같다.    

1. 각 물건들은 쌍으로 표현 <값, 무게>   
2. 냅색은 총 무게 w까지만 수용
3. 길이가 n인 벡터 L은 가능한 물건들의 집합을 표현.   
ex. L = [금괴, 반지, 책, 신문지, TV]
4. 벡터 V는 1과 0으로 물건을 가져가는지를 표현.         
ex. V = [1, 1, 0, 0, 0] -> 금괴와 반지만 가져간다.

가치를 최대화하려면 다음이 최대이면 된다.   
> $\sum_{n=0}^{n-1}$ V[i]*I[i].value

제한조건을 만족하려면 아래와 같다.  
> $\sum_{n=0}^{n-1}$ V[i]*I[i].weight $\leq$ w

<br/>

## 무차별 대입 알고리즘
앞선 문제를 해결하는 가장 간단한 방법은 당연히 다 해보는 것이다.    
좀 더 전문적으로 말하면, 물건 집합의 모든 부분집합, 즉 '멱집합'을 만든다. 그리고 무게를 초과하는 조합을 제거하고 가치가 가장 큰 집합을 선택하면 되는 것이다.    

그러나 당연히 그렇게 효과적이지는 않다. 그렇다고 아예 쓸모 없는 것도 아니다.    
본질적으로 '0/1 냅색 문제'는 지수적이기 때문이다.   
<br/>
## 예제
앞서 나온 칼로리 문제를 구체화하여 파이썬 코드로 제작한다. 교수님은 람다 함수의 사용도 권장하였다.

|Food|wine|beer|pizza|burger|fries|coke|apple|donut|
|---|---|---|---|---|---|---|---|---|
|value|89|90|30|50|90|79|90|10|
|calories|123|154|258|354|365|150|95|195|

~~교수님이 도넛을 별로 안좋아하나보다~~

[예시 코드 보러가기](https://github.com/Hyun3246/Code-Warehouse/tree/main/MIT%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%82%AC%EC%9D%B4%EC%96%B8%EC%8A%A4%20%EA%B8%B0%EC%B4%88)

이 알고리즘의 복잡도는 **nlogn**이다. 정렬(nlogn)과 선택 판단(n)에서 복잡도가 발생한다.     
<br/>

## 왜 항상 답이 다를까?
위 코드의 실행 결과는 항상 다르다. 이런.    
'지역적' 최적의 선택이 언제나 '전역적 최적의 선택'인 것은 아니다.
<br/>
<figure style="display:block; text-align:center;">
  <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/MIT 데이터 사이언스 기초/hills.jpg"
       style="width: 70%; height: auto; margin:10px">
  <figcaption style="text-align:center; font-size:14px; color:#808080">
    한 번 두 개의 정상 중 한 곳에 도착하면 더 이상 올라갈 곳이 없으므로 교착상태에 빠진다
  </figcaption>
</figure>
<br/>


이처럼 탐욕 알고리즘은 장단점이 존재한다.
- 장점: 쉽고 효율적이다
- 단점: 언제나 최적은 아니다.

<br/>
다음 강에서 진짜 최적을 찾는 방법을 알려준다고 한다.   

<br/>
<br/>

*포스트에 사용된 모든 이미지는 강의자료에서 발췌하였음을 밝힙니다.*