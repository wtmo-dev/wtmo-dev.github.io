---
title: "1. Theory of machine learning"
tags:
    - machine learning
    - theory
date: "2023-10-23"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# Linear Regression
---
종속변수와 독립변수간에 관계를 예측하는 모델로 선형적 모델을 가지고 종속변수와 독립변수의 관계를 도출하는 방법이다. 변수가 증가함에 따라 시간 복잡도가 많이 증가한다. 일반적으로 아래의 정규방정식을 통하여 계산이 가능하지만

$$\theta = (X^TX)^{-1}X^Ty$$

역행렬이 존재하지 않거나 하는 경우 유사 역행렬인 

$$\theta = X^+y$$

를 이용하여 계산을 하며 이는 sklearn에서 기본으로 제공이 된다.(np.linalg.pinv()를 통하여 직접 계산도 가능)

## Ridge Regression(규제형)
---
학습 모델의 가중치를 컨트롤하기 위한 모델로 규제항을 포함하여 훈련하고 성능평가에서 사라진다.  
$MSE(\theta)$에 L2 norm(규제항)을 추가된 모형으로 아래와 같은 loss function을 가진다.

$$J(\theta) = MSE(\theta) + \alpha \tfrac{1}{2}\sum_{i=1}^n\theta_i^2$$

## Lasso Regression(규제형)
---
학습 모델의 가중치를 컨트롤하기 위한 모델로 규제항을 포함하여 훈련하고 성능평가에서 사라진다.Ridge회기는 중요도가 낮은 변수를 규제하지만 Lasso는 0이 될수있다.  
$MSE(\theta)$에 L1 norm(규제항)을 추가된 모형으로 아래와 같은 loss function을 가진다.

$$J(\theta) = MSE(\theta) + \alpha \sum_{i=1}^n|\theta_i|$$

## Elastic Net Regression(규제형)
---
학습 모델의 가중치를 컨트롤하기 위한 모델로 규제항을 포함하여 훈련하고 성능평가에서 사라진다.Ridge, Lasso를 융합시킨 형태이다.  
$MSE(\theta)$에 L2 norm(규제항)을 추가된 모형으로 아래와 같은 loss function을 가진다.(r=0에서 Ridge r=1에서 Lasso가 된다.)

$$J(\theta) = MSE(\theta) + r\alpha \sum_{i=1}^n|\theta_i| + \tfrac{1-r}{2}\sum_{i=1}^n\theta_i^2$$

## Early Stopping Regression(규제형)
---
경사하강법과 같은 반복적 학습에서 과적합되기전에 멈추게 하는 방법

# Gradient Descent
---
비용함수를 최소화하여 계산복잡도를 감소시킨 방법이다. 시간 및 정확도를 위하여 scaler를 통하여 특성을 유사하게 만들어야한다.  $\eta$는 학습률을 의미한다.

$$cost \, function := MSE(\theta) = \tfrac{(\hat{y}-y)^2}{m}$$

$$\tfrac{\partial}{\partial\theta}MSE(\theta) = \tfrac{2X^T(X\theta-y)}{m}$$

$$\theta^{next step} = \theta - \eta\tfrac{\partial}{\partial\theta}MSE(\theta)$$

## Batch Gradient Descent
---
전체 데이터셋의 에러를 통한 기울기로 한번만 모델의 파라미터를 업데이트하는 방법

* 장점
    * 연산횟수가 적다.
    * 전체 데이터셋을 활용하기 때문에 안정적으로 수렴한다. 
* 단점
    * 지역 최적화에 걸리기 쉽다.
    * 스텝마다 학습량이 많아 시간이 오래걸린다.

## Stomatic Gradient Descent
---
매 스탭마다 무작위 샘플을 구하여 미분을 취하는 방법

* 장점
    * 알고리즘이 빠르다.
* 단점
    * 최적의 값을 구하기 힘들다.
    * 샘플 데이터를 활용하기 때문에 불안정적으로 수렴한다.

## Mini-Batch Gradient Descent
---
임의의 작은 샘플 세트를 활용하여 기울기를 구하는 방법

* 장점
    * batch-size를 키우면 SGD보다 안정적이다.
* 단점
    * 정해진 샘플의 사용으로 SGD보다 지역 최적화에 걸리기 쉽다.

# PolynomialFeatures
---
다항 회기방법으로 변수들을 이용해 고차항을 만드는 방법  
n이 변수의 갯수, d가 차원일때 아래와 같은 수의 변수가 생성이된다.

$$\tfrac{(n+d)!}{n!d!}$$

# Logistic Regression
---
종속변수와 독립변수간에 관계를 예측하는 모델로 linear regression과 다르게 이항, 다항과 같이 항을 기준으로 classification을 한다.
* odds  
성공확률과 실패 확률의 비율  

$$odds = \tfrac{p(y=1|x)}{1-p(y=1|x)}$$

* logit  
odds에 log를 취한 함수  

