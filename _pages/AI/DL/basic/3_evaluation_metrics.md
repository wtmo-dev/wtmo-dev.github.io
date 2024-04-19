---
title: "3. Evaluation metrics of deep learning"
tags:
    - deep learning
    - evaluation metrics
date: "2023-11-01"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# mean_absolute_error(regression)
---
mse라고 불리는 지표로 결과값과 예측값간의 차의 절대값 평균이다.

{% highlight python %}
from sklearn.metrics import mean_absolute_error
mean_absolute_error(Y_test, pred_value)
{% endhighlight %}

# mean_squared_error(regression)
---
mse라고 불리는 지표로 가장 일반적으로 사용되는 값으로 결과값과 예측값간의 차의 제곱합의 절대값이다.

{% highlight python %}
from sklearn.metrics import mean_squared_error
mean_squared_error(Y_test, pred_value)
{% endhighlight %}

# accuracy_score(classification)
---
결과와 예측간의 정확도를 나타내는 지표이다.

{% highlight python %}
from sklearn.metrics import accuracy_score
accuracy_score(Y_test, pred_value)
{% endhighlight %}

# confusion_matrix(classification)
---
예측값과 결과값간의 값을 matrix로 나타낸값

{% highlight python %}
from sklearn.metrics import confusion_matrix
confusion_matrix(Y_test, pred_value)
{% endhighlight %}

# classification_report(classification)
---

{% highlight python %}
from sklearn.metrics import classification_report
classification_report(Y_test, pred_value)
{% endhighlight %}

> * precision -> 예측1(positive, type1) 정확도
> * recall -> 실제1(Type2) 정확도
> * F-1 Score precision, recall의 유사성 높으면 유사함(기하 평균)

# roc_auc_score(classification)
---

{% highlight python %}
from sklearn.metrics import roc_auc_score
roc_auc_score(Y_test, pred_value, multi_class)
{% endhighlight %}

> * roc x축을 실제값이 1일때 예측값의 1의 비율, y축을 실제값이 0일때 예측값의 1의 비율로 하여 나타내지는 그래프를 의미한다.
> * auc -> roc그래프에서 desity를 나타내고, 0.5~1의 값을 나타내며 높을수록 정확도가 높다
> * multi_class는 1대1 매칭은 ovo 1대 다 매칭은 ovr로 입력값을 받는다.

# silhouette_score(clustering)
---

{% highlight python %}
from sklearn.metrics import silhouette_score

for i in range():
    model = KMeans(n_cluster=i)
    model.fit(<data>)
    pred = model.predict(<data>)
    [].append(silhouette_score(<data>, pred))
{% endhighlight %}

> * 값이 높을 수록 효과가 좋은 결과
