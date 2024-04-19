---
title: "함수"
tags:
    - python
    - basic
date: "2023-08-14"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **함수**
---
함수에는 입력과 출력이 존재하며, 입력을 받아서 함수가 가공후 출력을 하는것이 일반적인 형태이다. 어떠한 반복적인 활동(재생산성)이 필요할때 코드의 간편화를 위해 사용이된다. 코드를 함수화 하면 가독성이 증가하는 장점이 있음

{% highlight python %}
def name(input):
  action1
  action2
  return output

var3 = name(var1, var2)
{% endhighlight %}

**인수(arguments)**는 함수 호출시 전달하는 입력값은 지칭한다.

**매개변수(parameter)** : 매개변수는 함수에서 input을 의미한다.

* **디폴트 매개변수** : 매개변수에 디폴트값(초기값)을 설정해 줄수 있다. 매개변수가 여러개일때 디폴트값을 뒤에서 부터 작성

{% highlight python %}
def name(var1, var2='data2'):
  action1
  action2
  return output
{% endhighlight %}

* **가변 매개변수** : 매개변수를 여러개 사용할때 (*)을 이용하여 튜플화 하여 불러올 수 있다. 가변 매개변수 뒤에는 일반 매개변수가 올수 없음

{% highlight python %}
def name(var1, *vars): # vars = ['data2','data3']
  action1
  return output

name('data1', 'data2','data3')
{% endhighlight %}

* **키워드 매개변수** : 매개변수에 값을 넣을때 순서대로 입력을 받는데 키워드를 이용하면 순서와 상관없이 값을 넣을 수 있게된다.

{% highlight python %}
def name(var1, var2):
  action1
  return output

name(var1 = 'data1', var2 = 'data2')
{% endhighlight %}

* **키워드 가변 매개변수** : 키워드 매개변수를 여러개 사용할때 (**)을 이용하여 딕셔너리화 하여 불러올 수 있다.

{% highlight python %}
def name(**vars): # vars = {'var1':'data1', 'var2':'data3'}
  action1
  return output

name(var1 = 'data1', var2 = 'data2')
{% endhighlight %}

**지역변수(local variable)와 전역변수(global variable)** : 함수를 사용하게 되면 주의해야하는 것중에 하나가 지역변수와 전역변수의 혼동을 막는것이다. 지역변수는 해당함수에서 사용이 되는 변수를 의미하고 전역변수는 함수의 내외 적으로 사용이 되는 변수를 의미한다.

{% highlight python %}
data2 = 'value2'
data4 = 'value4'
def func(data1, data2):
  data3 = 'value3' # local variable
  global data4 # global variable
  print(data4) # value4
  data2 = 'value5' 
  ```data2는 인수를 받아서 지역변수화 된것을 활용하기에 
  전역변수인 data2는 변화없이 함수안에서만 value5로 작용```

func('value1',data2)
{% endhighlight %}

## **람다 함수(lambda function)**
---
람다함수는 간단한 함수를 작성할때 사용이된다. 아래는 일반 함수를 람다 함수로 표현한 것이다.

{% highlight python %}
def add(a, b):
  return a+b

add = lambda a, b : a + b
----------------------------------- level up
lambda a : True if <state1> else False
{% endhighlight %}

## **map 함수**
---
순서가 있는 자료형의 원소를 순차적으로 함수에서 활용하는 함수이다.

{% highlight python %}
list1 = [1,2]

def func1(data):
  return data+1

data = map(func1 ,list1) # map object type
list(data) # type conversion
{% endhighlight %}

## **filter 함수**
---
순서가 있는 자료형의 원소들에서 원하는 항목을 추출하는 함수이다.

{% highlight python %}
list1 = [1,2]

def func1(data):
  return data > 1

data = filter(func1 ,list1) # filter object type
list(data) # type conversion
{% endhighlight %}

## **reduce 함수**
---
순서가 있는 자료형의 원소들의 스택을 쌓는 함수이다.

{% highlight python %}
from functools import reduce

list1 = [1,2,3,4,5]

def func1(data1, data2):
  return data1+ data2

data = reduce(func1 ,list1) # reduce object type
{% endhighlight %}