$$logit(p) = log(\tfrac{p}{1-p})$$

* sigmoid function  
logit 함수의 입력과 출력을 바꾼함수  

$$p(X) = \tfrac{1}{1+e^{-\beta X}}$$

* logistic function  
sigmoid 함수 만들어진 예측 모델  

Logistic Regression은 $x$가 변할때 $y$가 1이 되는 경향성을 따지는 모델로서 아래와 같은 확률에서 시작된다.

$$p(X) = Pr(y=1|X)$$

우리가 parameter Estimation을 통하여 구하려고 하는 sigmoid의 $\hat{\beta}$는 이상 적으로 2가지 경우로 나뉜다.

> 1. $y=1$이라서 $\hat{Pr(y=1\|X)}$이 1에 수렴하는 경우  
> 2. $y=0$이라서 $1-\hat{Pr(y=1\|X)}$이 1에 수렴하는 경우

1.의 경우 최대 확률은 $\prod_{s \, in \, y_i=1} p(x_i)$  
2.의 경우 최대 확률은 $\prod_{s \, in \, y_i=0} (1-p(x_i))$  
종합적인 최대 확률은 $L(\beta) = \prod_{s \, in \, y_i=1} p(x_i) \times \prod_{s \, in \, y_i=0} (1-p(x_i))$ 가 된다.  

이 수식을 단순화 하면 아래의 수식이 된다.

$$L(\beta) = \prod_s p(x_i)^{y_i} \times \prod_s (1-p(x_i))^{1-y_i}$$

loss function을 활용해 최적의 함수를 찾아야하는 위의 수식은 미분에 있어서 쉽지 않다. 그래서 log를 이용한 log likelihood 함수를 만들고 음수를 취해주고 전체 샘플수로 나눠주면 loss function을 만들 수 있다.

$$J(\beta) = -\tfrac{1}{n}(\sum_{i=1}^n y_i log(p(x_i)) \times \sum_{i=1}^n (1-y_i) log(1-p(x_i)))$$

$$\tfrac{\partial}{\partial\beta_j}J(\beta) = \tfrac{1}{n}(\sum_{i=1}^n p(x^{(i)})-y^{(i)})x_j^{(i)}$$

## SoftMax
---
Logistic Regression의 경우 binary classification의 방법을 위하여 고안이 되었으나 multinomial classificaion에 활용할 수 있게 하는 방법이 SoftMax 기법이다.  
이는 도출된 경향성 점수를 $s(y_i) = \tfrac{e^{y_i}}{\sum e^y}$로 총합 1의 확률로 만들게된다.  
이러한 확률을 이용하여 크로스 엔트로피(주어진 정답의 불확실성의 정도) 비용함수가 최소가 되게한다.

# Decision Tree
---
Tree 구조로 형성된 의사결정 분류 알고리즘  
데이터의 회전성에 취약하여 PCA(주성분 분석, 차원축소)를 사용하면 좋다

## CART(Classification And Regression Tree)
---
tree가 subset을 나누는데 있어 gini가 작은 subset을 만드는 방법으로 greedy algorithm이다. loss function은 아래와 같다.

$$J = \tfrac{m_{left}}{m}G_{left}+\tfrac{m_{right}}{m}G_{right}$$

# Naive Bayes
---
특성들 사이의 독립을 가정하는 베이즈 정리를 이용한 확률 분류기
* Bayes Theorem  
어떠한 기존의 확률을 토대로 새로운 데이터의 확률을 구하는 방법

$$P(c\|x)=\tfrac{P(x\|c)P(c)}{P(x)}$$

* elements
    * $P(c\|x)$ posterior probabillity
    * $P(x)$ predictor prior probabillity  
    어떠한 기존의 발생 확률
    * $P(c)$ class prior probabillity  
    어떠한 특성을 가질 확률
    * $P(x\|c)$ likelihood
    특성에서의 발생이 될 확률

# Support Vector Machine(SVM)(SVC,SVR)
---
카테고리들이 있을때 데이터들의 사상된 공간의 경계중 가장 큰 너비를 가진 경계를 찾는 방법  
(복잡, 작거나 중간 데이터셋에 적합, scaler를 하면 효율 증가)
(SVC는 kernel을 통해 PolynoialFeature없이도 고차원 적용가능, 실제로 변수가 만들어지지 않아 속도빠름)
* margin  
서로 다른 두가지 클래스의 데이터에서 어떠한 선으로 구분을 할경우 해당 선의 너비를 의미한다.
* support vectors  
margin에 해당하는 위치에 놓여있는 elements를 의미한다.
* RBF(Radial Basis Fuction) Kernel
방사형 기저 함수라 불리며 비선형 데이터에서 차원을 높여서 margin을 설계하는 방법

# Clustering
---
흩어져있는 원소들을 군집화하여 유사한 데이터끼리 묶는 방식으로 하는 비지도학습

## K Nearest Neighbors(KNN)
---
새로운 데이터를 입력받을때 가까운 데이터들의 분포에 따라 통계적으로 분류를 하는 알고리즘

