---
title: "JAVA control"
tags:
    - JAVA
    - basic
date: "2024-04-04"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# control of JAVA
---
자바에는 제어문이 있습니다.

# if else
---
조건에 따른 수행을 나타냅니다. 기본적인 구조는 아래와 같습니다.

{% highlight java %}
if (<case1>) {

} else if (<case2>) {

} else {

}
{% endhighlight %}

삼항연산자로는 아래와 같이 활용가능합니다.
{% highlight java %}
(<condition>) ? (<true_case>) : (<false_case>)
{% endhighlight %}

# switch case
---
조건에 따른 수행을 나타냅니다. 기본적인 구조는 아래와 같습니다. 각 case는 독립적으로 끝나지 않기때문에 break가 없으면 case들을 통합적으로 사용 가능합니다.

{% highlight java %}
switch(입력변수) {
    case 입력값1:
        break;
    case 입력값2:
        break;
    default:
        break;
}
{% endhighlight %}

# while
---
조건에 따른 수행을 나타냅니다. 기본적인 구조는 아래와 같습니다. 조건에 따라 무한으로 작동될 수 있어서 탈출 할 수 있게 구조하면 좋습니다. ```break, continue```를 사용할 수 있습니다.

{% highlight java %}
while (<condition>) {
    <action>;
}
{% endhighlight %}

# for
---
조건에 따른 수행을 나타냅니다. 기본적인 구조는 아래와 같습니다. 조건에 따라 무한으로 작동될 수 있어서 탈출 할 수 있게 구조하면 좋습니다. ```break, continue```를 사용할 수 있습니다.

{% highlight java %}
for (<init_value>; <condition>; <value_increase>) {
    <action>
}
{% endhighlight %}

{% highlight java %}
for (<iterable>) {
    <action>
}
{% endhighlight %}

# condition(and or not)
---
```&&, ||, !``` 순서대로 and, or, not을 나타냅니다.
