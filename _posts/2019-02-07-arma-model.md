---
layout: post
title: 29가지 통계 개념 - ARMA 모형
date: 2019-02-07 00:30:00
toc: true
toc_sticky: true
category: statistics
tags:
    - statistics
    - translation
    - time-series
    - arma
mathjax: true
comment: true
---

시계열 모형 중 ARMA 모형에대해 알아보자.

## ARMA 모형

ARMA 모형, 또는 자기회귀이동평균 (Autoregressive Moving Average) 모형은 두 가지 다항식으로
약한 정상성을 가진 확률적 시계열을 표현하는데 사용한다.
이 두 다항식 중 첫 번째는 자기회귀(autoregressive)이며, 두 번째는 이동평균(moving average)이다.

때때로 이 모형을 **ARMA(p, q)** 로 나타내기도 하며, 여기서 p와 q는 아래와 같다:

* p: 자기회귀 다항식의 차수(order)
* q: 이동평균 다항식의 차수(order)

전체 방정식은 다음과 같으며, 모수들은 그 아래에 설명되어 있다.

$X_t = c + \epsilon_t + \sum_{i = 1}^p \phi_i X_{t-i} + \sum_{i = 1}^q \theta_i \epsilon_{t-i}$

* $\phi$: 자기회귀 모형의 모수
* $\theta$: 이동평균 모형의 모수
* $c$: 상수
* $\epsilon$: 오차항 (백색잡음; white noise)

## ARMA 모형과 ARIMA 모형과의 차이

두 모형은 비슷한 점이 많이 있다.
실제로 일반적인 자기회귀 모형인 AR(p) 와 이동평균 모형인 MA(q) 를 포함하는 것은 동일하다.
AR(p) 모형은 종속변수의 이전 값을 이용해서 예측을 한다.
MA(q) 모형은 시계열의 평균과 이전의 오차를 이용해서 예측을 한다.

ARMA 와 ARIMA 의 차이를 만드는 것은 *차분(differencing)* 이다.
ARMA 모형은 정상성을 가진 모형이다.
만약 모형이 정상성을 가지고 있지 않다면, 시계열을 차분함으로써 정상 시계열로 만들 수 있다.
ARIMA 모형에서 "I" 는 누적(integrated) 을 의미한다.
이는 비정상(non-stationary) 시계열을 정상(stationary) 시계열로 만들기 위해서 필요한 차분의 횟수를 나타낸다.
만약 **모형에 차분이 필요 없다면** ARIMA 모형은 ARMA 모형이 된다.

적합을 위해서 d차 차분이 필요한 ARMA(p, q) 모형은 차수가 (p, d, q) 인 ARIMA 과정(process) 라고 한다.
p, d, 그리고 q 값은 AIC, BIC, 그리고 경험적인 자기상관 등 다양한 방법을 통해서 선택할 수 있다(Petris, 2009)

또 다른 비슷한 모형으로는 ARIMAX 가 있는데, 이는 추가적인 설명변수(additional explanatory viariables)를 포함한 ARIMA 모형이다.

### 참고자료

Petris, G. et al. (2009). [Dynamic Linear Models with R](https://books.google.co.kr/books?id=VCt3zVq8TO8C&redir_esc=y). Springer Science & Business Media.

### 출처

[ARMA model](https://www.statisticshowto.datasciencecentral.com/arma-model/)
