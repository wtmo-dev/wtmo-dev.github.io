---
title: "명제"
tags:
    - math
    - thesis
date: "2023-07-17"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **명제(statement)**
---
참과 거짓으로 이루어지는 선언형 문장을 **명제(statement)**라고 명칭한다. 명제에 있어서 논리문자는 아래와 같다.


* 모두(for all)($\forall$)  
* 일부분(for some)($\exists$)  
* 하나(only one)($\exists!$)  
* 아니다(not)($!$)  
* 그리고(land)($\land$)  
* 또는(lor)($\lor$)  
* 정의(define)($:=$)  
* 반대되는(lnot)($\lnot$)  
* 그렇다면(right arrow)($\rightarrow$) 
* 단일매칭(maps to)($\mapsto$) 


이외에도 많이 있으나 대표적으로 사용되는 몇개만 추려서 작성했다.  

# **논리조건(logical condition) & 필요충분조건(necessary and sufficient conditon)**
---
$p$조건과 $q$조건이 있을 경우 $p \rightarrow q$의경우 $p$는 $q$의 **충분조건(sufficient condition)**이라고 하고 반대로 $q$는 $p$의 **필요조건(necessary condition)**이라고 부른다. 필요조건과 충분조건이 둘다 해당이될경우 **필요충분조건(necessary and sufficient conditon)**이라고 지칭한다.

| $p \; q$ \| $p \wedge q$ | $p \; q$ \| $p \vee q$ | $\;\,p\;\; \| \;\;\neg p$ | $p \; q$ \| $p \rightarrow q$ |
| ----------- | ----------- | ----------- | ----------- |
| $0 \; 0$ \| $\;\;\; 0$ | $0 \; 0$ \| $\;\;\; 0$ | $\;\,0\;\; \| \;\;\;\, 1$ | $0 \; 0$ \| $\;\;\; 1$ |
| $0 \; 1$ \| $\;\;\; 0$ | $0 \; 1$ \| $\;\;\; 1$ | $\;\,1\;\; \| \;\;\;\, 0$ | $0 \; 1$ \| $\;\;\; 1$ |
| $1 \; 0$ \| $\;\;\; 0$ | $1 \; 0$ \| $\;\;\; 1$ |  | $1 \; 0$ \| $\;\;\; 0$ |
| $1 \; 1$ \| $\;\;\; 1$ | $1 \; 1$ \| $\;\;\; 1$ |  | $1 \; 1$ \| $\;\;\; 1$ |
