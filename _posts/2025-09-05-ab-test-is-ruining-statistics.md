---
layout: post
title: "A/B 테스트가 통계학을 망치고 있다"
date: 2025-09-05
toc: true
toc_sticky: true
category: 
    - statistics
tag:
    - experiment
mathjax: true
comment: true
---

A/B 테스트란 무엇이고, 제가 왜 이게 통계학을 망치고 있다고 생각하는지 설명드리고자 합니다.

## TL;DR

- A/B 테스트는 다양한 통계적 가설 검정 방법 중 한 카테고리로, 이를 대체할 수 있는 용어가 아니며, 대체해서도 안 된다고 생각
- A/B 테스트 대신 RCT (Randomized Controlled Trial; 무작위 대조군 연구) 또는 온라인 대조 실험 (Online Controlled Experiment) 정도의 용어를 제안

## Origin of A/B Test (the term)

저는 어떤 현상을 살펴볼 때 그 기원을 찾아 보는 것을 매우 좋아합니다. 그래서 `A/B Test` 라는 용어를 처음 만든 사람을 찾고 싶었으나 그건 매우 어려웠고, [구글 트렌드](https://trends.google.com/trends/explore?date=all&q=A%2FB%20testing&hl=en)를 이용하여 간접적으로나마 확인해볼 수 있었습니다.

![google-trend-ab-testing](/images/2025-09-05/ab-test-vs-statistical-hypothesis-testing.png)

> 구글 트렌드 (에서는 가장 높은 검색량을 100으로 잡고 상대적인 검색량을 보여주는 것으로 알고 있습니다. 따라서 검색량이 매우 적은 경우, 검색이 있었음에도 불구하고 0으로 나올 수도 있습니다.) 의 검색 결과에 따르면 2007년 9월 처음으로 4라는 값을 가진 것을 확인할 수 있었습니다. 2010년 이전에는 통계적 가설 검정 (Statistical Hypothesis Testing) 의 검색량이 A/B Test 보다 높았으나, 2010년대에 들어서 A/B Test 의 검색량이 역전하였으며, 그 이후로 꾸준히 증가하였습니다.

저는 [린 분석 (Lean Analytics - Allistair Crol, Benjamin Yoskovitz 2013)](https://www.oreilly.com/library/view/lean-analytics/9781449335687/) 과 [그로스해킹](https://en.wikipedia.org/wiki/Growth_hacking)의 등장이 `A/B Test` 라는 용어를 더 널리 퍼트리지 않았을까 추측합니다.

## A/B Test is just a part of Statistical Hypothesis Testing

그렇다면 비교에 사용한 **통계적 가설 검정 (statistical hypothesis testing)** 에 대해 간략하게 설명하자면, 말 그대로 우리가 세운 '가설 (hypothesis)' 을 '통계적으로 (statistically)' '검정 (test)' 하는 것입니다.

![categories-of-hypothesis-testing](https://cdn1.qualitygurus.com/wp-content/uploads/2022/12/Common-Types-of-Hypothesis-Tests.png?lossy=1&ssl=1)

그렇기 때문에 여기에는 매우 다양한 방법이 있고, 모수적인 (parametric) 검정 방법만해도 비교하고자 하는 집단의 수와 통계량 (statistic) 에 따라 이렇게 다양하게 나눌 수 있습니다. 하지만 A/B 테스트는 그 이름에서 알 수 있듯이, 두 집단에 대한 것만 다루고 있습니다. A/B 테스트의 대상이 되는 값은 수치형이고, 비교하는 그룹의 갯수는 2개이므로 위의 그림에서는 `Two Sample` 가지 아래에 있는 기법들만 다룬다고 할 수 있습니다.

그리고 3개 이상의 그룹을 대상으로 통제 실험을 하는 경우 `A/B/C 테스트, A/B/n 테스트` 와 같은 형태로 부르는 것도 어렵지 않게 확인할 수 있습니다.

## Terminology matters

[제 다른 글](https://chukycheese.github.io/statistics/parameter-clt/) 에서도 밝혔지만 저는 일부 통계학 용어에 대해 꽤나 민감하게 반응하는 편입니다 (지금은 좀 나아진 것 같기도 하지만요). 통계적 가설 검정이라는 용어가 길어서 사용하기 번거로운 편인 것은 인정합니다. 그렇지만 해당 단어는 매우 직관적입니다.

우리가 가설 (hypothesis) 을 세우고, 이를 통계적으로 (statistically) 검정 (test) 하기 위해 실험을 설계하고, 그 과정을 지켜야한다는 것을 7글자 안에서 모두 보여주기 때문입니다.

## References

- [Quality Gurus - Common Types of Hypothesis Tests](https://www.qualitygurus.com/common-types-of-hypothesis-tests/)
- [Win Vector LLC - I do not believe Google invented the term A/B test](https://win-vector.com/2015/06/12/i-do-not-believe-google-invented-the-term-ab-test/)
- [Oreilly - Lean Analytics (Allistair Crol, Benjamin Yoskovitz 2013)](https://www.oreilly.com/library/view/lean-analytics/9781449335687/)
- [Wikipedia - Growth Hacking](https://en.wikipedia.org/wiki/Growth_hacking)
