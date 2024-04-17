---
title: "예외와 에러처리"
tags:
    - python
    - basic
date: "2023-08-16"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **예외&에러 처리**
---
## **예외처리**
---
프로그램 실행중에 발생하는 에러를 미연에 방지하기 위한 방법

{% highlight python %}
try:
  <case1> # 예외 발생 가능성 있는 코드
except:
  <case2> # 예외 발생시 실행
else:
  <case3> # 예외 미발생시 실행
finally: # 리소스와 같은 관리가 필요할때
  <case4> # 최종적으로 항상 실행할 코드
--------------------------level up
try:
  <case1> # 예외 발생 가능성 있는 코드
except ValueError as e: # 에러명을 지정시 여러 except문 작성가능
  print("", e)
except ZeroDivisionError:
  print("", e)
{% endhighlight %}

**예외 계층 구조** : 예외를 발생할때 해당 구조에 따라 예외를 발생시킬 수 있다.

[예외 계층 구조 참조](https://docs.python.org/ko/3/library/exceptions.html#exception-hierarchy)

## **에러제작**
---
**내장 에러 수정**은 기존의 예외 계층 구조를 따르는 에러의 경고문을 커스텀 할때 사용

{% highlight python %}
# state1에서 "에러 메시지"라는 에러를 발생
if <state1>:
  raise Exception("에러 메시지")

# state1에서 ValueError를 발생하고 "에러 메시지"라 부른다
...
  if <state1>:
    raise ValueError("에러 메시지")
except ValueError as e:
  print("", e)
{% endhighlight %}

**커스텀 에러 제작**은 기존의 예외 계층 구조 이외의 나만의 에러 경고문을 커스텀 할때 사용

{% highlight python %}
class <error_name>(Exception):
  def __init__(self):
    super().__init__("에러 설명")

...
  if <state1>:
    raise <error_name>
except <error_name> as e:
  print("", e)
{% endhighlight %}
