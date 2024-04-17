---
title: "라이브러리 이해"
tags:
    - python
    - basic
date: "2023-08-21"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **라이브러리**
---
## **인코딩(encoding) & 디코딩(decoding)**
---
**인코딩(encoding)**은 사람이 인지하거나 사용하는 데이터를 컴퓨터가 인지하고 사용하는 0,1의 데이터로 변경하는 과정을 칭한다.

$e.x.,\;$ ASCII, Base64, unicode

{% highlight python %}
data.encode('utf-8')
# b.'xxx' 처럼 byte형식으로 변경이된다.
{% endhighlight %}

**디코딩(decoding)**은 컴퓨터가 인지하고 사용하는 0,1의 데이터를 사람이 인지하거나 사용하는 데이터로 변경하는 과정을 칭한다.

{% highlight python %}
data.decode('utf-8')
# byte형식이 기존의 코드로 변경이된다.
{% endhighlight %}

python은 utf-8(3.x) ASCII(2.x)을 기본 인코딩으로 사용한다.

{% highlight python %}
# 디폴트 인코딩을 따르지만 선언시 선언한 형식으로 인코딩한다
# -*- coding: utf-8 -*-
data = "hello world"
{% endhighlight %}

인코딩과 디코딩은 서로 다른 형식으로 변환을 할경우 에러를 유발한다.

## **클로저(closure) & 데코레이터(decorator)**
---
**클로저(closure)**는 함수안의 함수를 결과로 반환할때 출력되는 함수를 클로저 라고 부른다. 클로저는 아래와 같은 경우에 사용한다.

* 콜백함수
* 함수 실행 순서 조정
* 데코레이터 함수

{% highlight python %}
def func1():
  def func2():
    return <output2>
  return func2

if __name__=="__main__":
  data1 = func1()
  real_data = data1() #클로저 사용법
{% endhighlight %}

**데코레이터(decorator)**는 함수를 인수로 받는 클로저를 의미하며, 함수를 꾸며주는 함수로 어노테이션으로 @를 사용해서 표현이 가능하다.

{% highlight python %}
def func3()
  return <output3>

def func1(func3):
  def func2():
    func3()
    return <output2>
  return func2

data1 = func1(func3)
real_data = data1()
---------------------------#same
def func1(func3):
  def func2():
    func3()
    return <output2>
  return func2

@func1
def func3()
  return <output3>

real_data = func3()
{% endhighlight %}

## **이터레이터(iterator) & 제너레이터(generator)**
---
**이터레이터(iterator)**는 for문과 같이 순차적으로 사용할 수 있는 객체를 의미하며 한번 사용시 재사용할 수 없다.

1. iter()를 이용하여 반복 객체 생성
2. next()를 이용하여 객체에서 각각 다음값을 추출

{% highlight python %}
list1 = []
iterator = iter(list1)
next(iterator)
next(iterator)
...
{% endhighlight %}

**제너레이터(generator)**는 이터레이터를 생성하는 함수로 함수의 출력이 순차적으로 다른 값을 출력하기 원할때 사용한다.

{% highlight python %}
def generator():
  yield 'a'
  yield 'b'
  yield 'c'

gen = generator()
next(gen)
next(gen)
...
{% endhighlight %}

## **타입 어노테이션(type annotaion)**
---
**타입 어노테이션(type annotaion)**은 각변수의 자료형을 적시하는 것으로 에러의 가능성을 감소시키고, 코드의 가독성과 협업의 효율성을 위하여 사용한다.

{% highlight python %}
def func(data1: <type>, data2: <type>) -> <type>

func__annotations__
#{data1: int, 'data2': int, 'return': int }
{% endhighlight %}

## **문자열 처리**
---
문자열을 처리하는 방식으로는 str(), repr() 두가지가 있으며 아래의 특징을 가진다.

* str() : 사용자 인터페이스 문자열
* repr() : 프로그램 인터페이스 문자열

{% highlight python %}
data = repr("hello world")
eval(data) #프로그램에서 다시 사용가능한 형태로 변형
{% endhighlight %}

## **외부라이브러리 사용**
---
**pip 라이브러리 매니저**

{% highlight shell %}
pip install <pkg>
pip uninstall <pkg>
pip install <pkg==version> 버전별 설치
pip install —upgrade <pkg> 업그레이드
pip list
pip list —format=freeze > requirements.txt 리스트 파일로 저장
pip install -r requirements.txt 리스트 설치
{% endhighlight %}
