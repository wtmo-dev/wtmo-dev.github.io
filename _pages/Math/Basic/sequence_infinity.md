---
title: "수열과 극한"
tags:
    - math
    - sequence
    - infinity
date: "2023-07-24"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **열거(enumerate)**
---
대부분의 countable한 집합 $A$의 경우 **열거(enumerate)**할 수 있으며 $A={\{a_1,a_2,...}\}$와 같이 표기 할 수 있다.  

# **수열(sequence)**
---
함수 $f$가 $N$에 대하여 임의의 정수가 매칭이 되는 대상이 있을때 다음과 같이 정의 될때 다음을 $f : N \rightarrow \square$  e.q. $f : n \mapsto f(n)$ **수열(sequence)**이라고 정의한다. 다양한 경우에서 예시를 보면

 $a_n = {1 \over n} \in R$은 실수의 수열,

$A_n=\begin{pmatrix}
  n & 0 \\
  0 & 1 
\end{pmatrix} \in M_2(R)$은 $2 \times 2$ 배열의 수열,

$f_n(x) := x^n \rightsquigarrow {\{f_n}\}_{n=1}^\infty$ $(x \in [0,1])$는 함수의 수열 이다.  

# **무한(infinity)**
---
**무한(infinity)**을 표현 하는 방법은 여러가지 있는데 그중에서 수열을 이용한 방법으로는 다음과 같다. ${\{a_n}\}_{n=1}^\infty$ , $L \in R$ 일때, 

$\underset {m \rightarrow \infty}{lim}a_m =L$ $\overset {def}{\leftrightarrow}$ $\forall \epsilon >0, \; \exists M \in N$ s.t. $m \leq N \rightarrow \|a_n -L\|<\epsilon$  
으로 나타낼 수 있다.  
$e.q.$ $\quad a_n={1 \over n} \rightarrow 0$ in $n \rightarrow \infty$  
