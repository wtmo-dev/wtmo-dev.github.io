---
title: "회기분석"
tags:
    - statistic
    - regression test
date: "2023-08-04"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **회기분석(regression test)**
---
예측변수를 토대로 결과변수를 예측해내는 방법을 **회기분석(regression test)**이라고 부르며, $Y=f(X_1,…,X_k)+\epsilon$, $\epsilon \sim N(0,\sigma ^2)$라고 표현된다.

# **선형회기(linear regression)**
---
$Y = \alpha + \beta X + \epsilon \rightsquigarrow \hat{Y}=\hat{\alpha}+\hat{\beta}X$로 만드는 것을 회기선($\hat{Y}$)을 만드는 것이다.

$y_i - \hat{y_i}$를 **잔차(residual)**라고 한다.

# **다각형회기(polynomial regression)**
---
$Y = \alpha_0 + \alpha_1 X + \alpha X^2 + \epsilon$

# **논리회기(logistic regression)**
---
$\sigma(x) = {1 \over {1+e^{-x}}} \rightarrow \sigma (\beta_0 + \beta_1 x)$  
