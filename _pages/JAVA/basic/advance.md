---
title: "JAVA advance"
tags:
    - JAVA
    - basic
date: "2024-04-09"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# Package
---
Package는 연관성이 있거나 유사한 class들을 하나의 집단으로 묶는 방법입니다. 같은 Package 내에서는 import 없이 사용이 가능합니다. 하지만 sub package의 경우에는 import가 필요합니다.

# access modifier
---
접근 제어자는 변수나 메서드의 권한 설정을 하는 키워드 입니다.
```private < default < protected < public```의 순서로 권한이 약해집니다.

## private
---
클래스에서만 사용가능한 가장 보안적인 권한입니다.

## default
---
가장 기본적인 권한으로 access modifier가 없으면 적용됩니다. 동일한 package 내에서 사용이 가능합니다.

## protected
---
동일한 package 내에서 또는 상속받은 class에서 사용이 가능합니다.

## public
---
자유롭게 사용가능한 권한입니다.

# static
---
클래스간의 공유가 필요한 인자의 경우 static을 사용합니다. 이는 메모리를 줄일 수 있으나 무분별한 사용은 인스턴스간의 간섭을 유발할 수 있습니다.

## static method
---
static을 method에서 사용할 경우 인스턴스가 아니더라도 클래스인 상태에서 method를 직접적으로 사용이 가능합니다. 이는 모든 인스턴스에 공유됩니다.

## singleton pattern
---
static의 개념을 확장하면 singleton pattern으로 사용이 가능합니다. 이 방식은 메모리낭비를 줄이며, 하나의 객체로 유지되어야하는 디자인 패턴에서 유용합니다. 아래는 singleton pattern을 만드는 방식입니다.

{% highlight java %}
class Singleton {
    private static Singleton one;
    private Singleton() {
    }

    public static Singleton getInstance() {
        if(one==null) {
            one = new Singleton();
        }
        return one;
    }
}

Singleton singleton = Singleton.getInstance();
{% endhighlight %}

# exception
---
코드를 구성하다보면 다양한 예외 케이스들이 생길 수 있습니다. 그에 따라서 예외 처리를 핸들링 할 수 있어야합니다. 다음은 try except문을 활용하여 기본적인 exception 구조를 만드는 방법입니다. 이러한 구조를 통하여 transaction이 관리될 수 있습니다.

{% highlight java %}
try {
    c = 4 / 0;
} catch(ArithmeticException e) {
    c = -1;  // 예외가 발생하여 이 문장이 수행된다.
} finally {
    System.out.println("end")
}
{% endhighlight %}

{% highlight java %}
public void sayNick(String nick) throws ArithmeticException {
    if("a" == "b") {
        throw new ArithmeticException();
    }
    System.out.println("hi");
}
{% endhighlight %}

# thread
---
프로그램이 동작하는 process에서 다중업무를 동작하는 방법을 threading이라고 합니다. 아래의 방식은 thread를 사용할 수 있는 방법을 나타냅니다.

{% highlight java %}
public class Sample extends Thread {
    public void run() {  // Thread 를 상속하면 run 메서드를 구현해야 한다.
        System.out.println("thread run.");
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        sample.start();  // start()로 쓰레드를 실행
        sample.join(); // 쓰레드가 종료될때까지 대기
    }
}
{% endhighlight %}

위의 방식은 가장기본적인 방식이며, 확장성을 위하여 interface를 사용하는 방식을 권장합니다.

{% highlight java %}
public class Sample implements Runnable {
    int seq;
    public Sample(int seq) {
        this.seq = seq;
    }

    public void run() {
        System.out.println(this.seq+" thread start.");
        try {
            Thread.sleep(1000);
        }catch(Exception e) {
        }
        System.out.println(this.seq+" thread end.");
    }
    public void main() {
        Thread t = new Thread(new Sample(i));
    }
}
{% endhighlight %}


# functional style
---

## lambda function
---
java에서 이제 lambda를 지원하고 있습니다. 아래는 그 예시이며, 주의할 점은 interface에 2개이상의 method를 허용하지 않습니다.

{% highlight java %}
@FunctionalInterface
interface Calculator {
    int sum(int a, int b);
}

public class Sample {
    public static void main(String[] args) {
        Calculator mc = (int a, int b) -> a +b;  // 람다코드
        int result = mc.sum(3, 4);
    }
}
{% endhighlight %}

## stream
---
streaming과 같은것으로 오해할 수 있지만, stream은 말그대로 서순적인 흐름을 의미합니다. 아래는 stream을 사용하는 방법이며, 이와 같이 복잡한 변환을 가시성 있게 정리 할 수 있습니다.

{% highlight java %}
int[] data = {5, 6, 4, 2, 3, 1, 1, 2, 2, 4, 8};
int[] result = Arrays.stream(data)  // IntStream을 생성한다.
    .boxed()  // IntStream을 Stream<Integer>로 변경한다.
    .filter((a) -> a % 2 == 0)  //  짝수만 뽑아낸다.
    .distinct()  // 중복을 제거한다.
    .sorted(Comparator.reverseOrder())  // 역순으로 정렬한다.
    .mapToInt(Integer::intValue)  // Stream<Integer>를 IntStream으로 변경한다.
    .toArray()  // int[] 배열로 반환한다.
    ;
{% endhighlight %}
