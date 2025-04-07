---
layout: post
title: 넷플릭스 게임 사용자의 모험
date: 2025-04-07
toc: true
toc_sticky: true
category: 
    - data-analytics
tag:
    - product-analytics
    - product-growth
mathjax: true
comment: true
---

이 글은 넷플릭스 (Netflix) 에서의 분석 엔지니어링 (Analytics Engineering) 관련 업무의 범위를 공유하기 위한 여러 편의 글 중 두 번째 글이며, 최근에 열렸던 분석 엔지니어링 컨퍼런스에서 발표된 내용이기도 합니다. 더 많은 내용이 궁금하신가요? [첫 번째 글](https://research.netflix.com/publication/part-1-a-survey-of-analytics-engineering-work-at-netflix) 도 확인해보세요. 이 글에서 저희는 몇 가지 흥미로운 비지니스 사례에서의 분석 업무에 대해 공유하고, 마지막 부분에서 기술적인 부분에 대해서도 다루려고 합니다.
### 들어가기에 앞서

원문: [Part 2: A Survey of Analytics Engineering Work at Netflix](https://netflixtechblog.com/part-2-a-survey-of-analytics-engineering-work-at-netflix-4f1f53b4ab0f)

원문은 [넷플릭스의 기술 블로그](https://netflixtechblog.com/) 에 공유되었으며, 넷플릭스 게임과 관련된 여러 글 중 Netflix Games Player's Adventure: Modeled using State Machine 에 대한 부분만 발췌하였습니다.
### 관련 포스트

- [의미있는 지표 (데이터로 제품팀이 집중해야할 것을 뾰족하게 만든 방법)](https://chukycheese.github.io/data-analytics/meaningful-metrics/)
- [듀오링고가 사용자의 성장에 다시금 불을 지핀 방법 - Part 1](https://chukycheese.github.io/data-analytics/how-duolingo-reginited-user-growth-part-1/)
- [듀오링고가 사용자의 성장에 다시금 불을 지핀 방법 - Part 2](https://chukycheese.github.io/data-analytics/how-duolingo-reginited-user-growth-part-2/)
- [듀오링고가 사용자의 성장에 다시금 불을 지핀 방법 - Part 3](https://chukycheese.github.io/data-analytics/how-duolingo-reginited-user-growth-part-3/)
- [듀오링고 그로스 모델에 대한 오해](https://chukycheese.github.io/data-analytics/what-everyone-gets-wrong-about-the-duolingo-growth-model/)

---

## 넷플릭스 게임 사용자의 모험: 상태 기계를 이용한 모델링을 곁들인

넷플릭스 게임에서 저희는 매달 게임을 이용한 사용자의 수를 높이고자 했고, 이를 월간 활성 계정 수 (Monthly Active Accounts; MAA) 라고 정의했습니다. 이 목표를 잘 달성하고 있는지를 평가하고, MAA 를 높일 수 있는 부분을 찾기 위해 저희는 넷플릭스 게임 사용자의 여정을 상태 기계 (state machine) 로 표현하였습니다.

저희는 매일 사용자의 상태 사이의 전환 확률을 보여주는 상태 기계를 추적하였습니다.

![netflix-player's-journey-as-state-machine](https://miro.medium.com/v2/resize:fit:720/format:webp/0*j2wKL4S3ywEs9mpf)

게임 사용자의 여정을 상태 기계로 표현하였더니, 미래의 상태를 시뮬레이션할 수 있었고, 목표 했던 참여 지표를 얼마나 달성했는지도 파악할 수 있었습니다. 가장 기본적인 운영에는 일별 상태 전환 행렬을 현재 상태 값과 곱해서 다음날의 상태 값을 구하는 것이 있습니다.

![basic-operation](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*ud5xnQi9QM6ELiVP)

이 기본적인 운영을 이용하면 다양한 시나리오를 탐색해볼 수 있습니다.

- 변하지 않는 경우: 만약 전환 확률이 동일하기 유지된다고 하면, 일별 상태 전환 확률을 새로운 상태 값에 반복적으로 곱해서 미래의 상태 값을 예측할 수 있으며, 이를 통해 아무런 변화가 없는 상태에서의 연간 목표 수치 달성 정도를 평가할 수 있습니다.
- 동적인 시나리오: 전환 확률을 변경함으로써 복잡한 시나리오에 대한 시뮬레이션을 할 수 있습니다. 예를 들어, 과거 전환 확률에서의 변화를 이용하여 미래 특정 기간 동안의 전환 확률을 변경함으로써 향후의 비슷한 출시 과정에서의 효과를 예측할 수 있습니다.
- 정상 상태 (Steady State): 상태 전환 행렬의 정상 상태를 계산해서 (신규 사용자를 제외하고) 모든 사용자가 넷플릭스 게임에 대한 경험을 했을 때의 MAA 를 추정할 수 있고, 장기적인 리텐션과 재활성 효과를 이해할 수 있습니다.

미래 상태를 예측하는 것을 넘어서, 저희는 상태 기계를 이용하여 어떤 전환 확률이 MMA 에 끼치는 영향이 가장 큰지 민감도 분석 (sensitivity analysis) 를 수행하였습니다. 각 전환 확률를 조금씩 변화시키면서 저희는 MAA 의 변화를 계산하였고, 그 영향을 측정하였습니다. 이 덕분에 저희는 퍼널 윗부분의 개선, 사용자 리텐션, 그리고 재활성 중 어디에 집중해야할지 우선순위를 정할 수 있었습니다.
