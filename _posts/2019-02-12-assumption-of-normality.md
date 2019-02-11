---
layout: post
title: 29가지 통계 개념 - 독립성 가정
date: 2019-02-11 00:30:00
category: statistics
tags:
    - statistics
    - assumption of normality
    - 정규성 가정
    - normality test
    - 정규성 검정
mathjax: true
comment: true
---

통계적 검정과 회귀분석에서 자주 사용되는 정규성 가정과 정규성 검정에 대해 알아보자.

## 정규성 가정이란 무엇인가?

정규성 가정은 통계적 검정이나 회귀분석을 실행하기에 앞서 데이터가 종 모양의 분포를 대략적으로 따르는지 확인해야 한다는 것을 의미한다.
데이터가 정규분포를 따라야하는 검정들은 다음과 같다.

* 독립 표본 t-test
* 계층적 선형 모형([Hierarchical Linear Modeling](https://www.statisticshowto.datasciencecentral.com/hierarchical-linear-modeling/))
* 공분산분석(ANCOVA)
* 적합도 검정(Goodness of Fit test)

## 정규성 검정을 하는 방법

정규성 검정을 하는 방법으로는 크게 두 가지가 있다.
그래프를 눈으로 살펴보거나, 정규성 검정을 위해서 만들어진 검정을 실행하는 것이다.
하지만, **정규성을 만족하지 않는 데이터는 특정 종류의 테스트에 대해서 좋지 않은 성능을 보여주기도 한다**
(예를 들어, 정규성 가정을 만족해야만 한다고 표기되어 있는 것들!).
그렇다면 데이터가 정규성 검정을 어느 정도로 만족해야 할까?
이는 판단하기 나름이다.

(일반적으로 통계학적인 지식에 기반하는) 이러한 판단을 내리기 껄끄럽다면,
통계적인 검정을 실행하는 것이 나을 것이다(검정 방법에 대해서는 아래를 참조하라).
즉, 어떤 검정들은 사용하기도 번거롭고, 검정 통계량과 임계값을 찾아야한다.

**어떤 것을 선택해야하는지 헷갈리는가?**
통계학에 대한 지식이 많지 않다면 해석하기 가장 쉬운 그래프는 히스토그램이다.
가장 쉬운 검정 방법은 아마도 자크-베라 검정(Jarque-Bera test)일 것이다.

## 그래프를 이용해서 정규성 검정하기

### 1. Q-Q Plot

![normal-exponental-qq](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2015/08/Normal_exponential_qq.svg_.png)

Q-Q plot 은 두 가지 다른 분포를 비교한다.
만약 두 데이터셋이 서로 같은 분포에서 뽑혔다면,
데이터 포인트가 45도의 직선 위에 위치할 것이다.
이러한 종류의 그래프를 정규성 검정에 이용하기 위해서는
*알려진* 정규분포에 데이터를 비교해야 한다.

### 2. 상자그림(Boxplot)

![normal-boxplot](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2016/03/normal-boxplot-2.png)

*정규분포를 따르는 데이터의 상자그림(위)과 정규분포를 따르지 않는 데이터의 상자그림(아래)*

데이터를 이용해서 상자그림을 그려보라.
데이터가 정규분포를 따른다면 상자그림은 좌우대칭이고, 평균과 중앙값이 가운데에 있는 형태를 띌 것이다.
데이터가 정규성 가정을 만족한다면 이상치(outlier)는 거의 없어야 한다.

### 3. 정규확률그림(Normal Probability Plot)

![normal-probability-plot](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2013/09/normal-probability-plot-5.gif)

*대략적으로 정규분포를 따르는 데이터의 정규확률그림(Normal probability plot)*

정규확률그림은 정규성 가정을 검정하기 위해서 만들어졌다.
만약 데이터가 정규분포에서 왔다면, 

### 4. 히스토그램(Histogram)

![histogram](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2013/09/normal-probability-plot-4.jpg)

*종모양을 가진 정규분포를 따르는 데이터, 출처: NASA*

잘 알려진 히스토그램은 데이터가 정규성 가정을 만족하는 지에 대해 알려줄 수도 있다.
데이터가 종모양과 비슷하다면, 정규분포를 따를 수도 있다.

## 통계적으로 정규성 검정하기

정규성 검정에는 *엄청나게 많은* 방법이 있다.
아래에 있는 대부분의 방법은 SPSS 와 같은 통계 패키지에서 사용할 수 있다.

1. **카이제곱 정규성 검정(Chi-square normality test)**:
정규성 검정에 카이제곱 분포를 이용할 수도 있다.
이 방법의 장점은 사용하기에 쉽다는 것이지만, 아주 강력한 검정 방법은 아니다.
표본의 갯수가 작은 경우(20개 미만)에는 사용할 수 있는 *유일한* 방법일 것이다.
표본의 갯수가 많다면 훨씬 더 다양한 방법을 사용할 수도 있다.

2. **디아고스티노-피어슨 검정(D'Agostino-Pearson test)**:
이 검정 방법은 왜도(skewness) 와 첨도(kurtosis) 를 사용해서 데이터가 정규분포와 일치하는 지를 살펴본다.
표본의 크기가 20개보다 큰 경우에만 사용할 수 있다.

3. **자크-베라 검정(Jarque-Bera test)**:
이 일반적인 검정은 비교적으로 직관적이다.
디아고스티노-피어슨 검정과 마찬가지로 기본적인 아이디어는 정규분포에서 기대하는 왜도와 첨도와
데이터에서 얻은 값이 일치하는지를 살펴보는 것이다.
JB 통계량이 클수록 정규분포에서 얻은 것일 확률이 높다.

4. **콜모고로프-스미르노프 적합성 검정(Kolmogorov-Smirnov Goodness of Fit test)**:
이 방법은 알려진 분포(예를 들어, 정규분포) 와 주어진 데이터를 비교하는 방법이다.

5. **릴리포스 검정(Liliefors test)**:
릴리포스 검정은 임계값과 비교할 수 있는 검정 통계량 T 를 계산한다.
검정 통계량이 임계값보다 크다면 데이터가 정규분포를 따르지 않는다는 신호라고 할 수 있다.
또한 유의수준과 비교할 수 있는 p-value 도 계산해준다.

6. **샤피로-윌크 검정(Shapiro-Wilk test)**:
이 검정 방법은 임의의 표본이 정규분포에서 추출된 것인지를 알려준다.
검정 통계량 W 값을 주는데, 값이 작은 경우 주어진 데이터가 정규분포를 따르지 *않는다는* 것을 말해준다.

출처: [Assumption of Normality / Normality Test](https://www.statisticshowto.datasciencecentral.com/assumption-of-normality-test/)
