---
title: "확률"
tags:
    - statistic
    - probability
date: "2023-07-26"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **표본공간(sample space)과 사건(event)**
---
전체 공간의 부분집합을 **사건(event)**이라고 정의하고 전체 공간에서 관측 가능한 모든 집합을 **표본공간(sample space)**이라고 한다.  

# **확률(probability)**
---
표본공간에서 다음의 규칙들을 만족하는 것을 **확률(probability)** $P$라고 한다. 

> * $P(S)=1$
> * $\forall \; event \; A \; on \; S$, $0 \leq P(A) \leq 1$(positive measure)
> * $A_1,A_2,… : event \; with \; A_i \cup A_j=\phi$(=mutually disjoint)  
> → $P(A_1 \cup \cdots ) = P(A_1) +\cdots$

# **확률변수(random variable)**
---
$X:S \rightarrow R$인 함수가 모든 출력을 포함하고 있으면 확률변수(random variable)라고 한다.  

# **이산확률변수(discrete random variable)**
---
확률변수는 크게 두종류로 나뉘어지며 countable 할 경우는 **이산확률변수(discrete random variable)**로 불려지며 확률을 계산을 할때 사용하는 확률밀도함수(probability density function)는 

$f:X(X) \rightarrow [0,1]$, $f(x):=P(X=x)$

$P(a \leq X \leq b)= \underset{a\leq x \leq b}{\sum}f(x)$

로 나타낼 수있다.  

# **연속확률변수(continuous random variable)과 연속균등분포(uniformdistribution)**
---
uncountable할때는 연속확률변수(continuous random variable)로 불려지며 확률밀도함수는 $\int_a^bf(x)dx=P(a \leq X \leq b)$로 나타내진다.

연속확률변수가 균등한값을 가지게 되는 특이케이스를 **연속균등분포(uniformdistribution)**라고 부르며 다음과 같이 표기하기도한다. $-\infty < a < b < + \infty$, $f(x):=\begin{cases}
  {1 \over {b-a}} \; if x\in[a,b] \\
  0 \; otherwise 
\end{cases}$  

# **확률에서의 변수들(variables in probability)**
---
확률에서는 통계및 분석을 위해서 다양한 변수들을 구한다.

> * 이산확률분포에서  
>    기댓값(expectation)은 $E(X) = \mu :=\sum_x x\cdot f(x)$  
>    분산(variance)은 $Var(X) :=E((x-\mu)^2) = E(X^2)-E(X)^2$  
>    표준편차(standard deviation)는 $\sigma(X) := \sqrt{Var(X)}$  
> * 연속확률분포에서  
> 기댓값은 $E(X) = \mu :=\int_{-\infty}^{+\infty} x\cdot f(x)dx$  
> 분산은 $Var(X) :=\int_{-\infty}^{+\infty}(x-\mu)^2f(x)dx = E(X^2)-E(X)^2$  
> 표준편차는 $\sigma(X) := \sqrt{Var(X)}$
    

# **확률분포(distributions)**
---
## **베르누이 실행(bernoulli trial)**
---
동전을 던져서 앞뒤를 확인 하는것처럼 단 1회의 기회에 참과 거짓이 있는것을 **베르누이 실행(bernoulli trial)**이라고 부른다.  

## **이항분포(binomial distribution)**
---
베르누이 실행과 같이 참과 거짓만 있는 분포도를 **베르누이 분포(bernoulli distribution)**라고 한다. 참과 거짓이 아닌 임의의 $p$확률과 $1-p$ 확률이 있을때 다회의 실행에서 나타내는 분포를 **이항분포(binomial distribution)**라고 부른다. 이는 $P(X=k)=
\begin{pmatrix}
n\\
k
\end{pmatrix} \cdot p^k(1-p)^{n-k} (0 \leq k \leq n, k \leq \mathbb {Z})$로 표현되며 $X \sim B(n,p)$이다.  

## **다항분포(multinomial distribution)**
---
이항분포의 경우 두개의 경우에서만의 확률이라면 더많은 경우에서의 확률을 가질때는 **다항분포(multinomical distribution)**라고 칭하며 $n$번의 시행횟수, $k$개의 경우, 각확률이 $p_1,…,p_k$라고 할때, $P(X=(x_1,...,x_k))=
\begin{pmatrix}
n\\
x_1,...,x_k
\end{pmatrix} \cdot p_1^{x_1} \cdots p_k^{x_k} (0 \leq k \leq n, k \leq \mathbb {Z}, p_i \in [0,1])$  

## **표준정규분포(standard normal distribution)**
---
$\phi(z):={1 \over \sqrt{2\pi}}e^{-{1 \over 2}z^2}$를 $pdf$로 가지는 확률분포를 **표준정규분포(standard normal distribution)**라고 부르며 $pdf$를 다음과 같이 $P(a \leq z \leq b)=\int_a^b \phi(z)dz, Z \sim N(0,1)$ 나타낸다.  

## **정규분포(normal distribution) z-score**
---
$\mu \in \mathbb{R}, \sigma > 0$이면서 ${1 \over \sigma}\phi({x-\mu \over \sigma})={1 \over \sqrt{2\pi}\sigma}e^{-{1 \over 2}({x-\mu \over \sigma})^2}$로 구성된 확률분포를 **정규분포(normal distribution)**라고 부르며 $pdf$를 다음과 같이 $P(a \leq x \leq b)=\int_a^b {1 \over \sigma}\phi({x-\mu \over \sigma})dx, X \sim N(\mu,\sigma^2)$ 나타낸다. 표준편차 $\sigma$에 해당되는 수치 별로 전체 데이터가 해당하는 비율을 알 수 있고 그것을 **z점수(z-score)**라고 부르며 $\sigma$에 해당하는 값을 68%, $2\sigma$에 해당하는 값을 95%라고 한다. 이와 같은 비율들로 이상치를 확인하기 쉬워진다.  

## **푸아송분포(poisson distribution)**
---
이항분포에서 시행 횟수가 무한히 클경우 계산하기 힘들어진다, 이때는 근사치를 이용하여 계산을 하는것이 비교적 쉬워지는데 이것을 푸아송근사 라고 칭하며 푸아송분포(poisson distribution)을 가지게 된다. $n \gg 1 \; \& \; p \ll 1$ s.t. $np_n \rightarrow \lambda \; as \; n \rightarrow \infty$ 일때 $pdf_X(x) ={n \choose x}p_n^x{(1-p_n)}^{n-x} \rightarrow {e^{-\lambda} \lambda^x \over x!} \; as \; n\rightarrow \infty$로 나타내진다. $X \sim Poisson(\lambda) \rightarrow E(X) =\lambda, \; Var(X)=\lambda$  
