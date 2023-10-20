---
layout: post
title: 사내 스터디에 대한 회고
date: 2020-02-09 00:30:00
toc: true
toc_sticky: true
category: retrospect
tags:
    - retrospect
    - data-analytics
    - recommendation-system
mathjax: true
comment: true
---

회사 서비스의 추천 시스템을 개선하기 위해 팀 내에서 (아직까진 두 명이긴 하지만) 지난 두 달 동안 스터디를 진행했습니다. 얼마 전 두 번째 스터디가 끝났고 이에 대한 회고를 해보려고 합니다.

![full-brain](https://pbs.twimg.com/media/EHt924WVAAAwMxa?format=jpg&name=900x900)

## 진행 방식 및 일정

### 진행 방식

* 한 명씩 돌아가면서 일정 부분을 공부해서 상대방에서 설명하기

### Google Machine Learning Crash Course

* 바로 Google Recommendation Systems 를 시작하려고 했으나 `ML 에 대한 기본적인 지식이 있으면 좋다` 는 강좌 소개를 보고 빠르게 보고 정리하면서 까먹고 있던 것들을 되새기기 위해 진행

#### ML Crash Course 에서 좋았던 점

* 한동안 ML 보다는 통계적 모델링이나 검정을 업무에 많이 사용했어서 기억 속 어딘가에 쳐박혀있던 지식을 조금이나마 꺼낼 수 있는 시간이었음
* 이전까지 했던 ML 공부는 혼자 하거나 내가 동료들을 가르쳐주는 입장이어서 피드백을 제대로 받지 못했는데 이번에는 잘못 이해하고 설명을 하면 이에 대한 피드백을 바로 받을 수 있어서 좋았음
* 피드백을 `그거 틀렸어` 가 아니라 `왜 그렇게 생각하느냐, 이런 경우는 어떻게 하느냐, 다시 잘 정리해서 설명해보라` 는 식으로 해주셔서 피드백을 더욱 적극적으로 요구했던 것 같음

#### ML Crash Course 에서 아쉬웠던 점

* Google 에서 제공하는 것이니 TF 를 쓰는 것이 당연하겠지만 온전히 TF 로만 진행되는 부분은 조금 아쉽긴 했음
* `Crash Course` 답게 후루룩!!! 하고 넘어가는 게 있어서 전혀 모르는 상태에서 보기에는 쉽지는 않을 듯

### Google Recommendation Systems

* 본격 추천 시스템 스터디! ML Crash Course 처럼 강의가 있는 줄 알았으나 온전히 텍스트만으로 이루어진 과정입니다.

#### Recommendation Systems 에서 좋았던 점

* 막연히 `이렇게 하면 되겠지` 라고만 알고 있던 추천 알고리즘들에 대해서 조금은 더 깊게 알 수 있게 된 계기
* 이론적인 설명을 그림과 간단한 데이터셋으로 해줘서 긴 설명이 없는데도 불구하고 이해하는 것이 엄청나게 어렵지는 않았음

#### Recommendation Systems 에서 아쉬웠던 점

* 아쉬웠다고 하기는 애매하지만, 막연히 알 때는 크게 고민하지 않았던 것들인데 실제 서비스에 적용할 수 있을까 하는 걱정이 늘어남
* TF 를 안 쓰다 보니 여전히 진입 장벽이 크게 느껴짐

끝!!

![pengsu-graduation](https://cdn.clien.net/web/api/file/F01/9309261/503d92f7c56aa4.png?thumb=true)

인줄 알았으나 Coursera 에서 University of Minnesota 에서 진행하는 [Recommendation Systems](https://www.coursera.org/learn/recommender-systems-introduction/home/welcome) 시작 예정!!

## 향후 일정

* 해당 Specialization 은 총 4개의 강좌로 구성되어 있는데 아직까진 첫 강좌에 대해서만 일정을 세운 상태
* 진행 방식은 동일하게 한 사람씩 번갈아가면서 해당 부분을 이끌어서 일주일에 1시간 이내로 정리한 내용을 설명하는 시간을 가지는 방식
* 2월 18일 ~ 4월 28일
  * `Introduction to Recommender Systems: Non-Personalized and Content-Based`
