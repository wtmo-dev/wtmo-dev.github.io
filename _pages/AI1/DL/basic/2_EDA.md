---
title: "2. EDA of deep learning"
tags:
    - deep learning
    - EDA
date: "2023-10-31"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# 고속 옵티마이저
---
* 모멘텀 최적화
경사 하강법에 모멘텀을 추가한 형태(초기에는 느린데 모멘텀을 추가로 가져서 종단 속도까지 빠르게 도달함)

{% highlight python %}
optimizer = keras.optimizers.SGD(learning_rate=0.001, momentum=0.9)
{% endhighlight %}
* 네스테로프 가속 경사  
모멘텀에 미리 한 스탭 나아간 것을 추가하여 진동을 감소시킴

{% highlight python %}
optimizer = keras.optimizers.SGD(learning_rate=0.001, momentum=0.9, nesterov=True)
{% endhighlight %}


# 전이학습
---

{% highlight python %}
<model>.layers[:-1] -> 최종 층을 제외하고 추출
<clone_model> = keras.models.clone_model(<model>)
<clone_model>.set_weights(<model>.get_weights())
{% endhighlight %}
