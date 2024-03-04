---
layout: post
title: Booking.com 에서의 축차 검정 (Sequential Testing)
date: 2023-11-03
toc: true
toc_sticky: true
category: 
    - data-analytics
tag:
    - hypothesis-testing
    - sequential-testing
    - statistics
    - booking-dot-com
mathjax: true
comment: true
---

원문: [Sequential Testing at Booking.com](https://booking.ai/sequential-testing-at-booking-com-650954a569c7)

## 들어가기에 앞서

- 원문의 저자는 Booking.com 에서 데이터 사이언티스트로 근무하고 있는 Dr. Nils Skotara 입니다
- 아래의 번역된 글은 원문의 저자에게 번역 및 게재 허락은 받았지만, Booking.com 에서 리뷰를 받은 것은 아님을 알려드립니다.
- 저자의 요청으로 일부 수정이 있었습니다.

### 믿을 수 있고 빠른 제품 의사 결정

![image-from-the-author](https://miro.medium.com/v2/resize:fit:640/format:webp/1*zI-2HSlpR4B8LPTKVx6XsQ.png)

## 들어가기

Booking.com 에서 저희는 웹사이트나 모바일 앱에서의 변경이 고객 경험에 긍정적인 영향을 주는지 평가하기 위해 A/B 테스트를 사용합니다. A/B 테스트는 제품에서의 변경이 전환율 (conversion rate) 이나 클릭률 (click through rate)과 같은 특정 지표에 끼친 인과적인 영향을 측정하는 방법 중 하나입니다. 저희는 사용자를 무작위로 두 집단으로 나눕니다. 한 집단은 변경되지 않은 웹사이트를 보게 되며, 다른 집단은 변경된 사이트를 보게 됩니다. 이러한 무작위 배정은 두 집단을 나누는 기준을 제품의 변경사항만으로 한정할 수 있도록 해주며, 결과에 대한 다른 변수들의 영향이 체계적이지 않도록 만들어 줍니다. 덕분에 저희는 두 집단에서 관찰된 차이가 제품 변경에 의한 것이라고 결론을 내릴 수 있게 됩니다.

저희는 통계적 검정을 통해 결과를 분석하며, 그래서 두 가지 사업적 결정 중 하나를 내릴 수 있게 됩니다. 제품의 변경이 긍정적인 영향을 끼쳤기에 배포를 하거나, 그렇지 않았기 때문에 배포하지 않는 것이죠. 통계적 검정은 효과가 없는 변경사항이 잘못 배포되거나 (1종 오류 또는 $\alpha$ 오류), 또는 효과가 있는 변경사항을 배포하지 않는 (2종 오류 또는 $\beta$ 오류) 상황을 통제할 수 있습니다. 많은 경우 가설 검정은 미리 정한 $\alpha$ 와 $\beta$, 그리고 최소 상대 효과 크기 (minimum relevent effect size) 를 가지고, 결정을 내리기 위해서는 얼마나 많은 데이터가 있어야 하는지를 계산함으로써 이루어집니다. 이러한 계산은 미리 행해져야하며, 충분한 데이터가 모일 때까지 (소위 말하는 fixed horizon testing) 기다려야만 합니다. 실무에서 실험자는 보다 빠른 의사결정을 위해 중간 결과를 보고자 하는 욕망을 참는 것은 어려운 일입니다. 결정적으로, 실험 기간을 충실히 지키지 않으면 $\alpha$ 오류가 증가합니다. 축차 검정의 큰 장점은 적절한 $\alpha$ 오류율을 유지하면서도 중간 분석이 가능하다는 것입니다.

흥미롭게도 선행 계산은 우리가 들인 노력이 가치있다고 판단하기 위해서는 사용자에게 어느 정도의 영향이 있어야 하는가와 같은 개인적 견해에 의한 판단 역시 필요합니다. 저희는 이 숫자를 최소 상대 효과 크기, 또는 줄여서 MRE 라고 합니다. 표본의 크기에 대한 계산은 MRE 에 기반하고 있으며, 이는 팀의 이전 실험이나, 사업적인 목표, 또는 성공에 대한 정의에 의해 정해집니다. 이론적으로, 최적의 MRE 를 판단하기 위해서 비용과 효용을 고려할 수도 있습니다. 하지만 실무에서 이는 매우 복잡한 계산이며, 많은 경우 순수한 비용-효용 상충관계 (trade off) 이외의 것들을 고려해야하기도 합니다. 그러므로 MRE 를 정하는 것은 조금은 임의적이라 할 수도 있겠습니다. 게다가, 제품 변경의 실제 영향은 이 MRE 보다 훨씬 더 클 수도 있으므로 계산된 표본의 크기가 목적에 비해 지나치게 커질 수 있습니다. 이러한 잘못된 예측은 귀중한 시간과 자원을 낭비하게 만들어서 제품 커뮤니티와 사업에 결정적인 방식으로 영향을 끼칩니다. 주로 실험이 시작되면 프로덕트 매니저는 미리 정한 표본의 수에 도달할 때까지 기다리고 나서야 비로소 의사결정을 내릴 수 있습니다. 이는 두 가지 이유로 문제가 있다고 생각합니다.

1. 만약 실험 초기에 순조로운 신호를 보더라도, 거짓 양성율이 크게 높아지더라도 보고만 있어야합니다. MRE 의 제멋대로인 특성 때문에 실제 영향이 MRE 를 충분히 상회한다면 초기 신호가 나타날 가능성이 있습니다.
2. 실제 영향이 MRE 보다 훨씬 더 작다면, A/B 테스트는 필요한 표본의 크기가 될 때까지 실험이 진행될 것이고, 실험 기간 동안 영향이 거의 없거나 관계가 있다고 보기에는 미비한 크기의 영향만을 보여줄 것입니다.

위의 두 가지 경우 모두에서 소중한 시간을 낭비하게 됩니다. 실험자는 실험의 성공과 실패를 훨씬 더 빨리 보여줄 수 있음에도 불구하고 결과가 나올 때까지 기다려야만 합니다.

이러한 문제의 해결책은 검정의 결과를 중간에 판별하여 적절하게 대응할 수 있는 기회를 얻을 수 있는 방법들입니다. 이러한 개념의 축차 검정 (sequential testing) 은 Wald (1945) 로 거슬러 올라가며, Armitage el al. (1969) 에 의해 의학 연구에 적용되었습니다. Pocock (1977, 1982) 와 O'Brien and Leming (1979) 은 이 글의 주된 주제인 집단 축차 설계 (group sequential design; GSD) 를 개발하였습니다. GSD 는 의학과 약학 연구에서 다음과 같은 명확한 이유로 인해 널리 사용되고 있습니다. 조기 중단은 많은 환자를 필요로 하지 않고, 가능한 한 가장 빠른 시점에, 가장 많은 환자들에게 더 나은 조치를 취할 수 있고, 강력한 안전 문제가 있는 경우라면 환자들이 불필요하게 역효과를 겪는 것을 방지해줍니다.

하지만 다른 학문 분야나 산업에서는 여전히 많이 쓰이고 있지 않습니다. 저는 이 방법이 대부분의 비지니스 요구사항에 부합한다는 사실과 다른 방법들에 비해 어떤 이점이 있는지 이야기를 하려고 합니다.

## 일반적인 축차 검정에 대한 개요

이 섹션에서 저는 집단 축차 설계 (GSD) 를 대체할 수 있는 방법으로 종종 언급되는 기법들에 대해 대략적인 소개를 하려고 합니다. 뒤에서 살펴보겠지만, 이들은 모두 다른 사용법과 목적을 가지고 있습니다. 그러므로 사업 목적에 따라 다른 방법을 사용해야할 것입니다. 하지만 Booking.com 과 다른 온라인 회사들의 사용 사례는 이론적인 이유뿐만 아니라 실용적인 면에서도 GSD 에 완벽하게 부합합니다.

## 적응 슬롯머신 (Adaptive Bandits)

슬롯머신 (bandit) 방법은 일반적으로 가설 검정과는 다른 목적을 가지고 있습니다. 슬롯머신의 주요 아이디어는 착취 (exploitation) 를 위해 어느 정도의 탐색 (exploration) 을 희생한다는 것입니다 (Gittins, 1979, Bobbins, 1952). 이 기법은 최적의 시간을 들여서 유효한 통계적 결론을 도출하는 것이던 목표를 실험 중 얻은 정보를 이용해서 가장 성능이 좋은 변형(들)에 더 많은 트래픽을 보내고, 진행하는 동안 이득을 취하는 것으로 바꾸었습니다. 대표적인 사례로는 온라인 뉴스 기사의 헤드라인을 바꿔서 효과를 비교하는 것이 있습니다. 이 실험에서 독자는 며칠이 지나면 흥미를 잃을 가능성이 높기 때문에 신뢰 구간이나 위양성률 (false positive rate) 을 통제할 필요가 없습니다. 충분한 확률로 가장 좋은 버전을 정하고, 클릭률 (click through rate) 을 최대화하는 변형에 더 많은 트래픽을 할당하는 것이면 충분합니다.

유효한 통계적 결론을 내야하는 상황에서 밴딧 알고리즘 (bandits) 은 필요한 표본의 크기에 대한 측면에서도 차선의 성능을 보여줍니다. 게다가 적응 슬롯머신은 계통적인 편향 (Nie, 2017) 을 겪기도 합니다. 과하게 낙관적인 점 추정치를 보여주는 변형들이 더 많은 트래픽을 부여받는 반면, 그 반대인 변형들은 훨씬 적은 트래픽을 할당 받습니다. 그러므로 표본 오차 (sampling error) 는 데이터 수집에 직접적인 영향을 주고, 더이상 서로 상쇄 되지도 못합니다.

## 항상 유효한 유의확률 (Always valid p-values)

신뢰 구간의 유효성을 희생하지 않고 계속해서 결과를 살펴면서 위양성률을 통제하기 위한 노력으로 항상 유효한 유의확률 (Lindon et al., 2022, Ramesh et al. 2019) 은 괜찮은 대안입니다. 항상 유효한 유의확률은 검정력 (power) 과 실행 시간 사이에서 괜찮은 트레이드오프를 얻을 수 있게 해줍니다. 이 글에서 저는 Optimizely, Uber, Netflix, 그리고 Amplitude 에서 사용하고 있는 혼합 축차 확률비 검정 (mixture sequential probability ratio test; **mSPRT**, 줄여서 **sprt**) 에 대해 다뤄보려고 합니다.

이 기법을 사용하면 실험을 지속적으로 살펴볼 수 있고 최대 표본 크기를 정하지 않고도 언제든지 추론을 도출할 수 있습니다. 이 기법은 매우 강력한 검정 프레임워크이긴 하지만, 대부분의 실제 사례에서 최대 표본 크기를 정해 놓는 것은 도움이 됩니다. Booking.com 에서 저희가 겪은 거의 모든 사례에서, 제품 팀은 의사 결정을 위한 유효한 통계적 결과를 얻기 위해서 얼마나 기다려야 하는지 알고 싶어 합니다. Spotify 와 그들이 작성한 [블로그 글](https://engineering.atspotify.com/2023/03/choosing-sequential-testing-framework-comparisons-and-discussions/) 를 보고 저희는 보다 일반적인 방법의 항상 유효한 유의확률 (Howard et al. 2022) 을 고려하였고, 이는 현재 Eppo 에서 사용하고 있는 항상 유효한 유의확률의 일반화 (**gavi**) 라고 부릅니다.

항상 유효한 유의확률은 정확한 통계적 특성을 가지고 있고, 대응하는 신뢰 구간에 대한 공칭 커버리지 속성 (nominal coverage property) 을 지니고 있습니다. 비록 흔히 간과하는 미묘한 측면으로는 해당 기법이 유효한 의사 결정 과정을 제공해주지는 않는다는 점입니다. 이는 두 가지 이유 때문입니다.

- 1종 오류는 신뢰 구간이 최초로 0을 포함하는 바로 그 시점에 사용자가 실험을 종료해야지만 맞기 때문입니다
- 게다가 이러한 검정이 결국에는 표본의 크기가 매우 커지면 1에 가까운 검정력을 주지만, 이는 표본의 크기가 매우 크면 어떤 검정이더라도 큰 검정력을 보여주기 때문에 의미있는 속성은 아니기 때문입니다. 그러나 표본의 크기가 무한히 클 수는 없습니다. 그렇기 때문에 표본의 크기가 유한하다면 사실상 검정력을 통제하는 것은 불가능합니다.

## 추가적인 분분석

Statsig (2023년부터 StatSig 로 변경) 와 같은 회사들에서는 표본의 크기에 맞춰서 표준 오차 (standard error) 를 크게 하는 간단한 조정을 취하는 방식을 사용합니다. 표본의 크기가 작을수록 표본 오차는 커집니다. 이는 고정 기간 검정 (fixed horizon test) 의 매 중간 분석을 단순히 보는 것에 비해 축차 분석에서의 위양성률의 증가를 부분적으로 낮출 수 있습니다. 하지만 이 방법도 계통적인 접근 방법이 결여되어 있고, 유의수준 또한 특정 설정에 의존적입니다.

## 집단 축차 설계 (Group Sequential Design)

이 글이 중점적으로 보고자하는 내용은 집단 축차 설계 (Group Sequential Design) 로, 반복 유의성 검정의 한 갈래입니다. 이 방법의 가장 중요한 부분은 오류율을 미리 정의한 함수에 따라 (error-spending functions, Lan and DeMets 1983) 실험 과정에서 소비되는 자원으로 본 것입니다. 여기서의 아이디어는 특정 중간 분석 체크포인트까지 소비된 원하는 유의 수준의 비율을 특정하는 것인데, 이 방법은 수정된 유의 수준의 형태를 직접 정하는 다른 대안들에 비해 많은 이점이 있습니다. 가장 중요한 것은 각 체크포인트에서의 표본의 크기이며, 체크포인트의 정확한 갯수조차도 미리 알아야할 필요도 없었습니다. 그저 실험을 종료할 때 최대 표본의 크기만 정하면 됐습니다 (Lakens, 2021). 오류 소비 함수 (error-spending function) 은 상한과 하한과 같은 결정 경계를 한두 개 정도 정할 수 있습니다. 검정통계량이 상한을 넘을 때 귀무가설은 기각되고, 검정통계량이 하한에 미치지 못한다면 해당 실험은 무위로 돌아가고, 귀무가설은 기각할 수 없습니다 (추가: 원문에서는 accpect the null hypothesis 라고 되어 있지만, 귀무가설은 채택의 대상이 아니기 때문에 기각할 수 없다고 번역하였습니다). 집단 축차 설계에서는 구속력이 있는 경계값 (binding bounds) 을 사용할 수 있는데 (Wassmer, 2016), 한 번 경계값을 넘어서면 결정을 번복할 수 없습니다. 구속력이 없는 경계 (non-binding bounds) 는 실험을 지속할 수 있는 선택지를 부여하기도 하고, 이후에 결정을 뒤엎을 수도 있습니다. 비지니스의 맥락에서 구속력이 있는 경계를 선호하는데, 이는 해석의 여지가 없이 명확하고 잘 정의된 결정 프레임워크를 제공하기 때문입니다. 게다가, 평균과 최대 지속 시간에 대한 명확한 기대값을 제공해주기도 합니다. 이러한 사실 덕분에 특정 표본의 크기마다 확인하는 게 아니라 매일 확인할 수 있는 것이 자연스러운 온라인 실험에 더 매력적으로 다가오는 이유입니다.

또한 GSD 를 이용하면 유효한 신뢰 구간을 계산하는 것도 가능합니다 (Wassmer, 2016). 정확한 신뢰 구간을 구하는 방법은 기본적으로 두 가지가 있습니다. 한 방법은 실험이 완전히 종료되었을 때에만 계산이 가능하며, 미리 정의된 종료 규칙에 종속되어 있습니다. 이 방법을 최종 신뢰 구간 (final confidence intervals) 이라고 부르기도 합니다 (Wassmer, 2016). 다른 방법은 추가적인 체크포인트의 갯수로 인해 늘어난 통계적 오차가 어느 정도인지만 고려합니다. 이는 반복 신뢰 구간 (repeated confidence interval) 이라고도 하며, 연구자가 미리 실험을 종료할 수 있었음에도 (또는 해야 했음에도) 종료하지 않는 결정을 내리더라도 여전히 유효합니다. 이 방식은 유효한 신뢰 구간과 함께 추가적인 데이터 수집이 요구되는 임상 실험 (clinical trial) 에서 특히 유용한 방법입니다. 초기에 유효한 효과를 보인 특정 약물을 정량적으로 모니터링 해야하거나, 여러 종료 시점에 대해 가치있는 연구가 여전히 남아있는 경우를 예를 들 수 있겠습니다.

## 경험적인 비교

경험적인 비교는 다음과 같은 기법들을 수반합니다.

- Booking.com 에서 사용하는 것과 같은 집단 축차 설계 검정 (Group Sequential Design Test; gst)
- Spotify 에서 사용하는 집단 축차 설계 검정 (Group Sequential Design Test; gst_spot)
- Eppo 에서 사용하는 일반화한 Always Valid Inference (Generalization of Always Valid Inferece; gavi)
- Optimizely, Uber, Netflix, 그리고 Amplitude 에서 사용하는 (혼합된) 축차 확률비 검정 (Sequential Probability Ratio Test; sprt)
- StatSig 에서 사용하는 단순한 임시 유의수준 수정 (Simple ad-hoc alpha correction; ss)

저는 1,000번이 넘는 A/B 테스트를 시뮬레이션 해보았습니다. 모든 모의 A/B 테스트는 위에서 언급한 5가지 방법을 모두 사용해서 다양한 시점에 중간 분석을 진행하였고, 실험군과 대조군에 할당된 사용자는 1,000명이었습니다.

- gst 와 gst_spot 은 매 200명의 방문자 마다 중간 분석을 실시하여 총 5번의 계산을 하였습니다
- gavi, sprt, 그리고 ss 는 매 방문자마다 중간 분석을 실시하여 계산하였습니다 (첫 방문자만으로는 표준편차를 계산할 수 없기 때문에 최대 999번)

이러한 환경은 정규분포를 따르는 데이터를 이용해서 4가지 기저 처치 효과 (0 또는 효과 없음, 0.09, 0.13, 0.17) 의 시나리오에 사용되었습니다. 이는 각각 검정력 5%, 64%, 90%, 그리고 98% 에 해당합니다. 그러므로 각 기법에 대해 총 4,000 번의 A/B 테스트를 분석하였습니다. 효과가 없는 시나리오의 경우 5% "검정력" 은 명목상의 위양성률인 유의수준 ($\alpha$) 와 같습니다. 저는 아래의 세 가지 항목에 대해 분석을 진행하였습니다.

- 위양성률 (False Positive Rate): 5% 위양성률은 1,000번의 A/B 테스트 시뮬레이션에서 50번의 양성 결과를 의미합니다
- 검정력 (Power): 80% 진양성률 (true positive rate) 은 1,000번의 A/B 테스트 시뮬레이션에서 800번의 양성 결과를 의미합니다
- 필요한 표본의 크기 (Required sample size): 이는 어떤 기법에서 신뢰 구간이 처음으로 0을 넘는 순간과 같은 확정적인 결론에 도달할 수 있는 표본의 크기를 의미합니다

결과를 살펴보기에 앞서 다음 그림 (그림 1) 을 먼저 살펴보도록 하겠습니다. 이 그림은 시간의 경과에 따른 신뢰구간이 어떻게 변화하는지를 보여줍니다. Booking.com 에서 사용했던 집단 축차 설계의 의사결정 시점에서이 최종 신뢰구간은 어두운 파란색으로 나타냈고, Spotify 에서 사용한 방법의 최종 신뢰구간은 밝은 파란색으로 나타냈습니다. 우리는 여기서 두 방법이 모두 항상 유효한 기법 (gavi) 에 비해 충분히 작은 신뢰구간을 보여주는 것을 확인할 수 있습니다. 앞서 언급한 것처럼, 집단 축차 설계의 신뢰구간은 수정된 명목 범위 (correct nominal coverage) 를 제공합니다 (Wassmer, 2016). 임시 유의수준 수정 기법 (ss) 의 신뢰구간은 초기에는 매우 넓고 축차 검정의 마지막에는 매우 좁아집니다.

![그림 1](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*bgn74vIzXd5Hc59m0_coHg.jpeg)
**그림 1**. 시간의 경과에 따른 다양한 기법들의 신뢰구간

## 위양성률과 검정력

집단 축차 설계 방법은 지금까지 가장 높은 검정력을 보여줬습니다 (표 1과 그림 2 참조). Booking.com 에서 사용하는 GST 방법의 경우 고정 기간 검정 (fixed horizon test) 와 거의 비슷한 수준에 이르렀습니다. Spotify 에서 사용하는 GST 설계의 경우 두 가지 경우의 중간 크기의 효과에 대해서는 약 6-8%p 정도 낮은 검정력을 보였습니다. 그 다음 두 후보인 gavi 와 sprt 는 모든 시나리오에 대해 상당히 낮은 검정력을 보여주었습니다.

![표 1](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*hL_YSugDBqxb4oCqnuk3eg.png)

**표1**. 다양한 방법과 효과에 대한 실질 검정력 (또는 **위양성률**). 첫 번째 열은 실제 효과 (A/B 테스트에서 실험군과 대조군 사이의 차이) 가 없는 경우에 해당한다. 따라서 위양성률을 제대로 통제하지 못하는 ss 기법을 제외하고는 모든 기법에서 그 값은 이론적으로 0.05 가 되어야 한다. 0.05 에서 조금 벗어난 값을 가진 이유는 시뮬레이션에서의 표본오차에 의한 것이며, 횟수를 거듭한다면 평균값은 0.05로 회귀할 것이다.

흥미롭게도 ss 기법은 위양성률을 크게 증가시키며, 따라서 이 방법에서의 검정력은 직접 비교하기 어렵습니다.

![그림 2](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*R1YgHrFi18FhtxYjFJNccA.jpeg)

**그림 2**. 네 가지 효과와 모든 기법에 대한 검정력. 제대로 된 위양성률을 보여주지 못하는 ss 기법을 제외하면, Booking.com 에서 사용하는 gst 는 고정 기간 검정에 가장 가까운 검정력을 보여준다. Spotify 에서 사용하는 gst 는 약 6-8%p 정도 낮다. 항상 유효한 유의확률 기법 (gavi) 과 sprt 기법은 실험한 모든 효과에 대해서 매우 낮은 검정력을 보여준다.

## 표본의 크기 (Sample size)

그림 3과 4는 X 축에는 실험을 종료하는데 필요한 표본의 크기의 누적 분포를 나타냈고, 출현 빈도는 Y 축에 나타냈습니다. 보다 효과적인 표현을 위해 커널 밀도 추정 (kernal density estimation) 을 이용하여 그래프를 자연스럽게 이어지도록 했습니다.

![그림 3](https://miro.medium.com/v2/resize:fit:720/format:webp/1*-h6FQgBFs779fag8fzdJ_A.jpeg)
**그림 3**. 각 기법과 효과에 대해 필요한 표본의 크기의 누적 분포. 필요한 표본의 크기의 중위수를 점으로 표기했다. 중위수는 Y 축의 0.5에 대응해야하는 값이다. 그럼에도 불구하고 그렇지 않은 경우가 보이는 이유는 분포 추정에 대한 평활화 효과 때문이다. 중위수의 자격을 갖춘 다른 값들이 있는 경우, 정확한 Y 값은 평활화에 의해 정해진다.

아래의 표 2에서 알 수 있듯이, 가장 빠르게 종료되는 기법은 Booking.com 에서 구현한 gst 입니다. 특히나 놀라운 점은 다른 기법들과 비교했을 때 거의 균등 분포에 가까운 (균등 분포의 누적 밀도는 선형적으로 증가합니다) 모양의 초기 중단에 필요한 표본의 크기인데, 효과가 없는 경우에 더욱 눈에 띕니다.

![표 2](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*denaX8s1KCU4yUyn2jQcXg.png)

**표 2** 다양한 효과와 기법들에 대해 해당 효과를 검출하기 위해 필요한 표본의 크기의 중위수

대부분의 경우에 있어서, 개입의 영향이 없는 경우가 실험의 많은 부분을 차지하는데, 제품 개발의 속도에 있어서 이는 다른 기법들에서 얻을 수 없는 매우 중요한 이점입니다.

![그림 4](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Sk1SHg8MuGLp3E4gR8ZfPw.jpeg)

**그림 4**. 각 기법과 효과에 대해 필요한 표본의 크기의 누적 분포. 필요한 표본의 크기의 중위수를 점으로 표기했다. 중위수는 Y 축의 0.5에 대응해야하는 값이다. 그럼에도 불구하고 그렇지 않은 경우가 보이는 이유는 분포 추정에 대한 평활화 효과 때문이다. 중위수의 자격을 갖춘 다른 값들이 있는 경우, 정확한 Y 값은 평활화에 의해 정해진다.

## 정리

집단 축차 설계 (GSD) 는 일별 보고서와 같이 데이터가 배치 (batch) 로 들어오는 상황에 특히 더 적절합니다. 비지니스의 관점에서 A/B 테스트의 수행 시간의 상한을 정하는 것은 바람직한 행위입니다. 집단 축차 설계는 최대 표본의 크기에 도달했을 때 결정적인 (decisive) 결과를 보장하기 때문에, 계획한 기간 내에 통계적으로 유효한 결론을 항상 내릴 수 있습니다. 반면에, 만약 실시간으로 데이터를 분석하거나, 정해지지 않은 시점까지 제품의 어떠한 변화에 대해 분석을 해야한다면, 이런 경우에는 항상 유효한 신뢰구간 (always valid confidence intervals) 을 제공해주는 기법이 보다 적절할 것입니다.

이 글에서 다뤘던 모든 유효한 통계적 기법들 (Booking.com 의 gst, Spotify 의 gst, gavi, sprt) 은 위양성률을 적절히 제어할 수 있습니다. StatSig 의 *ad hoc* 기법은 수정된 위양성률을 보장하지는 못합니다. 검정력과 평균적으로 요구되는 표본의 크기에 대해서, 두 가지 방법의 집단 축차 설계 기법의 성능은 다른 기법들을 크게 상회합니다. Booking.com 의 설계는 효과가 없는 상황에서도 조기 종료가 가능하다는 추가적인 장점이 있습니다.

또 최소 상대 효과 (Minimum Relevant Effect) 를 사전에 (*a priori*) 설정하는 것은 매우 어렵기 때문에 고정 기간 검정에 비해 축차 검정의 실용적인 이점은 단순히 위양성률과 통계저 검정력만으로 그 효과를 평가하는 것보다 훨씬 크다고 할 수 있습니다. 고정 기간 검정은 해당 검정이 설계된 영향을 정확하게 수정한 경우에만 제대로된 검정력을 얻을 수 있습니다. 그렇지 않으면 해당 검정은 훨씬 더 적은 수의 표본으로도 할 수 있었거나, 시작부터 가망이 없는 노력이 될 수도 있습니다. 저희는 Booking.com 에서 사용하는 집단 축차 설계 덕분에 제품의 변화가 큰 효과가 없던 대부분의 경우에 소중한 개발 시간을 아낀 경우를 많이 보았습니다. 집단 축차 설계 덕택에 제품 개발 사이클의 신뢰도와 속도를 크게 향상시킬 수 있었습니다.

## 수정한 내용

수정 되기 전의 글에는 ss 기법의 위양성률을 0.18 이라고 잘못 표기했습니다. 제대로 된 위양성률은 0.08 입니다. 코드에서의 오류에 의한 것임을 밝힙니다. 이에 대응하는 검정력 또한 수정하였습니다. 그 이후 StatSig 에서는 축차 검정 [기법](https://statsig.com/blog/sequential-testing-on-statsig)을 개편하였습니다. 새로운 접근법은 통계적 검정력을 개선하였고, 제대로 된 위양성률을 계산할 수 있게 되었습니다.

## 참고 문헌

- Armitage, P., McPherson, C. K., & Rowe, B. C. (1969). Repeated significance tests on accumulating data. Journal of the Royal Statistical Society A, 132, 235–244.
- Gittins, J. C. (1979). [Bandit Processes and Dynamic Allocation Indices](https://rss.onlinelibrary.wiley.com/doi/10.1111/j.2517-6161.1979.tb01068.x). Journal of the Royal Statistical Society. Series B (Methodological). 41 (2): 148–177. doi:10.1111/j.2517–6161.1979.tb01068.x. JSTOR 2985029. S2CID 17724147.
- Howard, S. R., Ramdas, A., McAuliffe, J., Sekhon, J.(2022). [Time-uniform, nonparametric, nonasymptotic confidence sequences](https://arxiv.org/pdf/1810.08240.pdf). arXiv 1810.08240
- Lakens, D., Pahlke, F., & Wassmer, G. (2021). [Group Sequential Designs: A Tutorial](https://osf.io/x4azm/).
- Lan, K. K. G., & DeMets, D. L. (1983). Discrete sequential boundaries for clinical trials. Biometrika, 70, 659–663.
- ​​Lindon, M., Ham D. W., Tingley M., Bojinov, I.(2022). [Anytime-Valid F-Tests for Faster Sequential Experimentation Through Covariate Adjustment](https://arxiv.org/pdf/2210.08589.pdf). arXiv 2210.08589
- Nie X., Tian X., Taylor, J., Zou J. ( 2017). [Why Adaptively Collected Data Have Negative Bias and How to Correct for It](https://arxiv.org/pdf/1708.01977.pdf). arXiv:1708.01977
- O’Brien, P. C., & Fleming, T. R. (1979). A multiple testing procedure for clinical trials. Biometrics, 35, 549–556.
- Pocock, S. J. (1977). Group sequential methods in the design and analysis of clinical trials. Biometrika, 64, 191–199.
- Pocock, S. J. (1982). Interim analyses for randomized clinical trials: The group sequential approach. Biometrics, 38, 153–162.
- Ramesh J., Pekelis L., Walsh D. (2019). [Always Valid Inference: Continuous Monitoring of A/B Tests](https://arxiv.org/pdf/1512.04922.pdf). arXiv: 1512.04922
- Robbins, H. (1952). [Some aspects of the sequential design of experiments](https://www.ams.org/journals/bull/1952-58-05/S0002-9904-1952-09620-8/). Bulletin of the American Mathematical Society. 58 (5): 527–535. doi:10.1090/S0002–9904–1952–09620–8.
- StatSig (2023). Documentation about [Sequential Testing](https://docs.statsig.com/experiments-plus/sequential-testing).
- Wald, A. (June 1945). [Sequential Tests of Statistical Hypotheses](https://projecteuclid.org/journals/annals-of-mathematical-statistics/volume-16/issue-2/Sequential-Tests-of-Statistical-Hypotheses/10.1214/aoms/1177731118.full). Annals of Mathematical Statistics. 16 (2): 117–186.
- Wassmer, G., Brannath, W. (2016). [Group Sequential and Confirmatory Adaptive Designs in Clinical Trials](https://link.springer.com/book/10.1007/978-3-319-32562-0). Springer Series in Pharmaceutical Statistics.

## 감사의 글

이 글을 쓰는 동안 소중한 피드백을 제공해 준 [Kostas Tokis](https://medium.com/@tokiskostas), [Sam Clifford](https://medium.com/@sj.clifford), Guy Taylor, [Kelly Pisane](https://medium.com/@kelly.pisane) 께 감사의 글을 남깁니다.
