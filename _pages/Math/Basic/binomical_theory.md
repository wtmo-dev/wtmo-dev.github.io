---
title: "이항정리"
tags:
    - math
    - binomical theory
date: "2023-07-20"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **팩토리얼(factorial)**
---
1에서 부터 $n$까지의 숫자를 전부 곱하는것을 $n!$라고 표기할 수 있으며 이를 **팩토리얼(factorial)**이라고 한다. 수식을 정리하면

$n! := \underset{1 \leq m \leq n}{\prod} m = n \times (n-1) \times \cdots \times 2 \times 1$ 와 같다.  

# **이항정리(binomical theorem) 이항계수(binomical coefficient)**
---
두개의 항을 가진 이항식을 거듭제곱을 하는경우를 단항식으로 나열하는것을 **이항정리(binomical theorem)**라고 하며 수식으로는 ${(a+b)}^n = \underset{r=0}{\overset{n}{\sum}}{n \choose r}a^rb^{n-r}$ 와 같이 표현을 한다.

이항정리에서 사용하는 계수를 **이항계수(binomical coefficient)**라고 하며 다음과 같이 정의한다 . ${n \choose r} := { n! \over r!(n-r)!}$  

# **다항정리(multinomical theorem) 다항계수(multinomical coefficient)**
---
이항정리와 이항계수를 차수를 높여서 포면 고차항에서도 사용이 가능하며 이를 **다항정리(multinomical theorem)**와 **다항계수(multinomical coefficient)**라고 한다. 다항정리는 다음과 같이 표현하며 

${(a_1+ \cdots +a_n)}^n = \underset{\underset{r_i \in N \cup {\{0}\}}{r_1+ \dots +r_k=1}}{\overset{n}{\sum}}{n \choose r_1, \cdots, r_k}a_1^{r1} \cdots a_k^{r_k}$

다항계수는 다음과 같이 표현한다.

${n \choose r_1, \cdots, r_k} := { n! \over (r_1, \dots , r_k)!}$
  $\quad n, r_1, \cdots, r_k \in N \cup {\{0}\}, \overset {k}{\underset {i=1}{\sum}}r_i=n$  
