---
title: "선형성과 선형대수"
tags:
    - math
    - linearity
date: "2023-07-21"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **선형대수학(linear algebra)**
---
**선형대수학(linear algebra)**은 문자 그대로 연산의 선형성을 다루는것이다. 선형성을 따지기 위해서는 선형연산이 적용되는것을 확인해야한다.  

# **선형연산(linear operations) 이항연산(binary operation)과 스칼라곱(scalar multiplication)**
---
**선형연산(linear operations)**에는 **이항연산(binary operation)**과 **스칼라곱(scalar multiplication)**이 있으며, $V$가 비어있지 않은 집합일때 $\ast : V \times V \rightarrow V$이와 같은 상황에서 $V$에 대한 이항연산이라 부른다.

$\cdot : R \times V \rightarrow V$에서는 $V/R$에 대한 스칼라곱이라 부른다.  

# **백터공간(vertor space)**
---
위와 같은 선형연산을 가지는 집합을 **백터공간(vertor space)**라고 부고 여기에는 다음과 같은 규칙들이 있다.



>> $(v,t):abelian \;group$
>>> $(v,t):group$
>>>
>>> 결합법칙(associativity) : $(v+w)+u=v+(w+u)$ for $v,w,u \in V$
>>>
>>> 항등원(identity) : $\exists 0_0 \in V$ s.t. $v+0_0=0_0+v=v$ in $\forall v \in V$
>>>
>>> 역원(inverse) : $\forall v \in V, \exists v^\` \in V s.t. v+v^\` =v^\`+v=0$
>>
>> 교환법칙(commutative property) : $v+w=w+v$ for $w,v \in V$
>
> 분배법칙(distributivity) $ in \; a,b\in R \; v,w\in V$ 
> * $(a+b)v = av+bv$ 
> * $(ab)v = a(bv)$
> * $A(v+w)=av+aw$
> 
>
> $1 \cdot v =v$, $\forall v \in V$


# **선형사상(linear map)**
---
두개의 백터공간이 입력과 출력이 되는 함수가 선형성을 가질경우 **선형사상(linear map)**이라 한다.  

# **선형대수학의 기본정리(Fundamental Theorem of Linear Algebra, FTLA)**
---
**선형대수학의 기본정리(Fundamental Theorem of Linear Algebra, FTLA)**에 따르면 선형사상과 행렬은 같은것으로 취급할 수있다.  
