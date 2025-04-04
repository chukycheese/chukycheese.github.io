---
layout: post
title: 29가지 통계 개념 - 독립성 가정
date: 2019-02-07 01:00:00
toc: true
toc_sticky: true
category: statistics
tag:
    - statistics
    - translation
    - independence
mathjax: true
comment: true
---

여러 통계 검정과 모형에서 사용되는 독립성 가정에 대해 알아보자.

## 독립성 가정이란 무엇인가?

![f-test](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2012/11/f-test.jpg)

*독립성 가정은 여러 통계 검정에 기반이 된다*.

독립성 가정은 t-검정, ANOVA 검정, 그리고 여러 다른 통계적 검정에 사용된다.
이는 모집단에서 찾을 수 있는 것을 반영하는 결과를 표본에서 얻는데에 필수적이다.
이 가정을 위반한다면 데이터에 있는 아주 작은 종속성이라도 (찾을 수 없을지도 모르는) 굉장히 큰 편향을 낳을 수 있다.

**종속성** 이란 데이터 사이의 연결을 의미한다.
예를 들어, 수입은 일하는 시간에 *의존한다*.
**독립성** 이란 이러한 관계가 없다는 뜻이다.
수입과 아침에 먹은 음식 사이에는 아무런 관계가 없듯이 말이다.
독립성 가정은 데이터들이 그 어떠한 관계도 없다는 것이다(적어도 모형에 고려하지 않은 것들 중에는).

사실 여기에는 두 가지 가정이 있다:

* **집단 사이의 관측치**는 독립적이어야 한다. 즉, 두 집단은 서로 다른 사람들로 구성되어 있다는 뜻이다.
한 사람이 두 집단 모두에 속해있다면 결과를 편향되게 만들 수 있기 때문에 별로 원하는 상황이 아닌 것이다.

* **각 집단 내의 관측치** 들은 독립적이어야 한다.
한 집단 안의 둘 이상의 데이터들이 어떤 형태로든 관계가 있다면, 이 또한 편향된 결과를 낳을 수 있다.
예를 들어, 사람들이 먹은 도넛의 갯수를 매일 아침 9시, 10시, 11시에 기록한다고 하자.
이 경우 사무직 종사자들이 하루 칼로리의 25%를 도넛으로 섭취한다는 결론을 내릴 수도 있다.
하지만 이 경우 사람들이 같이 먹을 도넛들을 가지고 들어오는 경우가 많으므로
조사 시간을 너무 가깝게 잡은 실수를 저질렀다고 볼 수 있다(이는 관측치들을 *종속적*으로 만든다).
만약 측정 시간을 오전 7시, 정오, 오후 4시로 했다면 측청치들을 독립적으로 만들 수 있을 것이다.

## 독립성 가정을 위반하면 어떻게 될까?

쉽게 말해서, 독립성 가정을 위반하면 모든 결과물이 틀릴 수도 있는 위험에 빠진다고 할 수 있다.

## 독립성 가정을 위반하지 않으려면 어떻게 해야할까?

안타깝게도 데이터를 보고, 그 데이터가 독립적인지 아닌지를 판단하는 것은
일반적으로 어렵거나 불가능하다.
독립성 가정을 위반하지 않으려면 *수집하는 과정에서부터* 독립적인 것을 확인해야한다.
해당 분야의 전문가가 아니라면 이는 어려울 수 있다.
하지만, 그 분야의 이전 연구를 살펴보고 데이터가 수집된 방법을 확인하도록 하라.

### 출처

[Assumption of Independence](https://www.statisticshowto.datasciencecentral.com/assumption-of-independence/)
