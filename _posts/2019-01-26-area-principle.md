---
layout: post
title: 29가지 통계 개념 - 통계학에서의 넓이에 대한 원칙
date: 2019-01-26 00:30:00
category: statistics
tags:
    - statistics
    - visualization
    - 시각화
mathjax: true
comment: true
---

시각화에서 주의할 점인 넓이를 표시하는 원칙에 대해 알아보자.

## 넓이에 대한 원칙이란 무엇인가?

넓이에 대한 원칙이란 그래프의 영역은 자료가 표현하고자 하는 정도와 동일해야한다는 것이다. 
쉬운 예를 들어보면, 4 ft, 5 ft, 6 ft 라는 세 길이에 대한 값을 얻었다고 하자.
**아래 그림 중 위의 것은 넓이에 대한 원칙을 만족한다**.

* 4 ft 로 측정된 것의 넓이는 4(높이가 1, 길이가 4인 상자)이다.
* 5 ft 로 측정된 것은 넓이는 5(높이가 1, 길이가 5인 상자)이다.
* 6 ft 로 측정된 것은 넓이는 6(높이가 1, 길이가 6인 상자)이다.

![area principle](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2015/08/area-principal.png)

**아래의 그림은 넓이에 대한 원칙을 위반한다**. 
표기된 수치보다 넓게 표현되었기 때문에 사람들의 시선은 자연스럽게 4 ft 짜리 상자들로 갈 것이다.
6 ft 상자가 명백하게 더 길지만, 더 넓은 영역을 가진 곳으로 가는 것이다.

* 4 ft 로 측정된 것의 넓이는 8(높이가 2, 길이가 4인 상자)이다.
* 4 ft 로 측정된 것의 넓이는 5(높이가 1, 길이가 5인 상자)이다.
* 4 ft 로 측정된 것의 넓이는 6(높이가 1, 길이가 6인 상자)이다.

## 넓이에 대한 원칙과 3D 파이차트

아래의 3D 파이차트에서 노란 부분은 초록 부분과 비슷해(보이거나 더 커) 보인다.
하지만 아래의 범례를 보면 실제로는 초록색이 노란색보다 10%p 더 크다.
모든 소프트웨어가 넓이에 대한 원칙을 지키지는 않는다.
그렇기 때문에 그래프를 만든 다음 이를 꼭 확인해야 한다.

![3d-piechart](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2015/08/area-principle-300x229.png)

## 넓이의 원칙과 막대그림(Bar Charts)

막대그림은 수직축이 0 에서 시작하지 않는다면 넓이에 대한 원칙을 위반할 수 있다.
이러한 전략은 언론사에서 실제 상황보다 더 나쁘게 말하기 위해 일반적으로 사용하기도 한다.
아래의 그래프틑 Fox News 에서 가져온 것으로, 부시 정부의 감세 정책이 끝나면 일어날 재앙에 대해 보여주고 있다.
수직축의 시작점이 34인 것에 주목하자.

![bush-cut](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2014/01/Bush_cuts2-300x221.png)

수직축은 주로 좌측에 있고, 0부터 시작한다.
축을 오른쪽에 놓은 것은 어쩌면 굉장히 똑똑한 선택이었을 수도 있다.
일반적인 시청자라면 왼쪽을 먼저 보고 없으면 오른쪽으로 옮겨갈텐데,
그렇게 되면 세금이 "엄청나게" 늘어났다고 볼 것이기 때문이다.
실제로 오른 세금은 4.6%p 정도이다.

출처: [What is the Area Principle?](https://www.statisticshowto.datasciencecentral.com/area-principle-in-statistics/)
