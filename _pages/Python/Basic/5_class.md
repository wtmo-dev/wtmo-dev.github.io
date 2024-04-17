---
title: "클래스"
tags:
    - python
    - basic
date: "2023-08-15"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **클래스**
---
**클래스(class)**는 각각의 개념화된 사물들을 객체화(object) 할 수 있고 이러한 객체들이 속성을 공유하는 방식을 지칭한다. 클래스 또한 함수와 같이 재사용성에 있어서 효과적이고, 유지보수에 유용하다. 클래스는 아래의 특징을 가진다.

> * **상속(inheritace)** : 상위의 개념과 하위의 개념간에 개념을 상속해주고 계승하는것을 의미한다. 상위의 개념은 superclass, 하위의 개념은 subclass라고 칭한다. e.x. 포유류(superclass) 고양이, 삵(subclass)
> * **다양성(polymorphism)** : 하위의 개념들이 상위의 개념에서 받은 개념 이외에 다양성을 가지는 것을 의미한다. e.x. 상위 개념(짖는다) 하위개념 (왈왈, 짹짹)
> * **추상화(abstraction)** : 클래스의 내부를 보지 않아도 내부의 변수와 같은것들을 보지 않아도 알수 있는것을 의미한다.
> * **은닉화(encapsulation)** : 클래스 내부에 변수(class variable) 기능(class method)을 가지게 되는것을 의미한다.

클래스가 사용하는 **메서드**는 다음과 같이 나눠질 수 있다.

> * 인스턴스 메서드 : 첫번째 파라미터로 self를 가진다.
> * 클래스 메서드 : 클래스의 속성에 접근하는것으로 cls파라미터 사용
> * 정적 메서드 : 메서드가 인스턴스와 독립적으로 사용될때 사용
> * 매직 메서드 :
>    * 클래스는 생성자(constructor)(__init__)를 이용하여 기본형을 정의한다.
>    * (__str__)은 문자열화를 하여 서로 다른 객체 간의 정보를 전달하는 데 사용된다.
>    * (__repr__)은 인간이 이해할 수 있는 표현으로 나타내기 위한 것입니다.  
우선 순위는 __str__이 __repr__보다 높다.
> * 추상 메서드 : 자식 class에서 필수적으로 구현해야하는 것을 지정

각각의 매서드들은 아래와 같이 사용이된다.

{% highlight python %}
class <class_name>(<superclass>):
  data0 = 0
  def __init__(self, data1, data2):
    self.data1 = data1
    ...

  def instance_method1(self, data3, data4): # 인스턴스
    action
    return 0

  @classmethod
  def class_method1(cls): # 클래스
    print(f"{cls.data0}")

  @staticmethod
  def static_method1(<input>): # 정적
    return <output>

  def __str__(self) -> str: # 매직
    return f""
  def __repr__(self) -> str:
    return f""

  @abstractmethod
  def abstract_method1(self):  # 추상
    pass
{% endhighlight %}

**클래스의 속성**은 다음과 같이 구분을 할 수 있다.

- 각 객체의 속성

{% highlight python %}
class <class_name>():
  def __init__(self, data1):
    self.data1 = data1 # 각 객체의 속성
{% endhighlight %}

- 모든 객체가 공유하는 속성

{% highlight python %}
class <class_name>():
  data0 = 0
  def __init__(self, data1):
    self.data1 = data1
    <class_name>.data0 += 1 # 모든 객체가 공유하는 속성
{% endhighlight %}

- 클래스 내부에서만 접근 가능한 속성(네임 맹글링(name mangling) 을 이용하여 변경은 가능)

{% highlight python %}
class <class_name>():
  def __init__(self, data1):
    self.__data1 = data1 # 불변 속성

._<class_name>__data1 = "x" # 네임 맹글링 하는법
{% endhighlight %}

**docstring**은 모듈, 함수, 클래스 또는 메소드 정의의 첫 번째에 오는 문자열으로 해당 객체의 doc 속성으로 사용됨.

{% highlight python %}
class <class_name>():
	"""
	문서화 자료 입력
	"""
	def __init__(self, data1):
{% endhighlight %}
