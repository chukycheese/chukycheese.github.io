---
layout: post
title: (번역) Testing Product Ideas Handbook
date: 2023-08-22
toc: true
toc_sticky: true
category: 
    - book-review
tag:
    - book-review
    - product-management
mathjax: true
comment: true
---

## 소개

트위터 (지금은 X가 되었지만...) 에서 [Idea Validation - Much more than just A/B Experiment](https://itamargilad.com/idea-validation-much-more-than-just-a-b-experiments/) 라는 글을 알게 되었고, 글을 읽다 보니 다른 글들과 같이 엮어서 Testing Product Ideas Handbook 이라는 eBook 을 냈다고 해서 냉큼 뉴스레터 가입하고 책을 받아서 읽기 시작했습니다. 여러 개의 블로그 글을 엮은 책이다 보니 40 페이지 정도로 길지 않아서 주말에 잠깐 시간 날 때 읽으면서 정리했더니 한 시간 이내로 걸렸던 것으로 기억합니다.

최근 회사에서 프로덕트팀과 협업을 많이 진행하면서 기능이나 제품 구현부터 관여하는 경우가 생겼고, 이런 방법론들을 알면 도움이 될 것 같아서 겸사겸사 정리를 했고, 책에 담겨 있는 알찬 내용을 모두 정리하기에는 능력이 부족했던 것 같으니 꼭 시간을 내서 책을 읽어 보시길 추천 드립니다. 저는 뒤에 소개할 AFTER 프레임워크 중 가장 첫 단계인 Assessment 부분을 가장 관심있게 읽어서 이 부분만 정리를 해보았습니다. 각자의 관심사가 다르기 때문에 다른 분들은 그 외 부분을 흥미롭게 생각하실 수도 있을겁니다. 길지 않은 책이니 꼭 시간 내서 빠르게 훑어 보시기를 추천드립니다.

## TL; DR

- 최대한 많은 아이디어를 빠르게 평가하는 방법으로 AFTER 프레임워크를 활용해보자
- AFTER 는 Assessment, Fact finding, Tests, Experiments, Release result 의 머릿글자를 따서 만든 프레임워크이다
- 평가를 하는데 있어서 가장 중요한 기준은 가치 (Value) 이다.

## 시작

`"If you want to have good ideas, you must have many ideas. Most of them will be wrong, and what you have to learn is which ones to throw away" -- Linus Pauling`

최대한 많은 아이디어를 살펴 보아야 한다. 그리고, 각 아이디어가 더 깊게 살펴볼 가치가 있는지부터 빠르게 훑어볼 필요가 있다.

빠르게 훑어볼 때 평가할 네 가지 항목은 Value, Feasibility, Usability, Viability 이며, 이에 대한 설명은 다음과 같다.

- Value: 시장에서의 요구가 있는가, 그 크기는 얼마나 되나?
- Feasibility: 합리적인 시간과 비용을 들여서 구현이 가능한가?
- Usability: 사용자들이 쉽고 빠르게 사용할 수 있는가?
- Viability: 사업적으로 합당하고, 현재 사업에 위협이 되지는 않는가?

모든 아이디어에 대해 네 가지 항목을 다 살펴볼 필요는 없다. 다른 항목들보다 가치(Value) 에 우선 순위를 두고 살펴보고, 가치가 낮다고 판단이 되면 다른 항목들은 보지 않고 해당 아이디어는 후순위로 미뤄 두거나, 폐기하는 게 가능하다. 가치를 제외한 나머지 항목들은 어느 정도 타협이 가능하다.

## AFTER 프레임워크

`"If it disagrees with experiment, it's wrong. In that simple statement is the key to science" -- Richard Feynman`

위의 네 가지 항목에 대한 평가를 통과한 아이디어를 조금 더 깊게 살펴보기 위한 방법으로 AFTER 프레임워크를 제안한다. 각 알파벳은, 다섯 가지 항목의 첫 글자를 따서 만들었고, 이는 다음과 같다.

- Assessment: 잠재성과 위험을 빠르게 평가
- Fact Finding: 아이디어의 유효성을 지지하거나, 반대하는 근거 찾기
- Tests: 훨씬 발전된 형태의 아이디어를 사용자에게 보여주고 반응 살펴보기
- Experiments: 양적 실험 수행하기
- Release results: 사용자의 반응을 살펴보면서 더 많은 사용자에게 제품을 보여주기

우리는 앞선 단계에서 아이디어의 가치와 사용성, 구현 가능성, 그리고 사업적인 가능성을 살펴보았다. 이제 우리의 미션은 가장 앞날이 창창해 보이고, 투자를 많이 해야할 아이디어를 정하는 것이다.

이 단계에서도 앞선 단계와 마찬가지로, 모든 아이디어에 대해 다섯 단계를 다 수행할 필요는 없다. 그리고 위에서 말한 다섯 단계는 크게 세 단계로 묶을 수 있다.

![AFTER Funnel](https://itamargilad.com/wp-content/uploads/2021/05/Screenshot-2021-05-23-at-11.53.08-1024x573.png)

많은 아이디어들이 Assessment/Fact Finding 단계에서 탈락할 것이다. 여기서 살아남은 아이디어에 대해서만 Tests/Experiments 단계를 거치고, 또 여기서 살아남은 아이디어만 Release 단계를 거쳐서 최종적으로 런칭 단계까지 도달할 수 있다.

적은 비용으로 쉽고 빠르게 구현할 수 있는 아이디어는 이 퍼널을 빠르게 통과할 것이고, 비용이 많이 들거나 구현이 어려운 아이디어는 느리게 통과하게 될 것이다. 이 과정에서 아이디어 검증과 개발은 병렬적으로 일어날 수도 있으며, 개발 과정에서 범위 (scope)를 축소하여 빠르게 프로세스를 진행할 수도 있을 것이다.

이제 각 단계에 대해서 조금 더 깊게 살펴보도록 하자.

## Assessment

아이디어 평가의 핵심은 외부 연구 없이, 해당 아이디어를 더 진행할 가치가 있는지 빠르게 정하는 것이다. 이 과정에서 해야할 일들에 대해 살펴보자.

### Goals Alignment

- 이 아이디어가 우리의 목표를 달성하는데 도움이 되는가?
- 그게 아니라면, 새로운 목표로 삼아야 하는 것을 다루는가?

위의 두 질문에 대한 대답이 모두 '아니오' 라면, 해당 아이디어는 다음 기회에 살펴보아야 한다. 명확하고 집중된 측정가능한 목표를 가지는 것이 이 단계에서 매우 중요하다. 이를 위해서는 `hierarchical metric tree` 나 `OKRs` 과 같은 기법을 사용하는 것을 추천한다.

---

OKR 은 매우 유명한 방법론이니 추가 설명은 안 하겠지만, `hierarchical metric tree` 는 다소 생소한 개념일 수도 있을 것 같습니다. 저도 얼마 전에 알게된 개념인데, 여러 지표들의 계층 관계를 그리고, 이를 통해 지표들 사이의 관계를 파악하는 방법이라고 합니다. 예를 들어, 회사의 목표가 `2023년 12월 월간 활성 사용자 수 1,000만명 달성` 이라고 했을 때, `월간 활성 사용자 수` 를 조금 더 잘게 나눠 보는 방식입니다. 월간 활성 사용자 수는 전월에도 사용하던 사용자 + 신규 가입 사용자 + 복귀 사용자 로 나눌 수 있을 것이고, 복귀 사용자 수는 휴면 사용자 x 복귀율을 통해 계산할 수 있고, 전월에도 사용하던 사용자는 전전월에도 사용하던 사용자 x 유지율 + 신규 가입 사용자 x 유지율과 같이 나눠볼 수도 있을 것입니다. 그 과정에서 필요 없는 메트릭과 관련된 아이디어에 대한 진행 여부도 같이 판달할 수 있을 것입니다.

여담으로, 이러한 메트릭 트리를 만들고 나서 구성원들과 공유하고, 잘 볼 수 있는 곳에 두는 것이 더 중요한 것 같습니다. 아직 공유를 제대로 하지는 못했지만, 잘 해보려고 준비 중입니다. 이 내용도 끝나는대로 공유해보도록 하겠습니다.

---

### ICE Analysis

![ICE Analysis](https://itamargilad.com/wp-content/uploads/2021/12/Idea-Bank-1024x427.jpg)

ICE Score = Impact x Confidence x Ease

가장 좋은 아이디어는 효과가 크고, 결과에 대해 확신할 수 있고, 자원이 적게 드는 것이다.

- Impact: 시장 또는 회사에 가져올 가치는 얼마인가?
- Confidence: 예상 가치에 대해 얼마나 확신하는가?
- Ease: 얼마나 적은 노력이 필요한가?

ICE Score 자체는 의미가 없다. 이런 평가를 하는 이유는, 아이디어를 보다 체계적이고 편향되지 않은 시각으로 평가하고, 다른 아이디어들과 비교하고, 아이디어에 대한 점수를 기록하기 위해서다.

### Business Modeling

![Business Model Canvas](https://upload.wikimedia.org/wikipedia/commons/thumb/1/10/Business_Model_Canvas.png/2560px-Business_Model_Canvas.png)

비지니스 모델링은 비지니스 모델 캔버스 (The Business Modling Canvas) 라는 도구를 이용할 수 있다.

이 단계에서는 아래와 같은 질문을 할 수 있다.

- (선택) 아이디어가 의미있는 이익을 가져올 것인가?
- 아이디어 구현에 필요한 자원은 있는가?
- 잠재적인 고객에게 다가갈 채널은 존재하는가?

### Assumption Mapping

![Assumption Mapping](https://www.product-frameworks.com/images/assumption_mapping.png)

이번 단계는 불확실성과 중요도를 두 축으로 하는 2차원 그래프 위에 아이디어를 놓는 것이다. 이를 위해서는 각 아이디어에 대해 여러 질문들이 있어야 할 것이고, 이에 대한 대답 또한 존재해야할 것이다.

### Stakeholder / Partner Review

일을 하다보면 이해관계자나 내부 협력자, 또는 내부적인 요인에 의해 아이디어가 좌절되는 일이 발생할 수도 있다. 그렇기 때문에 초기 단계에 이해관계자와 내부협력자를 포함하여 리뷰를 진행하는 것도 좋은 방법일 수 있다.
