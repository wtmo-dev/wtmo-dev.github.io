---
title: "고급 활용"
tags:
    - python
    - basic
date: "2023-08-24"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **삼항연산자**
---
단순 True or False 인 상황에서 가독성을 높이는데 좋음

{% highlight python %}
if <state1>:
    <case1>
else:
    <case2>
----------------
<case1> if <state1> else <case2>
{% endhighlight %}

# **리스트 컴프리헨션(list comprehension)**
---
리스트를 만드는데 있어서 효과적으로 제작하는방법

{% highlight python %}
list1 = []
for i in range(1, 11):
    list1.append(i)
----------------
list1 = [i for i in range(1, 11)]
{% endhighlight %}

# **삼항연산자 & 리스트 컴프리헨션**
---

{% highlight python %}
<list> = [<data> for <data> in <datas> if <state>]
{% endhighlight %}

# **딕셔너리형 합치기**
---

{% highlight python %}
<dic1> = {'am': 10}
<dic2> = {"a": 20, "b": 50}
<dic1>.update(<dic2>)
----------------
<dic1> = {'am': 10}
<dic2> = {"a": 20, "b": 50}
<dic3> = {**<dic1>, **<dic2>}
{% endhighlight %}

# **정규표현식**
---

[참고사이트](https://regexr.com/)

{% highlight python %}
import re
{% endhighlight %}

re.match(\<str\>, \<data\>) 문자열 처음부터 검색(객체)  
re.search(\<str\>, \<data\>) 문자열 전체 검색(객체)  
re.findall(\<str\>, \<data\>) 문자열 전체를 검색(list형)  
re.finditer(\<str\>, \<data\>) 문자열 전체를 검색(iter형)(객체)  
re.fullmatch(\<str\>, \<data\>) 완벽한 일치하는 검색(객체)  
\<object\>.group() 객체에서 매칭된 문자열을 반환  
\<object\>.start() 객체에서 매칭된 문자열의 시작 위치  
\<object\>.end() 객체에서 매칭된 문자열의 끝 위치  
\<object\>.span() 객체에서 매칭된 문자열의 시작과 끝(tuple형)  
re.sub(\<from\>, \<to\>, \<data\>) data에서 \<from\>을 \<to\>로 변환  
