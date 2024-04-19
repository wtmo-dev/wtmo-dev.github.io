---
title: "표본분포"
tags:
    - statistic
    - distribution
date: "2023-08-02"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **카이제곱분포($X^2$ distribution)**
---
$k \in \mathbb{N}$이고 $Z_{11}^2, \cdots ,Z_{1k}^2 \overset{iid}{\sim} N(0,1)$ 일때 $X \sim X^2(k) \overset{def}{\leftrightarrow} X \overset{d}{\equiv} Z_{11}^2+ \cdots +Z_{1k}^2$를 **카이제곱분포($X^2$ distribution)**라고 부르며 $k$를 **자유도(degree of freedom)**이라고 부른다.

$X \sim X^2(k) \rightarrow E(X) =k, Var(X)=2k$  ( $\therefore k$가 커질 수록 그래프가 오른쪽으로 이동하며 평평해진다.)

$X_1,…,X_n \overset{iid}{\sim} N(\mu, \sigma ^2)$ 일때,

$\bar{X} \sim N(\mu, \sigma ^2 / n)$

$S^2=\sum(X_i-\bar{X})^2/(n-1)$ $in$ $\bar{X}$ : independent

${(n-1)S^2 \over {\sigma ^2}} \sim X^2(n-1)$

카이제곱 분포는 모집단의 분산을 추정하기 위해 사용한다.  

# **t분포(t-distribution)**
---
$Z \sim N(0,1), \; V \sim X^2(r), \; Z,V$: 독립적 일때, $X \overset{d}{\equiv} {Z \over {\sqrt{V/r}}} \sim t(r)$ 이다.

$X_1,…,Xn \overset{iid}{\sim} N(\mu,\sigma ^2) \rightarrow {\bar{X}-\mu \over {S/\sqrt{n}}} \sim t(n-1)$ (모표준편차를 표본표준편차로 대체하는것)

t분포는 표본의 크기가 작거나 모분산을 알 수 없을때(위와 같이 표준편차를 대체하여) 모집단의 평균은 측정할때 사용된다.  

# **f분포(f-distribution)**
---
$V_1 \sim X^2(r_1), \; V_2 \sim X^2(r_2), \; V_1,V_2$: 독립

$F \overset{d}{\equiv}{V_1/r_1 \over {V_2/r_2}} \sim F(r_1-1,r_2-1)$

두개 이상의 모집단의 분산비를 추론하여 비교할때 사용된다.  