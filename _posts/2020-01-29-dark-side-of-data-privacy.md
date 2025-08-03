---
layout: post
title: (번역) 데이터의 어두운 면 - 개인정보 (Dark Side of Data:Privacy)
date: 2020-01-29 00:30:00
toc: true
toc_sticky: true
category: data-ethics
tag:
    - data-privacy
    - translation
    - data-ethics
mathjax: true
comment: true
---

원문: [Dark Side of Data: Privacy](https://towardsdatascience.com/dark-side-of-data-privacy-ba2850de512) by Emre Rencberoglu

AI 와 머신 러닝의 가치는 높이 평가하지만, 개인정보의 측면에서는 어떨까요?

![A photo of a covered webcam](https://miro.medium.com/max/2686/1*JGDVK805U0qFNAODNbtrNQ.png)

최근 일상 생활에서 **구글 글래스 (Google Glass)** 를 쓰는 사람을 보셨나요? 아마 몇 년이 더 지나면 이 질문은 그 제품을 아는 사람이 있는지를 묻는 것으로 바뀔 겁니다. 구글 글래스의 이야기에 대한 일반적인 의견은 이를 [비즈니스적 실패](https://www.wired.com/story/google-glass-reasonable-expectation-of-privacy/) 로 인지하는 것인데, 우리가 이 실패의 개인정보 측면을 무시하는 우를 범하지 않는다면 합리적인 추론입니다.

개인의 데이터에 대한 사생활 침해 문제는 오늘날 10년 전보다 더 심해졌으며, 계속해서 증가하고 있습니다. 하지만 이게 진정으로 대기업 제품의 매력적인 기능에도 불구하고 이를 무너트릴 정도의 수준일까요?

저는 우리 사회에서 개인정보의 개념이 만족할만한 수준에 도달했다는 사실에는 강력한 의문을 품고 있습니다. 기술은 빠르게 발전하고 이러한 발전에 뒤따르는 영향은 수년이 지나야 나타납니다. 우리 모두는 **AI** 와 **머신 러닝** 의 가치를 높이 평가합니다만, 이 모든 데이터의 개인정보에 대한 측면은 어떤가요? 저는 이를 **데이터의 어두운 면** 이라고 부르며, 특히 데이터에 기반해서 일을 하는 사람들은 여기에 큰 책임을 가지고 있다고 생각합니다.

## 현대에서의 개인정보

개인정보는 [Warren 과 Brandeis](https://groups.csail.mit.edu/mac/classes/6.805/articles/privacy/Privacy_brand_warr2.html)가 1890년에 처음으로 설명했습니다. 그들의 글에서 개인정보는 **"방해받지 않을 권리"** 로 정의되었습니다. 그 당시의 세상은 지금과 달랐고, 이 정의를 주장할 때 사진기기와 신문이 사용되었습니다. 오늘날에도 이는 유의한 주장이지만, 현대의 개인정보 개념의 관점을 표현하기에는 충분하지 못한 것이 사실입니다.

현대에는 개인정보를 정의하는 것이 훨씬 더 복잡해졌습니다. 사실 이전보다 더욱 모호해졌습니다. 기술의 이점과 더불어 우리는 최신 발전의 부작용을 가까이 마주하고 있습니다. ***푸코(Foucault)*** 의 책 ***감시와 처벌: 감옥의 탄생 (Discipline and Punish: The Birth of Prison)*** 에서 설명되었듯이, 사람들이 감시 하에 있다는 것만으로도 새로운 아이디어를 만드는 것을 막고, 자신에게 의문을 던지고, 사회에서 자기 검열을 불러오며, 이는 강압적인 정권이 사회를 쉽게 지배할 수 있는 적당한 환경을 만들도록 도와줍니다.

![A panopticon (A prison design by Jeremy Bentham, who inspired Foucault)
](https://miro.medium.com/max/1510/0*qzmSbsZFOi-vmURB.png)

그렇다면 우리 스스로를 보호하기 위해 기술을 더이상 사용하지 말아야 할까요? 이토록 기술에 중독된 세상에서 그렇게 하기란 말처럼 쉽지가 않습니다. 몇 가지 사례에 대해 생각해 봅시다. 사생활 침해의 관점에서 아래의 기계에 여러분들은 어떻게 반응하실 건가요?

* 집 주변의 **CCTV** 카메라 - *이것이 테러리스트의 공격을 예방해준다면?*
* 여러분의 전화기에 달린 **위치 추적기** - *자연재해에서 여러분들을 구해준다면?*
* 시계의 **심박 측정기** - *심정지가 오기 전에 경고를 보내준다면?*
* TV에 달린 **음성 인식장치** - *여러분이 찾는 제품을 추천해준다면?*

네, 마지막 것은 그렇게 필수적일 것 같진 않지만, 모든 것들에는 개인마다 다른 정도의 장단점이 있고, 자신의 데이터에 대해 의식적인 결정을 내리기 위해서는 일정 수준의 경각심은 필수입니다. 여러분의 일상 생활에서 얻는 수많은 기술적인 이점들을 생각하더라도 여전히 한 가지 의문이 남습니다. 우리의 민감한 개인정보를 이기적인 기술 회사들, 공격적인 정부, 또는 실용주의자 해커들로부터 지켜줄 사람은 누구일까?

<font size="5" color="grey"> 개인정보를 지키는 것은 힘들다. 왜냐하면 한 번만 실수하더라도 영원히 남기 때문이다

— 애런 슈워츠 </font>

**캠브리지 애널리티카 (Cambridge Analytica)** 와 같은 곳이 데이터의 윤리적인 측면에 대해 사회의 관심을 모은 최근의 사례를 보면 명백하다. 탯 터크 (Matt Turck) 는 이를 [2019 Data & AI Landscape](https://mattturck.com/data2019/) 보고서에서 설명했다.

> *그 어느때보다 심하게 개인정보 문제는 2019년 공개 토론의 최전선으로 뛰어들었으며, 이제는 사방에 존재한다. ... 사생활과의 관계는 계속해서 복잡해지고 있다. [사람들은 개인정보에 신경쓰고 있다](https://www.internetsociety.org/wp-content/uploads/2019/05/CI_IS_Joint_Report-EN.pdf)고는 하지만 개인정보 보호가 불확실한 다양한 커넥티드 단말기 (connected device) 를 구매한다. 그리고 페이스북의 개인정보 위반에 분노하지만, 페이스북은 계속해서 사용자를 늘리며 예상치를 경신하고 있다 ([2018년 4분기](https://www.cnbc.com/2019/01/30/facebook-earnings-q4-2018.html) 와 2019년 1분기 모두)*

![who-watches-the-watchmen](https://miro.medium.com/max/1000/0*3l00nWr5zdQU5x_W.jpg)

## Quis Custodiet Ipsos Custodes?

위의 [멋진 문구](https://en.wikipedia.org/wiki/Quis_custodiet_ipsos_custodes%3F) 는 로마의 시인 유베날리스 (Juvenal) 이 한 말이며 **"누가 파수꾼을 지키는가?"** 로 번역할 수 있습니다. 저는 정부와 공공 기관과 같은 개인정보보호 당국들 간의 상호 의존성을 강조하기 위해 해당 문구를 사용합니다.

오늘날까지, 모든 종류의 데이터와 관련된 행위는 모두 **GDPR** 과 같은 법적 규제에 달려 있었으며, 이러한 규제가 개인정보 보호를 위한 노력으로써는 큰 걸음이지만, 확실한 해결책이라고는 할 수 없습니다.

반면에 [**Privacy International**](https://www.privacyinternational.org/) 같은 재단은 사람들을 모집하고 데이터에 대해 공통 윤리를 만드는 역할을 하는 데에 있어서 매우 중요합니다. 게다가 데이터 관련 분야의 관심이 커진 덕분에, 일부 기관들은 이러한 카프카적인(kafkaesque, 부조리하고 절망적인) 환경을 정화하기 위해 자신들만의 윤리 강령을 공개하기도 합니다.

그러나 사생활 보호에 관한 이러한 기관과 대중 운동만으로는 충분하지 못합니다. 이러한 노력들은 데이터 산업 한 가운데에 있는 종사자들의 실행과 지원을 요구한다고 생각합니다. 이 분야에 종사하는 모든 사람들은 스스로의 업무에 책임을 져야합니다.

[DJ Patil (전 미 백악관 최고 데이터과학자)](https://twitter.com/dpatil) 은 [데이터 과학에서의 도덕 규범](https://medium.com/@dpatil/ethics-data-science-ff21d0c29346)을 5가지 C 로 설명합니다:

* 동의 (Consent)
* 명확성 (Clarity)
* 일관성 (Consistency)
* 통제와 투명성 (Control & Transparency)
* 결과와 해악 (Consequences & Harm)

여러분이 데이터에 얼마나 깊이 깊이 관여를 하건 이러한 데이터 과학 규범에 주의를 기울이는 것은 데이터 프라이버시를 수립하고, 모두의 인권을 존중하며 여러분의 업무를 진행할 수 있도록 만들어줄 것입니다

유럽 연합에서 발행한 [신뢰할만한 AI를 위한 윤리 가이드라인](https://ec.europa.eu/futurium/en/ai-alliance-consultation) 보고서는 인권의 가치와 그것과 인공지능과의 관계를 강조합니다.

> 도덕적인 가치와 모든 인류에 대한 존엄성을 동등하게 존중해야만 합니다. 이는 객관적인 정당화에 기반한 서로 다른 상황을 구별 짓는 것을 허용해야한다는 비차별을 넘어서야 합니다.

뿐만 아니라 동일한 보고서에서 인공지능의 프라이버시 부분에 대해서도 언급이 되었습니다:

> 인공지능 시스템은 해당 시스템의 전체 라이프사이클에 대해서 프라이버시와 데이터 보호를 보장해야만 합니다. ... 사람의 행동에 대한 디지털 기록 덕분에 인공지능 시스템은 개인의 선호 뿐만 아니라 성적 지향, 연령, 젠더, 종교, 또는 정치적 견해에 대해서도 추론할 수 있습니다. 개인이 데이터 수집 과정을 신뢰할 수 있도록 하려면, 수집된 데이터가 자신들을 불법적으로 또는 불공정하게 차별하는 데에 사용되지 않는다는 것을 보장해줘야 합니다.

## 인류의 가장 오래된, 가장 강력한 감정

이 글에서 저는 프라이버시 침해의 해악에 대해서 이야기하는 대신, 의식이 있는 사람의 **윤리적인 책임** 에 대해 이야기하려고 했습니다. 물론 윤리적인 행위와 그렇지 않은 행위를 판단하는 것이 경우에 따라 다르기 때문에 굉장히 어렵다는 것을 저는 알고 있습니다. 어쨌든 간에, 윤리적 가이드라인은 우리에게 로드맵을 제공해주고, 우리의 업무가 인권과 데이터 프라이버시를 존중하도록 만드는 것은 우리의 의무입니다. 저는 이러한 의무가 재화보다 앞선다고 생각하고 있으며, 그렇기 때문에 누군가가 여러분에게 이를 어길 것을 요구한다면 이를 거부할 능력을 가지고 있어야만 합니다.

<font size="5" color="grey">

인류의 가장 오래되고 가장 강력한 감정은 공포이며, 가장 오래되고 가장 강력한 공포는 미지의 것에서 오는 공포이다. - H.P. 러브크래프트

</font>

## 결론

우리 모두는 방대한 양의 데이터 소스에 접근하고, 이러한 기술적인 기회를 쉽게 이용할 수 있도록 해주는 강력한 머신러닝 툴을 이용해서 업무를 하고 있습니다. 그러나 우리는 이러한 능력은 책임을 동반하며, 데이터 윤리는 이 분야에서는 불가분한 것임을 명심해야만 합니다. 즉, 우리는 미지의 것을 최소화하고 우리의 가장 강력한 공포와 맞서 싸워야 합니다.

### 해당 분야에 대한 추가적인 읽을 거리들

* [OECD Principles on AI](https://www.oecd.org/going-digital/ai/principles/)
* [The Declaration — Montreal Responsible AI](https://www.montrealdeclaration-responsibleai.com/the-declaration)
* [AI Ethics: Seven Traps](https://freedom-to-tinker.com/2019/03/25/ai-ethics-seven-traps/) by Annette Zimmermann and Bendert Zevenbergen
* [Privacy Is the New Digital Divide](https://onezero.medium.com/privacy-is-the-new-digital-divide-e06f6e5ca7fe) by Stephane Lavoie
* [Zeynep Tüfekçi](https://twitter.com/zeynep) 를 팔로우 하는 것을 강력히 추천합니다. 해당 주제에 대한 그의 글은 아주 뛰어납니다.
