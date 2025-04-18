---
layout: post
title: 듀오링고가 사용자의 성장에 다시금 불을 지핀 방법 - Part 3
date: 2025-04-02
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

듀오링고의 350% 성장의 뒷 이야기, 리더보드, 연속 학습, 알림, 그리고 혁신적인 그로스 모델
### 들어가기에 앞서

원문: [Lenny's Newsletter, How Duolingo reignited user growth](https://www.lennysnewsletter.com/p/how-duolingo-reignited-user-growth)

- 원문은 Substack 에서 발행 중인 Lenny's Newsletter 에 듀오링고의 전 CPO 였던 [Jorge Mazal](https://www.linkedin.com/in/jorgemazal/) 이 기고한 글입니다.
- 원문은 하나의 글로 이루어져 있지만 편의를 위해 여러 부분으로 나누었습니다.

---
몇 달 전 제가 참석한 작은 행사에서 듀오링고의 전 CPO 인 Jorge Mazal 이 듀오링고의 재성장에 관한 뒷이야기를 해준 적이 있습니다. 저는 그 이야기에 되었습니다. 이전까지 단 한 번도 그정도의 성장을 들어본 적이 없었거든요. 이미 성숙한 제품에서 4.5배의 성장이 있었고, 그게 여러 개의 자그마한 제품 변화가 이를 이끌었다고 했고, 혁신적인 그로스 모델 (the Growth Model) 에 뿌리를 두고 있으며, 매우 자세한 행동에 대해서 설명해주었습니다. 그래서 저는 Jorge 에게 더 많은 사람들에게 (그리고 더 깊게) 그 이야기를 들려줄 생각이 있느냐고 물었고, 이에 동의해준 것에 매우 기쁩니다. 많은 제품들이 이미 듀오링고로부터 영감을 얻고 있으며, 이 이야기 덕분에 그런 경향이 더 크게 생길 것이라고 기대합니다. 시작하겠습니다!

더 많은 정보를 얻고 싶으시면 [LinkedIn](https://www.linkedin.com/in/jorgemazal/) 과 [Twitter](https://x.com/jorgemazal) 에서 Jorge 를 팔로우 하세요.

---

![jorge-picture](https://substackcdn.com/image/fetch/w_1272,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F01d58ab8-30d0-4dab-bf99-772047443e44_8000x4000.png)

### 관련 글

- [의미있는 지표 (데이터로 제품팀이 집중해야할 것을 뾰족하게 만든 방법)](https://chukycheese.github.io/data-analytics/meaningful-metrics/)
- [듀오링고가 사용자의 성장에 다시금 불을 지핀 방법 - Part 1](https://chukycheese.github.io/data-analytics/how-duolingo-reginited-user-growth-part-1/)
- [듀오링고가 사용자의 성장에 다시금 불을 지핀 방법 - Part 2](https://chukycheese.github.io/data-analytics/how-duolingo-reginited-user-growth-part-2/)
- [듀오링고가 사용자의 성장에 다시금 불을 지핀 방법 - Part 3](https://chukycheese.github.io/data-analytics/how-duolingo-reginited-user-growth-part-3/)
- [듀오링고의 그로스 모델에 대한 오해](https://chukycheese.github.io/data-analytics/what-everyone-gets-wrong-about-the-duoling-growth-model/)

## 리더보드 벡터

이러한 명확한 방향성을 세우고 나서 저희는 의도치 않게라도 CURR 을 움직인 적이 있었는지 찾기 위해 모델링에 사용한 수년 간의 데이터와 실험 결과들을 살펴보았습니다. 놀랍게도 없었지만요. 사실 CURR 은 지난 몇 년 동안 꼼짝도 하지 않았습니다. 그래서 저희는 첫 번째 원칙에 기반하여 CURR 을 움직이기 위한 첫 삽을 떠야한다는 것을 깨달았습니다.

저는 지금도 리텐션을 높이기 위한 시도로써 게이미피케이션은 좋은 출발점이라고 생각합니다. 꿈의 정원 스타일의 이동 횟수 기능은 게이미피케이션이 듀오링고에 도움이 될 거라고 생각했던 이유가 사실이 아니라는 것을 증명한 것은 아니었습니다. 이동 횟수 기능이 매우 어설픈 시도였다는 것을 배우기는 했지만요. 이번에는 추가 또는 차용하고자 하는 기능에 대해 보다 체계적이고 똑똑하게 접근해야만 했습니다. 이전에 게이미피케이션을 이용하려고 했던 시도에서 배운 것을 제대로 적용해야 했습니다.

어느 정도의 논의를 거친 결과 저희는 리더보드를 만들기로 마음 먹었습니다. 그 이유와 방법을 설명드리겠습니다. 듀오링고는 이미 사용자가 친구, 그리고 가족과 경쟁할 수 있도록 리더보드를 만들어 놓았습니다만, 그닥 효과적이지는 못했습니다. Zynga 에서의 경험에 따르면 보다 나은 방법이 있다고 생각이 들었습니다. Zynga 에서 팜빌 2 (FarmVille 2) 를 개발하기 시작했을 때, 친구들과 경쟁하는 형태의 듀오링고 리더보드와 비슷한 기능을 포함하고 있었습니다. 그 당시 저는 게이머로서의 개인적인 경험에 비추어 봤을 때, 개인적인 관계에서의 친밀도 보다 경쟁자의 참여에 의한 친밀도가 훨씬 더 중요하다는 가설을 세워봤습니다. 특히 친구들이 더이상 이용하지 않는 성숙한 제품에서 더욱 그럴 것이라는 생각이 들었습니다. 이를 기반으로 Zynga 에서 만든 것과 같은 리더보드가 듀오링고의 상황에 훨씬 더 성공할 것이라고 판단했습니다.

팜빌2의 리더보드는 "리그 (league)" 시스템도 가지고 있었습니다. 주간 리더보드의 상위권에 위치하는 것을 넘어서 사용자는 일련의 리그 (예를 들어, 브론즈 리그에서 실버리그, 그리고 골드 리그) 를 넘어갈 수 있는 기회를 가질 수 있었습니다. 리그는 사용자들이 성장과 보상을 더욱 느끼게 해주었고, 게임 디자인에 있어서 통합된 요소이기도 했습니다. 그리고 참여도가 높은 사용자는 훨씬 더 경쟁이 심한 리그로 매주 올라갔기 때문에, 장기간에 걸쳐서는 참여도를 높이기도 했습니다. 저희는 이 기능이 일반적인 인간의 경쟁심과 향상힘의 동기를 직접적으로 자극할 수 있어서 듀오링고의 현재 제품에 잘 녹아들 수 있을 것이라고 여겼습니다.

![duolingo-leagues](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc30bdb3b-bf15-4b2d-8bb4-72827c136cdd_516x514.png)

하지만 팜빌2 리더보드의 모든 요소들이 듀오링고에 잘 반영될 수 있는 것은 아니었습니다. 저희는 듀오링고의 상황에 맞춰서 이 게이밍 요소를 적용할 수 있도록 잘 판단해야 했습니다. 팜빌2에서는 리더보드에서 경쟁을 하기 위해서는 기본적인 게임 플레이 이외에도 추가적인 과업을 완료해야 했습니다. 듀오링고에서 더 많은 요소를 집어 넣게 되면 언어 학습에는 필요없는 복잡도만 높이게 되는 꼴이었습니다. 저희는 최선을 다해서 이 리더보드가 일상적이고 유려하게 설계되도록 만들었고, 사용자들은 자동적으로 참가하게 되어서 정규 언어 학습만 지속적으로 진행하면 첫 번째 리그의 상위권에 안착할 수 있었습니다. 게임 메커니즘을 쉽게 유지하면서도, 팜빌2 보다는 간단하게 만듦으로써 저희는 적용 (adopt) 과 적응 (adapt) 의 균형을 잘 맞췄다고 생각했습니다.

리더보드 기능은 지표에 즉각적이고 강력한 영향력을 보여줬습니다. 전체적인 학습 시간은 17% 늘었고, 고 참여 학습자 (일주일에 5일 이상, 하루에 1시간 이상 학습한 사용자) 의 수는 3배로 늘었습니다. 이때까지도 저희는 CURR 에 대한 통계적 유의성을 계산할 수 있는 방법을 찾아내지는 못했지만, 기존에 사용하던 유지율 지표 (1일, 7일 등의 유지율) 가 눈에 띄게 증가했고, 통계적으로도 유의하다는 것을 확인했습니다. 이후에 리더보드 기능은 지표를 향상시키는 벡터 중 하나가 되었으며, 오늘날까지도 여러 팀이 최적화를 하고 있습니다.  그리고 또 중요한 것은 리더보드가 리텐션팀의 첫 번째 돌파구가 되었다는 사실입니다!

## 푸시 알림 벡터

리텐션팀은 현재 사용자들의 참여도를 높이고, 매일 학습할 동기를 부여할 메커니즘을 찾기 위해 아주 혈안이었습니다. 그 중 한 분야가 푸시 알림 (push notification) 이었죠. 지난 수년 동안의 수많은 A/B 테스팅에 의하면, 듀오링고에서 알림은 성장을 위한 큰 힘이 될 수 있도록 기반은 만들어 둔 상태였으나, 시간이 지나면서 그 영향력은 감소하고 있었습니다. 새로운 아이디어로 재무장한 팀원들과 함께 이 요소를 다시 이용하고자 마음 먹었습니다.

이 기능을 다시 파보면서, 저희는 한 가지 매우 중요한 원칙을 떠올렸습니다. 그루폰 (Groupon) 의 CEO 로부터 나온 주의사항이었습니다. 그는 듀오링고의 CEO Luis von Ahn 에게 그루폰은 오랫동안 하루에 하나의 이메일 알림만 보냈었다고 이야기를 했습니다. 그러던 중에 이메일을 더 많이 보내면 지표를 향상시킬 수 있을까 하는 물음을 가지기 시작했다고 합니다. CEO 는 각 사용자에게 이메일을 딱 하나만 더 보내보라고 지시를 내렸다고 합니다. 그리고 이 실험은 목표 지표를 크게 향상시키는 결과를 거두었다고도 했습니다. 이 사실에 고무되어서 그루폰은 더 많은 이메일을 보내는 실험을 지속했고, 많게는 하루에 5개까지도 보냈다고 합니다. 그렇게 얼마 간의 기간이 지나지 않아 그루폰의 이메일 채널은 그동안의 영향력을 모두 잃게 되었다고 합니다. 그루폰의 공격적인 이메일 실험이 누적되어서 마케팅 채널 하나를 아예 망가트린 것입니다. 과도한 이메일과 푸시 알림 실험의 한 가지 간과하기 쉬운 위험은 사용자가 해당 채널에서 벗어나는 것이고, 실험을 종료하더라도 수신을 거부한 사용자가 돌아오지 않는다는 것입니다. 이를 반복하면 마케팅 채널을 죽이는 것과 다름 없습니다. 그리고 이는 피해야만 하는 결과입니다. 저희는 푸시 알림에 있어서 한 가지 근본적인 규칙을 정했습니다. 채널을 사수하라.

이러한 제약 조건을 가지고, 저희는 타이밍, 템플릿, 이미지, 문구, 언어 등과 같은 다양한 요소들을 최적화할 수 있는 자율성을 팀에게 부여하기로 결정했습니다. 하지만 강력한 사유나 CEO 의 동의 없이 알림의 횟수를 늘릴 수는 없었습니다. 오랜 기간 동안 수없이 많은 반복과 실험, 그리고 밴딧 알고리즘을 통해 저희는 해마다 DAU 성장에 크게 기여한 크고 작은 성공들을 만들어낼 수 있었습니다.

![push-notification](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F48a366a3-a3cc-4286-bd9c-5e7c24155d09_464x242.png)

## 연속 학습 벡터

더 많은 성장 벡터를 찾는 과정에서 리텐션팀의 APM 은 리텐션과 듀오링고의 특정 기능을 사용하는 것 사이의 강력한 상관관계가 있는지 찾기 시작했습니다. 그는 사용자가 10일 연속 학습을 하게 되면, 중간에 그만두는 비율이 크게 낮아지는 것을 발견했습니다. 분명히 이 발견의 상당 부분은 단순한 상관관계이며, 선택 편향이었겠지만, 저희는 이 기능에 대해 다시 살펴볼만한 인사이트를 주었다고 생각했습니다.

연속 학습의 개념은 매우 간단합니다. 앱에서 특정 행동을 연속으로 행한 일자 수를 보여주는 것입니다. 하지만 놀랍게도 이 기능에는 최적화할 수 있는 요소들이 매우 많습니다.

저희의 첫 번째 성공은 연속 학습 이어가기 알림이었습니다. 연속 학습 기록을 잃을 것 같은 사용자들에게 알림을 보내는 것이었죠. 늦은 밤에 보내는 이 알림은 연속 학습 최적화를 강하게 밀어 붙일만한 장점이 있다는 것을 보여줬습니다. 이후에 몇 가지 개선을 추가하기도 했습니다. 달력을 보여주고, 애니메이션을 추가하고, 연속 학습 정지 (streak freeze) 기능을 출시하고, 보상을 주는 것도 해봤습니다. 각각은 기존의 연속 학습 아이디어를 개선하는 데에 도움을 주었고, 리텐션 향상에도 크게 기여하였습니다.

![streak](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6e7d9190-a4af-4e67-9f9b-2d1fae8a36be_242x417.png)

오늘날까지도 연속 학습 기능은 듀오링고의 가장 강력한 참여도 향상 기제 중 하나입니다. 사용자들이 듀오링고의 이용 경험을 이야기 할 때 종종 연속 학습 기록을 이야기 하곤 합니다. 저는 최근에 저에게 "제 최고 기록은 1,425일 연속 학습이요!", 라고 하면서 "연속 학습 정지 기능도 안 쓰고 말이죠!" 라고 덧붙이기도 했습니다. 직접 선택한 언어를 지난 4년 동안 하루도 빠지지 않고 학습했으니 충분히 자랑할만한 자격을 얻었다고 생각합니다.

연속 학습 기능이 작동할만한 이유는 많습니다. 그 중 하나는 시간이 지날수록 사용자에게 동기부여가 된다는 것입니다. 연속 학습 일수가 많아지면 이 기록을 잃지 않기 위한 의지도 커지기 마련입니다. 사용자 리텐션 관점에서, 저희가 사용자에게 바라는 바로 그 행동이기도 합니다. 학습자가 듀오링고에 방문하는 매일, 전날에 비해 이튿날 방문하는 것을 더 신경쓰게 하고, 결국에는 리텐션과 DAU 를 높이게 되는 것입니다. 메타 수업으로써, 연속 학습 기제에 대한 성공은 기존의 기능을 이용하더라도 눈에 띄는 성과를 만들어 낼 수 있다는 것을 보여줬다는 것이라고 생각합니다. 저희는 큰 돌파구와 빠른 최적화의 가치를 알 수 있었고, 뛰어난 팀은 이를 둘 다 가지고 있다는 것을 배웠습니다.

## CURR 이후의 성장

저희는 CURR 에서 멈추지 않았습니다. 언젠가는 CURR 이 더이상 상승할 수 없는 상태에 이르지 않을까 하는 건전한 형태의 강박증이 있었고, 머지 않아 신규 사용자 획득을 위한 성장 벡터를 찾아야 한다는 것도 알고 있었습니다. 리텐션팀은 CURR 을 높이는 데에 여전히 집중하였지만, 회사 전체로 보면, 제품과 마케팅 팀은 새로운 벡터 (리텐션과 획득에 있어서) 를 찾기 위해 지속적으로 투자하였습니다. 다행히도, 저희가 했던 도박들 중에서 세계로 진출하는 것, 소셜 기능을 추가하는 것 (최종적으로는 획득팀이 이쪽으로 피봇을 했고, 크게 성공했습니다), 수업 컨텐츠 생성을 빠르게 하는것, 인플루언서와 협업하는 것, 학교에서의 존재감을 높이는 것, (약간의 비용을 내고) 유료로 사용자를 획득하는 데에 투자한 것, 그리고 틱톡에서 엄청나게 바이럴이 된 것 등을 포함하여 성공한 것들이 있었습니다. 이것들 각각은 충분히 연구해볼 만한 사례들일 겁니다.

## 전체적인 결과들

4년 동안의 노력을 통해 저희는 CURR 을 21% 향상시킬 수 있었으며, 고관여 사용자들의 일일 이탈률을 40% 줄일 수 있었고, 다른 성공적인 것들과 함께 DAU 를 4.5배 성장시킬 수 있었습니다. 작년 한 해는 듀오링고 역사상 가장 빠른 성장률을 기록한 해이기도 했습니다. 전체 사용자의 질도 높아졌으며, 일간 활성 사용자들 중에서 7일 이상 연속 학습 기록을 가진 사용자의 비율은 3배 가까이 높아져서 DAU 의 절반 이상을 차지하고 있습니다. 즉, 지금의 듀오링고는 예전에 비해 활성 사용자 수가 훨씬 높을 뿐만 아니라, 지속해서 방문하고 있으며, 친구들을 더 많이 초대하고, 슈퍼 듀오링고를 구독할 가능성도 높습니다. 듀오링고의 성공적인 IPO 의 열쇠는 이러한 성장이었습니다.

## 글을 마치며

이 글을 통해 여러분들이 필요로 하는 새로운 벡터를 찾을 수 있는 영감을 얻기를 저는 바랍니다. 듀오링고의 제 경험에서 어떤 것을 적용하고자 한다면, 최선의 판단을 통해 여러분의 제품에 맞게 적응시키길 희망합니다. 듀오링고나 다른 제품들이 했던 것을 맹목적으로 좇지 않길 바랍니다. 이런 방식은 저에게도 통하지 않았습니다. 행복한 실험이 되길 바라겠습니다!
