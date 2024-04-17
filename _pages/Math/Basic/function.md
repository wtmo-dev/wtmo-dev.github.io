---
title: "함수"
tags:
    - math
    - function
date: "2023-07-18"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **이진관계와(binary relation) 순서쌍(ordered pair)**
---
집합 $A, B$가 있을때 $a \in A, \; b \in B$일경우 $A$에서 $B$로의 **이진관계(binary relation)($R$)**는 **순서쌍(ordered pair)** (a,b)로 이루어진 집합이며 $A \times B$의 부분집합이다.  

# **함수(function)**
---
$f \subset A \times B$이면서 $a \in A$와 매칭되는 유일한 $b \in B$를 가질경우 $f$를 $A$에서 $B$로 향하는 **함수(function)**라고 칭한다.  

# **정의역(domain) 공역(codomain) 치역(range / image) 그래프(graph)**
---
$(a,b) \in f$에서 $x \in A$의 경우 $A$를 **정의역(domain)**이라고 하고 $y \in B$의 경우 $B$를 **공역(codomain)**이라고 한다. $A$에서 $B$로 향하는 $f(A) := {\{f(x) \; : \; x \in A}\}$는 **치역(range / image)**이라고 한다.

$f: A \rightarrow B$에서 $G(f) := {\{(x,f(x) \; : \; x \in A }\} \subset A \times B$ 인 경우 $G$를 $f$의 **그래프(graph)**라고 한다.  

# **단사(injective / one-to-one) 전사(surjective/ onto) 일대일대응(bijective / an one-to-one correspondence)**
---
함수에는 다양한 형태의 함수가 있으며 $A$에서 $B$로 향하는 함수가 있을 경우 $A$의 원소가 유일 할경우 이를 **단사(injective / one-to-one)**라고 칭하며 아래와 같이 나타낸다.

$f(x_1)=f(x_2) \rightarrow x_1=x_2$

$i.e., \;$ $\forall y \in f(A), \exists! x \in A \; s.t. \; y=f(x)$

$B$의 원소가 모두 사용될경우 이를 **전사(surjective/ onto)**라고 칭하며 아래와 같이 나타낸다.

$f(A)=B$ i.e. $f(A) \supset B$

$i.e., \; $ $\forall y \in B, \exists x \in A \; s.t. \; y=f(x)$

단사와 전사가 한번에 적용이 될경우를 **일대일대응(bijective / an one-to-one correspondence)**이라고 칭하며 아래와 같이 나타낸다.

$\forall y \in B, \exists !x \in A \; s.t. \; y=f(x)$  

# **역함수(inverse function) preimage(역상)**
---
$y=f(x)$가 있을때 $f^{-1}(y)=x$로 사용한 함수를 $f^{-1} : B \rightarrow A$인 상태의 **역함수(inverse function)**라고 지칭한다.

역함수와 서로 오해하기 쉬운것으로 오해하지 말아야 하는것이 있는데 그것을 역함수이면서 일대일대응 인것을 **preimage(역상)**이라 하며 $f^{-1}(Q) := {\{x \in A :f(x) \in Q }\}$를 $f$에 대한 $Q$의 역상이라 한다.  

# **이동(translation)**
---
$f:R \cdots> R$인 함수에서 함수 $y = f(x)$에서 $y+b=f(x-a)$로 변환된다면 이를 $x$축에서 $a$만큼 **이동(translation)**, $y$축에서 $b$만큼 이동한다고 볼 수 있다. 또한 $y=f(ax)$은 $x$축에서 $1\over a$만큼 팽창(expansion)하고 $y = af(x)$은 $y$축에서 $a$만큼 팽창한다고 볼 수 있다.  

# **볼록함수(convexity)**
---
함수의 경우 다양한 형태의 모양을 가지게 되는데 $f: R \cdots > R$, $x,y \in Dom(f) \; with \; x<y \; and \; t \in [0,1]$에서 $f(tx+(1-t)y) \leq tf(x)+(1-t)f(y)$일경우는 **볼록형(convex)** $f(tx+(1-t)y) \geq tf(x)+(1-t)f(y)$일경우는 **오목형(concave)**이다.  
$e.g., \; $로그 그래프와 같은 형태를 오목형이라고 한다.  
