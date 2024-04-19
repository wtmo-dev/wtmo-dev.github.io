---
title: "4. Models of deep learning"
tags:
    - deep learning
    - models
date: "2023-11-02"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# supervised Learning
---

## LinearRegression
---
선형적인 모델로 예측이 될때 사용

{% highlight python %}
from sklearn.linear_model import LinearRegression
{% endhighlight %}

## LogisticRegression
---
0과1 처럼 나뉘어지는 형태 또는 0~1로 나뉘어지는 모델

{% highlight python %}
from sklearn.linear_model import LogisticRegression
{% endhighlight %}

## DecisionTreeRegressor
---
tree 형태로 구분이 되며 feature들에 따라 결과를 다각형의 직선으로 표현하는 형태이다
* 분류된 값의 평균

{% highlight python %}
from sklearn.tree import DecisionTreeRegressor

model = DecisionTreeRegressor(random_state=100,  min_samples_leaf=1, min_samples_split=5, max_depth=5)
{% endhighlight %}
> * random_state 시드값
> * max_depth 최대 깊이
> * min_samples_leaf 리프 원소의 최소갯수
> * min_samples_split root 원소의 최소갯수

## RandomForestClassifier
---
다수의 트리들을 랜덤하게 학습하는 방법으로 과적합을 방지하기 위해 탄생하였으나 비교적 느리다. feature들에 따라 결과를 구역으로 나뉘는 형태이다.  
* 복원 추출하는것을 bootstrap이라하며 복원추출로 subset을만들어 모델을 만드는것을 bagging이라고 함.  
* subset을 만들기 때문에 특정 feature의 과적합을 조절할 수 있다.  
* 트리들이 각각 독립적이다.
> * GINI index(default)  
> $1-\sum_{i=1}^n(p_i)^2$로 노드의 순도를 알 수있고 최하 0.5에서 최고 0까지 나타남  
> * cross entropy  
> $-\sum_{i=1}^n(p_i)^2*\log_2(p_i)$로 노드의 순도를 알 수있고 최하 1에서 최고 0까지 나타남

{% highlight python %}
from sklearn.ensemble import RandomForestClassifier
{% endhighlight %}

## XGBoost
---
boosting은 각트리가 이전 트리의 결과를 참조하는것.  
gradient descent(경사하강법)  
위의 기법들을 활용을 하며 level wise한 방법

## LightGBM
---
boosting은 각트리가 이전 트리의 결과를 참조하는것.  
gradient descent(경사하강법)  
위의 기법들을 활용을 하며 leaf wise한 방법

{% highlight python %}
from lightgbm import LGBMClassifier
{% endhighlight %}

# unsupervised Learning
---

## KMeans
---
cluster형태의 문제에서 포인트를 지정 후 근처값을 찾고 중심이동을 반복해 최종값을 구하게된다.(거리 기반 측정법)

{% highlight python %}
from sklearn.cluster import KMeans

model = KMeans(n_clusters = )
model.fit(X)
model.inertia_
{% endhighlight %}

> inertia_  
> 얼마나 밀집해있는지 알 수 있음(n의 갯수가 높으면 낮아지는 문제도 있음)

# survival analysis
---
## KaplanMelerFitter(survival analysis)
---
구독시간과 이탈률만을 가지고 평가하는 기본형

{% highlight python %}
from lifelines import KaplanMelerFitter

model = KaplanMelerFitter()
model.fit(<survived_time>, <is_leaved>)
model.survival_function_
model.event_table
{% endhighlight %}

> survival_function_는 시간에 따른 이탈치  
> event_table
> * removed 이탈량
> * observed 데이터 내의 이탈량
> * censored 데이터 이후 이탈 예상량
> * entrance 유입량
> * at_risk 잔류량

## CoxPH(survival analysis)
---
모든 데이터를 이용해서 평가하는 복합형으로 logistic regression에서 차용되었다.

{% highlight python %}
from lifelines import CoxPHFitter

model = CoxPHFitter()
model.fit(<data>, <survived_time>, <is_leaved>)
model.baseline_survival_
model.print_summary()
model.plot_partial_effects_on_outcome(covariates= <column_name>, values= [0,1,...])
model.predict_survival_function(<data>)
{% endhighlight %}

> baseline_survival_는 시간에 따른 이탈치  
> print_summary  
> * coef의 값과 exp(coef)등등의 값을 알 수 있으며 exp(coef)이 1에서 차이나는 만큼이 이탈률의 변화량에 미치는 비율을 말한다.
> plot_partial_effects_on_outcome  
> * \<column_name\>이 value일때 미친 영향 그래프  
> predict_survival_function  
> * 추가적인 데이터의 예측값 
