---
title: "입출력과 제어문"
tags:
    - python
    - basic
date: "2023-08-11"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **입출력**
---
## **사용자 입력 및 출력**
---
**사용자 입력**은 input() 함수를 이용하여 사용자로부터 문자열 자료형 데이터를 입력받는것이다. ()안에 작성하는 내용을 “프롬프트 문자열”이라고 한다.

**사용자 출력**은 print() 함수를 이용하여 자료형을 출력한다.

* (+)를 이용하여 문자열을 더할 수 있다. (+)는 생략가능.
* (,)를 이용하여 문자열을 띄워쓰기 가능하다.

## **파일 입력 및 출력**
---
**파일 입력**은 open() 함수를 이용해서 파일을 열 수 있다.

{% highlight python %}
  data = open(<path>, <mode>)
{% endhighlight %}

mode의 종류는 아래와 같다.

* **write 모드**는 파일을 작성하는 방법으로 아래와 같다.

{% highlight python %}
  data = open(<path>,"w") #path = D:/mydesk/a.txt or a.txt
  data.write("Hello world")
  data.close()

  with open(<path>) as data:
  # context manager(수행 방법을 기억하고 있는 방식) 
  # 기본적으로 사용하는 함수를  with문 안에 사용하면 되며
  # with문을 나올 때 close를 자동으로 불러줍니다.
    data.write("Hello world")
{% endhighlight %}

* **append 모드**는 파일을 이어서 작성하는 방법으로 아래와 같다.

{% highlight python %}
  data = open(<path>,"a")
  data.write("Hello world2")
  data.close()
{% endhighlight %}

* **read 모드**는 파일을 읽는 방법으로 아래와 같다.  
	* readline() : 파일을 한줄씩 읽기(\n도 불려짐)
	* readlines() : 파일을 한번에 읽어서 리스트로 출력(\n도 불려짐)
	* strip() : 줄바꿈 문자(\n) 제거

{% highlight python %}
  data = open(<path>,"r")
  for i in len(Data.readlines()):
    text = data.readline().strip()
    print(text)

  list_data = []
  with open(<path>,"r") as data:
    for text in list_data:
      list_data.append(text.strip())
{% endhighlight %}

* **xb모드**는 binay형식으로 사용할경우 wb, rb와 같이 사용한다.

# **제어문**
---
## **if문**
---
아래와 같은 형식이 가장 기본적인 형식이며 다양한 state에서 어떻게 action이 가해지는지에 대한 제어문이다.

{% highlight python %}
  if state1:
    action1
  elif state2:
    action2
  else:
    action3
{% endhighlight %}

**in / not in 연산자**는 데이터 안에 있는지 없는지를 구별하는 연산자로 아래와 같이 작용한다.

{% highlight python %}
  if 'a' not in 'state':
    action1
  else:
    action2
{% endhighlight %}

**pass 키워드**는 조건에 해당하지만 어떠한 액션도 없이 넘기고 싶을때 사용을 하며, 개발자들 사이에서는 추후에 작업을 하기위해 사용하기도 한다.

{% highlight python %}
  if 'a' not in 'state':
    pass
  else:
    action2
{% endhighlight %} 

## **관계 & 논리 연산자**
---
**관계 연산자**는 a, b의 관계를 알아보기 위한 연산자로 True / False로 값이 나오게 된다.
* ==(같음)
* !=(다름)
* <(오른쪽이 큼)
* \>(왼쪽이 큼)
* <=(오른쪽이 크거나 같음)
* \>=(왼쪽이 크거나 같음)

**논리 연산자**는 논리적으로 참과 거짓을 나타내는 연산자로 True / False로 값이 나오게 된다.

* not(부정)
* and(논리 곱)
* or(논리 합)

## **while & for문**
---
**loop case**는 리스트 형과 같이 루프를 가질 수있는 형식들은 다음과 같다.

* 문자열 : 문자열은 리스트와 같이 각 문자들을 변수로 사용가능하다.
* range() : 범위를 생성해주는 함수. (출력시 range()로 나오며 list()함수로 가시화 가능)
    * range(n)은 0~n-1의 정수 집합이다.
    * range(i,n)은 i~n-1의 정수 집합이다.
    * range(i,k,n)은 i~k-1까지 n의 차

**for문**은 아래와 같이 ~에서 반복이 될때 사용하는것으로 in에 해당하는 내용이 끝날때 까지 반복이된다. 특이점 중 하나는 딕셔너리형식을 반복할경우 변수로 key값이 도출된다.

{% highlight python %}
  for var in list('or other loop case'):
    action
{% endhighlight %}


**while문** : 어떠한 조건이 있을때 조건에 해당하면 반복하는 반복문으로 아래와 같이 사용된다. 일명 무한 루프라고 하며 조건에서 탈출 할 수 없을경우 심각한 오류를 발생할 수 있음

{% highlight python %}
  while state:
    action1
    action2
{% endhighlight %}

**break 키워드**는 반복문을 탈출 할때 사용이 되는 키워드로 무한 루프와 같은 에러발생이 의심되면 사용가능하다.

**continue 키워드**는 반복문에서 다음액션을 무시하고 처음부터 다시 시작하고 싶을때 사용이 가능하다. 