## K means
---
임의의 centroid를 지정후 근접합 데이터를 군집화 한다음 centroid를 재설정하는것을 반복하여 군집을 구하는 방법(변수들의 스케일링을 하면 효과가 좋다)

## DB Scan
---
밀도 기반 군집화 기법으로 범위내에 있는 샘플들의 갯수가 군집화가 되는 기준이다.

# 가우시안 혼합 모델(GMM)
---
Gaussian Mixture Model은 분류가될 집합이 가우시안 분포로 되어있다고 가정하여 클러스터를 구성하는 확률 모델이다.
흩어져있는 원소들을 군집화하여 유사한 데이터끼리 묶는 방식으로 하는 비지도학습

# Bagging VS Boosting
---
* bagging  
분산을 감소시키는 방법으로  
복원 추출을 통해 n개의 샘플을 만드는 boostraping을 통해 나온 샘플을 학습시켜서 선형 결합한것

* boosting  
편항을 감소시키는 방법으로  
weak learner를 생성해서 구한 error를 토대로 가중치를 가해 error를 줄이는 방법이다.

# Decision Tree ensemble
---
* ensemble  
우수한 모델들에서 나온 결과를 선형적으로 결합하여 성능을 향상하는 방법
## Random Forest
---
bagging을 사용한 알고리즘으로 모든 변수를 기반으로 Tree 생성
## Extra Trees
---
bagging을 사용하지 않는 random forest 알고리즘
## AdaBoost
---
boosting을 사용하여 샘플의 가중치를 더해 순차적 학습을 하는 알고리즘

# Decision Tree Gradient Boosting
---
* Gradient Boosting은 미분을 통해 Residual을 줄이는 방향으로 weak learner들을 결합하는 방법(과적합 이슈의 발생)
## Extreme Gradient Boosting(XGB)
---
Regularization과 다양한 loss function을 지원하여 과적합을 감소시킨 방법
## Light Gradient Boosting
---
histogram-based/GOSS/EFB와 같은 알고리즘으로 학습데이터를 감소시켜 속도를 향상시킨 방법  
GBM은 Level-wise한데 LGBM은 Leaf-wise해서 시간은 적게 걸려도 깊은 트리형으로 문제없이 작업한다.  
GOSS(Gradient-based One-Side Sampling)으로 infomation gain을 계산할때 기울기(가중치)가 작은 변수에 승수 상수로 데이터를 증폭시킴  
(데이터가 적으면 과적합 위험)
## Categorical Gradient Boosting
---
범주형 변수를 위한 알고리즘으로 one-hot encoding사용시 증폭되는 메모리 이슈를 보완하였음  
(oblivious Decision Tree, Feature Combination)
## Natural Gradient Boosting
---
각 예측값에 대한 신뢰도를 도출해주는 알고리즘으로 시간이 오래걸리는 단점이 있음

# 차원축소
---
대부분의 데이터는 고차원으로 구성이 되어있어도 가까이에 있는 경향이 많아 저차원 공간으로 투영(projection)과 같은 차원축소 기법을 통해 해결할 수 있다.  

## 매니폴트
---
고차원에서 휘어져있는 형태로 고차원에서 가까워 보이지만 실제로는 멀리있는 데이터를 효과적으로 차원 축소 하는 방법

## 주성분 분석(PCA)
---
Principal Component Analysis는 보편적인 차원축소 기법으로 분포도를 최대한 유지하는 방향으로 차원을 축소하는 방법이다.(평균이 0인 StandardScaler가 필요하다, sklearn은 자체 지원)  
sklearn은 explained_variance_ratio를 통하여 축소한 차원에서 얼마나 분산의 손실이 발생했는지 알 수 있다.

## 특잇값 분해(SVD)
---
Singular Value Decomposition은 주성분을 찾는 방법으로 $m \times n$인 행렬 $A_1$에 대한 특잇값 분해는 $U_1\sum_1V_1^T$이다. 이는 유사역행렬을 구하는 방법과 유사하지만 유사역행렬의 $\sum$은 $k \times k$로 변동성이 있지만 SVD는 $m \times n$이다.(thin SVD와 같이 축소기법을 사용하면 크기가 감소하기도 한다.)  
SVD를 통하여 구한 $V$의 각 열을 순서대로 $c_1, c_2, ...$로 주성분의 축을 구할 수 있다.  
$c_1, c_2, ...$의 갯수를 통하여 투영하려는 차원을 정할 수 있다.

$$X_{d-proj} = XW_d$$

## 지역선형임베딩(LLE)
---
Locally Linear Embedding은 투영을 하지않고 매니폴드를 활용하는 기법이다. 이웃 원소와의 선형성을 측정하여 국부적 관계가 보존되는 저차원을 표현함

## t-SNE
---
비슷한 샘플과 비슷하지 않은샘플로 구분하여 차원을 축소하는 방법
