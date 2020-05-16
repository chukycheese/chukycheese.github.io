---
layout: post
title: 번역] 몇 가지 추천 시스템에 대한 개괄
date: 2020-01-07 00:30:00
category: data science
tags:
    - data science
    - statistics
    - machine learning
    - recommendation
    - recommendation system
    - 데이터 사이언스
    - 추천 시스템
mathjax: true
comment: true
---

원문: [An Overview of Several Recommendation Systems](https://towardsdatascience.com/an-overview-of-several-recommendation-systems-f9f8afbf00ea)

협업 필터링 (collaborative filtering), kNN, 딥러닝 (deep learning), 전이학습 (transfer learning), TF-IDF 등에 대해서 살펴보자.

이번 글에서는 몇 가지 추천 알고리즘에 대해서 리뷰를 하고 KPI 를 통해 평가를 하고 실제로 비교를 해보려고 합니다. 다음과 같은 순서대로 살펴볼 예정입니다.

* 인지도 기반 추천 시스템
* 컨텐츠 기반 추천 시스템 (kNN TF-IDF, 전이학습)
* 사용자 기반 추천 시스템
* 하이브리드 (hybrid) 추천 시스템
* 딥러닝 추천 시스템

참고: 이 글은 [가브리엘 모레이라(Gabriel Moreira) 의 글](https://www.kaggle.com/gspmoreira/recommender-systems-in-python-101) 에 영감을 얻어서 쓰게 되었으며, 사용자 프로파일러나 평가 함수 같은 일부 모형과 함수는 그의 노트북에서 가져왔음을 알립니다.

---

## 들어가기ㅣ

데이터를 소개하고 어떤 것을 이용해서 우리의 모형을 평가할 수 있는지를 정의하고자 합니다. 보다 신뢰할 수 있는 컨텐츠 추천을 만들기 위해 조금 가공한 에니메이션 메타 데이터를 이용할 것입니다.

Introduction
I will introduce the databases and define what will allow us to evaluate our models. I have anime metadata that I modified a little bit to have more reliable content recommendations.