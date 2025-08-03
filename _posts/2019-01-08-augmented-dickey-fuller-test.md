---
layout: post
title: (번역) 29가지 통계 개념 - ADF(Augmented Dicky Fuller) 검정
date: 2019-01-01 01:30:00
toc: true
toc_sticky: true
category: 
    - statistics
tag:
    - statistics
    - translation
    - adf-test
mathjax: true
comment: true
---

단위근 검정 방법 중 하나인 Augmented Dickey Fuller 검정에 대해 알아보자.

## Augmented Dickey Fuller 검정이란 무엇인가?

Augmented Dickey Fuller(ADF) 검정은 정상성을 알아보기 위한 단위근 검정 방법이다.
단위근은 시계열 자료에서 예측할 수 없는 결과를 초래할 수 있다.

*Augmented* Dickey Fuller 검정은 자기 상관(serial correlation)과 함께 사용할 수 있다.
ADF 검정은 Dickey-Fuller 검정보다 더 복잡한 모형들을 다룰 수 있으며, 더 강력하기도 하다.
그 말인 즉슨, 이 검정은 다른 단위근 검정과 마찬가지로 조심해서 사용해야 하는데, 그 이유는 다소 높은 제1종 오류율 때문이다.

## 가설

**검정에 사용하는 가설은 다음과 같다.**

* 귀무가설($H_0$): 자료에 단위근이 존재한다.
* 대립가설($H_1$): 시계열 자료가 정상성을 만족한다(또는 추세 정상성을 만족한다). 하지만 대립가설은 어떤 방정식을 사용하느냐에 따라 조금씩 다르다.

## 모형과 시차(lag) 선택하기

**ADF 검정을 실시하기에 앞서**, 적절한 회귀 모형을 찾아내기 위해 여러분의 자료를 검사해보아야 한다.
예를 들어, 평균이 0이 아니라면 회귀 모형에 상수항이 존재할 것이다.
기본적인 세 가지 회귀 모형은 다음과 같다:

* 상수항도 없고, 추세(trend) 도 없는 경우: $\Delta y_t = Y_{y_{t-1}} + v_t$
* 상수항은 있고, 추세(trend) 는 없는 경우: $\Delta y_t = \alpha + Y_{y_{t-1}} + v_t$
* 상수항도 있고, 추세(trend) 도 있는 경우: $\Delta y_t = \alpha + Y_{y_{t-1}} + \lambda_t + v_t$

Augmented Dickey Fuller 는 이 모형들에 **시차 차분(lagged differences)** 을 더해준다:

* 상수항도 없고, 추세(trend) 도 없는 경우: $\Delta y_t = Y_{y_{t-1}} + \sum_{s = 1}^m a_s \Delta y_{t-s} + v_t$
* 상수항은 있고, 추세(trend) 는 없는 경우: $\Delta y_t = \alpha + Y_{y_{t-1}} + \sum_{s = 1}^m a_s \Delta y_{t-s} + v_t$
* 상수항도 있고, 추세(trend) 도 있는 경우: $\Delta y_t = \alpha + Y_{y_{t-1}} + \lambda_t + \sum_{s = 1}^m a_s \Delta y_{t-s} + v_t$

검정을 시행하기 위해서는 **시차의 길이를 선택해야 한다**. 잔차들이 [자기 상관(serially correlated](https://www.statisticshowto.datasciencecentral.com/serial-correlation-autocorrelation/)을 가지지 않도록 시차의 길이를 선택해야만 한다.
시차를 정하는 데에는 여러가지 선택지가 있다: AIC 또는 BIC 를 최소로 하는 값을 선택하거나, 마지막 시차가 통계적으로 유의할 때까지 시차를 바꾸는 것이다.

## 소프트웨어 사용해서 구하기

비록 프로그램이 검정을 대신 해준다고 해도 그 결과를 해석하는 것은 여러분의 몫이다.
일반적으로 p-value 가 0.05 보다 작으면 단위근이 존재한다는 귀무가설을 기각할 수 있는 근거가 충분하다고 할 수 있다.
뿐만 아니라, 도표로 정리된 임계값(critical value)들과 $DF_{\tau}$ 통계량과 비교할 수도 있다.
만일 $DF_{\tau}$ 통계량이 표의 값들보다 더 작다면, 단위근이 존재한다는 귀무가설을 기각할 수 있는 근거가 충분하다고 할 수 있다.
**Note**: DF 검정 통계량의 값이 더 작을 수록 단위근이 존재한다는 귀무가설을 기각할 수 있는 근거가 더 강력하다고 할 수 있다.

DF 검정 통계량:

$DF_{\tau} = \frac{\hat{\gamma}}{SE(\hat{\gamma})}$

![critical values for DF t-distribution](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2016/06/df-critical.png)

### Excel

Excel 은 ADF 검정을 위한 함수가 만들어져 있지는 않다. 하지만 회귀분석과 t 검정의 기능을 활용해서 여러분의 자료에 직접 실행할 수는 있다.
그 단계는 쉽지 않고, 여러 formula 를 요구한다(R 이나 SAS 같은 다른 소프트웨어에서는 훨씬 더 쉽다).
*[principles of Econometrics](http://econweb.tamu.edu/hwang/CLASS/Ecmt463/Lecture%20Notes/Excel/Excel_Lessons.pdf)* 의 181-185쪽에서 필요한 설정과 공식을 명확한 그림으로 보여준다.

### R

R 에서 ADF 검정을 실시하려면 `tseries` 패키지에서 `adf.test` 함수를 사용하면 된다.
이 함수에는 다음과 같은 여러 설정을 포함한다:

* "c"(기본값): 상수항은 포함하지만 추세는 포함하지 않는 모형
* "nc": 상수항도, 추세도 포함하지 않는 모형
* "ct": 상수항과 추세를 포함하는 모형

R 에서 다른 함수들로는 `forecast` 패키지의 *nsdiffs* 함수와 `fUnitRoots` 패키지의 *adfTest* 가 있다.

### Stata

*dfgls* 또는 *dfuller* 를 사용하면 된다.

### SAS

`PROC ARIMA` 에서 ADF test 를 실행하면 된다.

### 참고 자료

Fuller, W. A. (1976). Introduction to Statistical Time Series. New York: John Wiley and Sons. ISBN 0-471-28715-6.
Ogunc, A. & Hill, C. (2008) Using Excel: Companion to Principles of Econometrics, Third Edition. Retrieved January 4, 2017 from: http://econweb.tamu.edu/hwang/CLASS/Ecmt463/Lecture%20Notes/Excel/Excel_Lessons.pdf

### 출처

[ADF - Augmented Dickey Fuller Test](https://www.statisticshowto.datasciencecentral.com/adf-augmented-dickey-fuller-test/)
