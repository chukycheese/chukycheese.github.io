---
layout: post
title: 29가지 통계 개념 - 통계학에서의 68, 95, 99.7의 법칙(68 95 99.7 Rule in Statistics)
date: 2019-01-02
toc: true
toc_sticky: true
category:  
    - statistics
tag:
    - translation
    - statistics
mathjax: true
comment: true
---

## 68 95 99.7의 법칙이란 무엇인가?

[경험 법칙(The empirical rule)](https://youtu.be/hQTvdD8vtio)

통계학에서 표준 정규 모형을 사용하는 경우:

* 약 68%의 값은 평균에서 1-표준편차 이내에 위치한다
* 약 95%의 값은 평균에서 2-표준편차 이내에 위치한다
* 거의 대부분의 값(약 99.7%)은 평균에서 3-표준편차 이내에 위치한다

이러한 사실들이 68 95 99.7의 법칙이라고 불리며 때로는 *경험 법칙* 이라고도 한다. 그 이유는 이 법칙이 원래 **관측**에서 왔기 때문이다(*경험*이란 "관측에 기반한"이라는 의미이다)

![standard-normal-distribution](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2013/09/standard-normal-distribution.jpg)

* 표준편차들을 보여주는 표준 정규 분포(이미지 출처: University of Virginia)

정규 곡선이란 **가장 일반적인 형태의 자료 분포**이다. 정규분포에서는 모든 측정치들이 평균으로부터의 거리로 계산된다. 이 측청치들은 표준 편차로 보여진다.

정규 곡선은 좌우대칭인 분포이기 때문에 중앙의 68.2%는 반으로 나눠질 수 있다. 평균으로부터 0에서 1-표준편차 이내에는 34.1%의 자료가 위치한다. 반대편(0에서 -1-표준편차)에도 마찬가지 이다). 둘을 합치면 이 안에 68%의 데이터가 존재하는 것이다.

![standard-normal-distribution-2](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2013/02/standard-normal-distribution.jpg)

* *정규분포에서 각 표준편차만큼의 거리 안에서 기대되는 데이터의 비율*

## 이 법칙을 언제 사용할 수 있을까?

이 법칙은 여러분의 데이터가 정규분포를 따르거나, 거의 정규분포를 따른다고 할 수 있거나, 좌우 대칭이고 하나의 최빈값(unimodal)을 가진 분포의 형태를 띄고 있을 때 사용할 수 있다. 만약에 문제에서 정규분포나 근사 정규분포를 언급하고 있고, *그리고* 표준편차가 주어졌다면 평균으로부터 특정 표준편차 거리 안에 대략적으로 어느 정도의 데이터가 그 안에 위치하는지 구할 수 있다는 말이다.

## 예제

어떤 강아지들의 몸무게가 평균 70 lbs, 표준편차 2.5 lbs 아래에 평균 70 lbs였다고 하자. 이 몸무게가 정규분포를 따른다고 할 때:

1. 평균으로부터 2-표준편차 아래의 몸무게는 몇 lbs인가?
2. 평균으로부터 1-표준편차 위의 몸무게는 몇 lbs인가?
3. 가운데 68%에 위치한 강아지들의 몸무게의 범위는 얼마인가?

답:

1. 2-표준편차는 2 * 2.5 = 5(lbs) 이다. 즉, 평균으로부터 2-표준편차 아래인 강아지의 몸무게는 70 - 5 = 65 lbs 이다.
2. 1-표준편차는 2.5 lbs 이므로, 평균으로부터 1-표준편차 위에 위치한 강아지의 몸무게는 70 + 2.5 = 72.5 lbs 이다.
3. 68 95 99.7의 법칙에 의하면 68% 의 데이터는 평균으로부터 1-표준편차 이내에 위치한다고 한다. 2번 문제에서 1-표준편차 위의 몸무게는 72.5 lbs 였다. 1-표준편차 아래의 몸무게는 70 - 2.5 = 67.5 lbs 이므로 68%의 강아지는 몸무게가 67.5 에서 72.5 lbs 사이에 있다고 할 수 있다.

## 68 95 99.7의 법칙의 역사

68 95 99.7의 법칙은 정규분포 모형이 발간되기 75년 전인 1733년 아브라함 드무아브르(Abraham de Moivre)가 만들었다. 드무아브르는 확률론의 발전에 이바지했다. 아마도 통계학에 대한 그의 가장 큰 업적은 [우연의 교의(The Doctrine of Chances)](https://archive.org/details/doctrineofchance00moiv) 일 것이다. 이 책에는 시행 횟수가 많을 경우 이항 분포를 정규 분포로 근사하는 내용이 담겨 있다.

![abraham-de-moivre](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2013/09/abraham-de-moivre.jpg)

드무브아르는 실험을 통해 68 95 99.7의 법칙을 발견했다. 여러분도 100개의 공정한(fair) 동전을 던지는 것으로 실험을 해볼 수 있다.

* 윗면(head)가 나올 것으로 기대하는 숫자; 이를 이항 실험에서는 "성공"이라고 한다
* 표준편차
* 여러분이 68%, 95%, 99.7% 의 경우에 얻을 수 있는 윗면의 갯수의 하한과 상한

### 참고

Mónica Blanco and Marta Ginovart. How to introduce historically the normal distribution in engineering education: a classroom experiment. Retrieved December 28 2015. http://upcommons.upc.edu/bitstream/handle/2117/6483/howtointroduce.pdf

### 출처

[68 95 99.7 Rule in Statistics](https://www.statisticshowto.datasciencecentral.com/68-95-99-7-rule/) : 2023-10-20 현재 해당 주소로는 접근이 불가능한 것으로 확인했습니다.
