---
title: "JAVA class"
tags:
    - JAVA
    - basic
date: "2024-04-05"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# class of JAVA
---
객체 지향으로 구조를 사용할 수 있는 class는 JAVA의 큰 특징중 하나입니다. 클래스로 부터 인스턴스를 만들게 되는데 이것을 모두 객체라고 명칭합니다. 하나의 클래스 파일은 하나의 public class가 필요하며, 파일명과 동일한 명칭을 가져야합니다.

## method
---
method는 클래스 내부에 선언된 함수들을 칭하며 다음과 같습니다.
{% highlight java %}
class Animal {
    String name;

    public void setName(String name) { // method
        this.name = name;
    }
}
{% endhighlight %}
method는 class의 변수를 this를 이용하여 접근할 수 있습니다. 하지만 static method의 경우 class 명을 사용해야 접근이 되며, 변수 또한 static으로 선언되어야 합니다. 이렇게 선언된 변수는 모든 인스턴스가 공유하게 됩니다.

## inheritance
---
상속은 class가 가지는 큰 장점중 하나로 다음과 같이 사용할 수 있습니다. 상속을 받게되면 부모의 method를 모두 사용 가능하며, 부모는 자식의 method를 사용할 수 없습니다. override를 통하여 자식은 부모의 method를 재선언 할 수도 있습니다.

{% highlight java %}
class Dog extends Animal, Mammalia {  // Animal, Mammalia 클래스를 상속한다.
}
{% endhighlight %}

## constructor
---
인스턴스가 생성될때 초기화시키는것으로 생성자라고 불립니다. 이것은 class와 동일한 명칭으로 선언을 해주어야 하며, overloading을 통하여 재선언도 가능합니다.

{% highlight java %}
class CalculatorEx {
	int a;

	public CalculatorEx() { // default constructor
		a = 10;
	}

	public CalculatorEx(int num1) { // constructor overloading
		a = num1;
	}
}
public class ConstructorEx04 {
	public static void main(String[] args) {
		CalculatorEx cc = new CalculatorEx(); // default constructor
		CalculatorEx cc = new CalculatorEx(0); // constructor overloading
    }
}
{% endhighlight %}

## interface
---
인터페이스는 class간의 상속에서 간접적으로 사용할 수 있는 요인을 간접적으로 사용하기 위한 방법입니다. 이는 더욱 자유로운 확장성을 가질 수 있게 됩니다.

{% highlight java %}
interface Predator { // 먹이를 종류를 interface로 선언
    String getFood();

    default void printFood() { // default method로 class에서 선언없이 활용 가능
        System.out.printf("my food is %s\n", getFood());
    }
}
class Tiger extends Animal implements Predator {
    public String getFood() { // interface 활용
        return "apple";
    }
}
class ZooKeeper {
    void feed(Predator predator) { // 먹이를 주는 행위를 선언
        System.out.println("feed "+predator.getFood());
    }
}
{% endhighlight %}

## abstract
---
abstract는 interface와 class를 둘다 가능한 형태의 클래스입니다.

{% highlight java %}
abstract class Predator extends Animal {
    abstract String getFood();

    void printFood() {
        System.out.printf("my food is %s\n", getFood());
    }
}
class Tiger extends Animal implements Predator {
    public String getFood() {
        return "apple";
    }
}
class ZooKeeper {
    void feed(Predator predator) {
        System.out.println("feed "+predator.getFood());
    }
}
{% endhighlight %}
