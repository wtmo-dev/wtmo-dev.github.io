---
title: "2. EDA of machine learning"
tags:
    - machine learning
    - EDA
date: "2023-10-24"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# ordinal encoder
---
어떠한 컬럼값이 object형일 경우 학습을 시키기 힘들기 때문에 값들을 0, 1, ... 으로 넘버링하는 방법(높고 낮음의 연관성이 있을때)

1. replace()  

{% highlight python %}
data[<column_name>] = data[<column_name>].replace({"name": num})
{% endhighlight %}

2. OrdinalEncoder

{% highlight python %}
from sklearn.preprocessing import OrdinalEncoder

ohe = OrdinalEncoder()
train_ = ohe.fit_transform(train([<column_name>])) # 분류된 데이터가 도출됨
{% endhighlight %}

3. factorize

{% highlight python %}
pd.factorize()
{% endhighlight %}

# onehot encoder
---
어떠한 컬럼값이 object형일 경우 학습을 시키기 힘들기 때문에 값들을 0과 1로 이루어진 데이터로 변환하는 방법

1. train, test 카테고리 차이가 없을때 쉽게하는법  

{% highlight python %}
pd.get_dummies(data=[], columns=[], drop_first=False)
{% endhighlight %}

* data는 참조가 되는 데이터들을 나타낸다.
* columns는 데이터중 onehotencoding을 하려는 컬럼값들을 나타낸다.
* drop_first는 encoding하여 분할되는 컬럼들중 첫번째를 넣을지 뺄것인지 정하는것으로 선택적이다.

2. train, test 카테고리 차이가 있을때 진행하는법  

{% highlight python %}
from sklearn.preprocessing import OneHotEncoder

ohe = OneHotEncoder(sparse=False)
train_ = ohe.fit_transform(train([<column_name>])) # 분류된 데이터가 도출됨
ohe.categories_ # 카테고리 값이 도출됨
{% endhighlight %}

# StandardScaler
---
평균이 0 분산이 1인 값으로 데이터를 표준화하는 작업으로 보통 정규분포의 경우에서 성능향상을 위해 사용이 된다.(outlier 영향 강함)

{% highlight python %}
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
df_scaled = scaler.fit_transform(df)
{% endhighlight %}

# min max scaler
---
데이터를 0~1의 값으로 변환을 하게 되며 정규분포가 아닐경우 사용하게 된다.

{% highlight python %}
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
df_scaled = scaler.fit_transform(df)
{% endhighlight %}

# robust scaler
---
해당하는 값에서 중앙값을뺀값을 IQR로 나누어 만들어지며, ourlier 영향이 적게 스케일링이 가능하다.

{% highlight python %}
from sklearn.preprocessing import RobustScaler
{% endhighlight %}

# train/test data split
---
데이터가 학습및 학습결과 확인을 위하여 데이터를 분할해주는 작업이다.

## train_test_split
---

{% highlight python %}
from sklearn.model_selection import train_test_split

X_train, X_test, Y_train, Y_test = train_test_split(X ,y, test_size=0.2, random_state=54)
{% endhighlight %}

> random_state는 일종의 시드값으로 변화가없으면 계속 같은 값이 나온다.  

## StratifiedShuffleSplit
---
특정 \<data_\>를 동일한 비율로 나누고 싶을때 사용

{% highlight python %}
split = StratifiedShuffleSplit(n_splits=1, test_size=0.2, random_state=54)

for train_idx, test_idx in split.split(X, <data_>):

    X_train = X[train_idx]

    X_test = X[test_idx]

    y_train = y[train_idx]

    y_test = y[test_idx]
{% endhighlight %}

> random_state는 일종의 시드값으로 변화가없으면 계속 같은 값이 나온다.  

# Kfold
---

## StratifiedKfold
---

## cross validation issue
---
train/test로 나누어서 진행함에 있어서 보면 매번 결과가 뒤죽박죽으로 나올 수 있다. 이러한 이유는 train, test에 해당하는값이 치우쳐진 값으로 가질 수 있기 때문이며 이를 위해 아래와 같이 여러갯수로 분할하여 시행하는것이 더욱 정확하다고 볼 수있다.

{% highlight python %}
from sklearn.model_selection import KFold
kf = KFold(n_splits=5, random_state=100)

for train_index, test_index in kf.split(range(len(data))):
{% endhighlight %}
