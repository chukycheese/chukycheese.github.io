---
layout: post
title: 2016년 모든 데이터 사이언티스트가 알아야할 10+2 가지 데이터 사이언스 방법론
date: 2019-06-09 00:30:00
toc: true
toc_sticky: true
category: data-analytics
tags:
    - data-science
    - statistics
    - machine-learning
    - translation
mathjax: true
comment: true
---

2년 전 일본어로 [책](https://www.amazon.co.jp/dp/477416674X)을 내긴 했지만 대부분의 독자들이 이 책을 읽을 수는 없을 것 같았다.

실제로 이 책은 10가지 주로 사용하는 데이터 사이언스 방법론들을 요약해놓은 것이다. 하지만 2년이 지나면서 책의 내용이 조금 뒤쳐졌다. 통계학과 머신러닝 분야가 발전함에 따라 당연히 향후에도 업데이트가 필요할 것이다. 아래는 2016년을 기준으로 모든 데이터 사이언티스트가 알아야한다고 생각하는 10+2 가지 방법론들이다.

1. 통계적 가설 검정 (t 검정, 카이제곱 검정, 분산분석)
2. 다중 회귀분석 (선형 모형)
3. 일반화 선형 모형 (로지스틱 회귀, 포아송 회귀)
4. 랜덤포레스트
5. XGBoost (eXtreme Gradient Boosted Trees)
6. 딥러닝
7. MCMC 를 이용한 베이지안 모델링
8. word2vec
9. k-평균 클러스터링
10. 그래프 이론과 네트워크 분석

* 잠재 디리클레 할당 (LDA: Latent Dirichlet Allocation) 과 토픽 모델링

* 팩터라이제이션 (Facorization; SVD, NMF)

위의 10가지는 내가 잘 알고 있고, 매일 업무에서 사용하는 것들이지만, 마지막 두 가지는 실제 비지니스에 내가 직접적으로 사용해보지는 않았지만, 운영 매니저로 일하면서 친했던 동료들이 사용하는 것은 보았다. 그렇기 때문에 앞의 10가지에 대해서는 실제 예제를 이용한 R 또는 파이썬 코드가 있지만, 뒤의 두 가지는 다른 도움말 등에서 제공해주는 일반적인 예제들만 있을 뿐이다. 이 중 일부는 gcc / clang 컴파일러나 H2O와 같은 java 런타임 환경을 요구하기도 한다.

자 그럼 이제 시작해보자.

출처: [10+2 Data Science Methods that Every Data Scientist Should Know in 2016](https://tjo-en.hatenablog.com/entry/2016/04/18/190000)
