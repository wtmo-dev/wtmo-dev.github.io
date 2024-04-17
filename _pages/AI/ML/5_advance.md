---
title: "5. Advance of machine learning"
tags:
    - machine learning
    - advance
date: "2023-10-27"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# gridSearchCV
---
하이퍼 파라미터를 다양하게 활용하여 최적의 값을 찾는 방법

{% highlight python %}
from sklearn.model_selection import GridSearchCV

param_grid = [
    {'' : []},
    {'bootstrap' : [False]}
]
model = <model>
grid_search = GridSearchCV(model, param_grid, cv=5)
grid_search.fit()

grid_search.best_params_
grid_Search.best_estimator_
grid_Search.cv_results_
{% endhighlight %}

* best_params_  
최적의 파라미터 제공
* best_estimator_  
최적의 파라미터 모형 제공
* cv_results_  
iter한 객체로 전체 하이퍼파라미터 별 평가 확인가능

# Text Mining Process
---
1. corpus 정의(수집)
2. text cleaning(불용어 제거, 형태 통일)
3. tokenization(분석 단위 결정)
4. modeling
5. visualization

# 다중공산성
---
correlation이 높은 것을 의미하고 선형 모델에서 다중공산성은 문제가 될수 있고 tree 모델에서는 크게 상관이 없다.
빼는것을 결정할때는 피어슨 상관계수를 사용

$$\tfrac{corr_{1,2}}{\rho_1 \rho_2}$$

# 추천시스템
---
사용자에게 추천정보를 제공하는 방법

* contents based filtering  
나의 프로필 정보를 가지고 추천하는 방식  
* collaborative filtering(충분한 정보에서 우세)  
나의 평점 데이터를 가지고 추천하는 방식
    * item-based collaborative filtering  
    해당 사용자의 선호 item과 유사한 item 추천방식
    * user-based collaborative filtering  
    해당 사용자의 선호 item과 유사한 선호도를 가진 user의 item을 추천하는 방식

* explicit data  
평점이 명확하게 작성이 된 데이터
    * user-oriented-neighborhood model  
    평점을 기준으로 사용자간의 유사도를 확인해서 높은 평점을 가진 사용자의 추천을 추천
    * item-oriented-neighborhood model  
    평점을 기준으로 유사한 아이템을 사용자에게 추천하는 방식
* implicit data
평점이 명확하지 않아 타겟을 소비한 횟수로 구성된 데이터
    * latent factor model  
    확인된 평점의 특성을 토대로 미확인 평점을 추론해내는 방법으로 사용자와 아이템간의 평점을 나타내는 행렬을 두개의 latent factor로 나누어 학습하는 matrix factorization 기법을 사용한다.
        * matrix factorization
        $n$명의 사용자와 $i$개의 아이템이 존재할때 $n \times i$ 행렬을 임의의 factor($f$)개를 정하여 $f \times n$, $f \times i$의 행렬로 만드는것

## ALS(alternating least squares)
---
[구현예제](https://yeomko.tistory.com/8)  
두가지 인풋을 가지는 2차행렬에서 하나의 인풋을 상수로 취급하고 계산하고 다른 인풋을 상수로 취급하고 반복하는 로직을 일컷는다.  
matrix factorization에 따라 사용자 행렬을 $X$ 아이템 행렬을 $Y$라고 하면 평점행렬과 원소는 아래와 같이 표현된다.  

$$R=XY^T  \qquad  r_{ni} = x_n^Ty_i$$  

이것을 토대로 학습을 위한 loss function을 만들어야 하는데 이것은 아래와 같이 표현되며 $\lambda$는 과적합을 방지하기 위해 추가 됩니다.

$$min_{x^{'},y^{'}}\sum_{n,i}(r_{ni}-x_n^Ty_i)^2 + \lambda(\sum_u||x_n||^2+\sum_i||y_i||^2)$$

ALS에 따라 $y_i$를 상수로 취급하여 loss function의 최소값을 찾기 위하여 편미분을 취하여 $x_n$의 최소값을 찾아가면

$$-2\sum_i(r_{ni}-x_n^Ty_i)\times y_i+2\lambda x_n$$

$$\lambda x_n = \sum_i(r_{ni}-x_n^Ty_i)\times y_i$$

$$\lambda x_n = \sum_i(-x_n^Ty_i)\times y_i+\sum_i r_{ni}y_i$$

$(-x_n^Ty_i)$이 스칼라 값이라서 전치행렬을 취해도 값이 같다.

$$x_n(\lambda + \sum_i y_i \times y_i^T) = \sum_i r_{ni}y_i$$

$$x_n(\lambda I + Y Y^T) = R_{n}Y$$

$$x_n = R_{n}Y(Y Y^T + \lambda I)^{-1}$$

이와 같이 $x_n$가 최소가 되는 행렬을 찾았지만 이렇게 계산을 할 경우 implicit data의 문제에 봉착하게 된다. 이러한 missing value(미평가 점수)를 위하여 선호하는지 안하는지 알기위하여 $R_n$을 선호도 $p_{ni}$와 신뢰도 $c_{ni}$로 분할 한다.

$$p_{ni} =  {\left\{\begin{matrix}
1 \quad R_{ni} \;is \; known \\
\quad 0 \quad R_{ni} \;is \; unknown
\end{matrix}\right.}$$

$$c_{ni} = 1+ \alpha r_{ni}$$

이와같이 분할한 수식을 loss function의 편미분과 같이 다시 계산하면 

$$x_n = C_{n}Y(Y Y^T + \lambda I)^{-1}$$

가 나오게 되며 ALS 로직을 사용할 수 있다.
