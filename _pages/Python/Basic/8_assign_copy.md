---
title: "할당과 복사"
tags:
    - python
    - basic
date: "2023-08-18"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# 할당과 복사
---
**할당**은 객체가 같은 메모리를 사용하는 것으로 메모리 사용량을 줄일 수 있지만 변수값 변경시 생각지도 못한 변수도 변경이 될 수 있다.

{% highlight python %}
x = []
y = x
{% endhighlight %}

**복사**는 객체가 서로 다른 메모리를 사용하기 때문에 객체가 가지고 있는 주소도 서로 다른 값을 가지게 된다.(메모리 사용 증가)

{% highlight python %}
x = []
y = x.copy() # normal case
-----------------------------
import copy

x = [[],[]]
y = copy.deepcopy(x) # multi devision case
{% endhighlight %}
