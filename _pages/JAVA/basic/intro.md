---
title: "JAVA intro"
tags:
    - JAVA
    - basic
date: "2024-04-01"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# What is JAVA(W. setting)
---
JAVA의 강력한 장점은 아래와 같습니다.

* 객체 지향형 언어
* 오픈소스 프로그래밍 언어
* 인터프리터 언어
* 높은 점유율
* 안전성이 높다

JAVA가 설치되어 있지 않으면 아래를 참고하여 설치하면 됩니다.

[setting](./setting.html#how-to-set-java)

JAVA로 개발을 위한 IDE인 eclipse의 경우 아래를 참고하여 설치하면 됩니다.

[eclipse install](https://www.eclipse.org/downloads/packages/installer)

# Let's start JAVA
---
JAVA는 package > class를 가장 기본적인 구조로 가집니다. 그래서 package가 존재하고 해당하는 package 내부에 존재하는 class들을 특별한 import 없이 활용이 가능합니다.

다음은 class의 가장 기본적인 형태입니다. 하나의 클래스 파일에는 여러개의 클래스가 존재할 수 있으나 public 클래스는 하나만 허용 됩니다. 또한 해당명칭은 파일명과 같아야합니다.

method의 경우에는 main을 기본으로 합니다. method의 성격에 따라 ```public|private|protected``` 을 지정해주게 되며, 필요에 따라 없을 수 있습니다. ```static``` 키워드의 경우에는 클래스메소드로 사용 여부이며, 있을 수도 없을 수 있습니다. ```void```의 위치에는 반환타입을 나타내며, 필수 인자입니다.

{% highlight java %}
public class ClassName {

    /* method block */
    [public|private|protected] [static] void methodName(String[] args) {
    }
}
{% endhighlight %}

# type of JAVA
---
[link](./type.html)

# control of JAVA
---
[link](./control.html)

# class of JAVA
---
[link](./class.html)

# input, output of JAVA
---
[link](./io.html)

# advance of JAVA
---
[link](./advance.html)
