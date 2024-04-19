---
title: "중심극한정리와 큰수의 법칙"
tags:
    - statistic
    - CLT
    - LLN
date: "2023-07-31"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **중심극한정리(CLT)(central limit theorem)**
---
$X_1,…,X_n \overset{iid}{\sim}(\mu,\sigma^2)$ 이면서, $n$이 충분히 크다면 표준정규분포를 따르는데 이것을 **중심극한정리(CLT)(central limit theorem)**라고 한다.

# **큰수의 법칙(LLN)(law of large numbers)**
---
$X_1,…,X_n \overset{iid}{\sim}(\mu,\sigma^2)$ 일때, $\forall \epsilon > 0, \; \underset{n \rightarrow \infty}{\lim}P(|\bar{x_n}-\mu| < \epsilon)=1$ 즉, 시행횟수가 늘어나면 통계적 확률이 수학적 확률에 수렴할 확률이 1에 가까워 진다는 것으로 **큰수의 법칙(LLN)(law of large numbers)**이라고 불린다.  
