---
title: 통계학에서의 10% 조건이란 무엇인가?
date: 2019-01-02
category: 
    - translation
    - statistics
source: https://www.statisticshowto.datasciencecentral.com/10-condition/
---

# [통계학에서의 10% 조건이란 무엇인가?](https://www.statisticshowto.datasciencecentral.com/10-condition/)

## 10% 조건

10% 조건이란 표본의 크기가 **모집단 크기의 10%를 넘지** 않아야 한다는 것이다. 통계학에서 표본이 관련된 경우라면, 여러분이 완전한 결과를 얻었는지 확인하기 위해 이 조건을 확인하길 바란다. 몇몇 통계학자들은 [표준 정규 모형](https://www.statisticshowto.datasciencecentral.com/probability-and-statistics/normal-distributions/)을 사용하는 경우라면 10% 조건보다 5% 조건이 더 낫다고 말하기도 한다.

![sample_population](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2013/09/10-percent-condition.jpg)

예를 들어, 10% 조건은 다음과 같은 경우에 **적용**할 수 있다:

* 중심 극한 정리(Central Limit Theorem)에서 비복원 추출을 하는 경우
* 두 집단에서 비율을 가지고 있는 경우
* 아주 작은 모집단이나 아주 큰 표본에서 평균의 차이를 확인하는 경우
* Student's t-test 를 사용하는 경우
* 독립적이지 않은 베르누이 시행을 다루는 경우. 일반적으로 베르누이 시행은 독립적이나, 표본의 크기가 모집단의 10% 보다 크지 않은 경우에는 이 법칙을 거스르는 것도 괜찮다.
    
다음과 같은 경우에는 10% 조건을 **일반적으로 확인하지 않는다**:

* 카이제곱 검정(Chi-square test)을 하는 경우
* 평균의 차이를 확인하는 경우(작은 모집단이나 아주 큰 크기의 표본이 아닐 때)
* 임의 실험을 하는 경우(임의 실험에서는 표본 추출이 없기 때문에 10% 조건을 사용할 수 없다)
    
일반적으로, 통계적인 의미로 10% 조건을 언급한 것을 찾기는 힘들 것이다. 부분에 대한 추론을 해야하는 경우라면 대표본 때문에 10% 조건이 필수적이다. 하지만 평균에 대해서는 표본의 크기가 더 작기 때문에 **아주 작은 모집단에서 표본을 추출 하는 경우에만** 이 조건을 필요로 한다.

이 조건이 **베르누이 시행**에 적용되는 이유는 대부분의 경우 비복원 추출을 하기 때문이다. 예를 들어 "예"와 "아니오"를 묻는 전화 설문 조사라면 이미 그 질문에 대답한 사람을 다시 조사집단에 넣진 않는다는 뜻이다.


## 10% 조건은 어디서 온 것인가?

이 조건에 대한 가정을 뒷받침해주는 수학적인 증명이 있기 때문에 이는 통계학적으로 적절하다. 이에 대한 증명은 기초 통계학이나 고등학교 수준의 통계학을 넘어서지만, 이 조건을 뒷받침하는 원리에 대해 더 알고 싶다면 [텍사스대학교](https://www.ma.utexas.edu/users/mks/M358KInstr/TenPctCond.pdf)에서 제공하는 자료를 한 번 확인하라.

**원문:**

<https://www.statisticshowto.datasciencecentral.com/10-condition/>
