---
title: "모집단과 샘플링"
tags:
    - statistic
    - population
    - sampling
date: "2023-08-03"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **모집단(population) 샘플링(sampling)**
---
어떠한 정보를 구하려고 할때 해당 대상의 전체 집합을 **모집단(population)**이라고 하며 이러한 모집단에서 임의의 집합을 추출하면 이것을 **샘플링(sampling)**한다고 할 수있다.

이러한 샘플링에는 복원추출과 비복원추출이 있으며, 복원추출은 추출한 데이터를 포함하여 다시 추출하는것을 이르고 비복원추출은 추출한 데이터를 포함하지 않고 추출하는것이다.

샘플링 기법으로는 **단순(simaple random), 층화(stratified), 계통(systematic), 군집(cluster)** 샘플링이 대표적이다. 단순 샘플링은 랜덤하게 추출한것, 층화 샘플링은 그룹화된 모집단에서 균일한 갯수의 요소들을 추출한것, 계통 샘플링은 매 k번째 요소를 추출하는것, 군집 샘플링은 군집화된 집단들에서 몇개를 선택하는것이다.  

# **모집단에서 영향받은 독립 분포(iid)(independent & identically distributed)**
---
샘플의 이상적인 상황을 의미하며 iid일 경우 랜덤샘플 $X_1,…,X_k$, 모집단 $f(x: \theta)$ 이면 $X_1,…,X_k \overset {iid}{\sim} f(x: \theta)$으로 나타낼 수 있다.

랜덤샘플 $X_1,…,X_k$일때 $u(X_1,…,X_k)$를 통계량(statistic)으로 표기할 수 있다.  

# **표본 변수(sample variable)와 불편향성(unbiased estimator)**
---
모집단 $X \sim Bernoulli(p)$에서 $iid$ 랜덤샘플 $X_1,…,X_k$일때,

표본비율(sample rate) $\hat{P}:={1 \over n}(X_1+ \cdots + X_n)$,

표본평균(sample mean) $\bar{X} := {1 \over n} \sum_{i=1}^n X_i$

표본분산(sample variance) $S^2:={1 \over {n-1}} \sum_{i=1}^n{(X_i-\bar{X})^2}$

이 된다.

$X \sim (\mu , \sigma ^2) \rightarrow E(\bar{X})=\mu , \; E(S^2)=\sigma ^2$ 일때 $\bar{X}, \; S^2$을 **불편향성(unbiased estimator)**을 가진다고 한다.  