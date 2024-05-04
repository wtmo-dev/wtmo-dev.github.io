---
title: "JAVA types"
tags:
    - JAVA
    - basic
date: "2024-04-03"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# type of JAVA
---
자바에는 다양한 타입이 있습니다. 이는 엄격하며, 규칙을 잘 지켜서 작성해야 합니다.

## normal types
---
다음은 일반적인 type에 대한 설명입니다. 선언할때 final 키워드를 넣을 수 있는데 이는 값이 변환이 없어야 할때 사용됩니다.

* int
```-2147483648 ~ 2147483647```를 표현 가능한 정수입니다.
{% highlight java %}
int num = 20;
{% endhighlight %}
* long
```-9223372036854775808 ~ 9223372036854775807```를 표현 가능한 정수입니다.
{% highlight java %}
long num = 20L;
{% endhighlight %}
* byte
```-128 ~ 127```를 표현 가능한 정수입니다.
{% highlight java %}
byte num = 20;
{% endhighlight %}
* short
```-32768 ~ 32767```를 표현 가능한 정수입니다.
{% highlight java %}
short num = 20;
{% endhighlight %}
* float
```$-3.4^{38} \sim 3.4^{38}$```를 표현 가능한 실수입니다.
{% highlight java %}
float num = 3.14F;
{% endhighlight %}
* double
```$-1.7^{308} \sim 1.7^{308}$```를 표현 가능한 실수입니다.
{% highlight java %}
double num = 3.14;
{% endhighlight %}
* boolean
```true, false```를 표현 가능한 자료형입니다.
{% highlight java %}
boolean isOkay = true;
{% endhighlight %}
* char
```단일 문자```를 표현 가능한 자료형입니다. char는 다음과 같이 다양한 형태로 대입이 가능합니다.
{% highlight java %}
char data1 = 'a'; // 문자
char data1 = 97; // 아스키 코드
char data1 = '\u0061'; // 유니 코드
{% endhighlight %}
* String
```다중 문자```를 표현 가능한 자료형입니다. String은 다른 자료형과 다르게 객체입니다. 이러한 이유는 다중문자는 가변적인 사이즈를 가지기 때문입니다.
{% highlight java %}
String name = "Minsu";
{% endhighlight %}
string은 객체이기 때문에 다음과 같은 method와 특징들을 가집니다.
> a.equals(b) : a,b가 같은지 비교합니다.
> a == b : a,b가 같은 객체인지 비교합니다.
> a.indexOf("name") : name이 몇번째 위치에 있는지 확인합니다.
> a.contains("name") : name이 포함되어 있는지 확인합니다.
> a.charAt(num) : num에 있는 문자를 반환합니다.
> a.replaceAll("A","B") : A를 B로 변환합니다.
> a.substring(num1, num2) : num1에서 num2에 있는 문자들을 반환합니다.
> a.toUpperCase() : 대문자로 변환합니다.
> a.split(char) : char를 기준으로 문자를 잘라서 배열로 반환합니다.
* StringBuffer
```다중 문자```를 표현 가능한 자료형입니다. String과 다른점은 수정을 할때 용이하다는 점입니다. String은 객체로 구성되어 있어 수정할때마다 객체가 생성되지만 StringBuffer는 1개의 객체로 수정이 가능합니다. 하지만 수정이 빈번하게 일어나는 경우가 아닌경우 오히려 메모리 사용량 효율이 좋지 않습니다.
{% highlight java %}
StringBuffer name = new StringBuffer();
name.append("Minsu");
name.insert(0, "Kim");
name.substring(0, 10);
String result = name.toString();
{% endhighlight %}
* StringBuilder
StringBuffer과 같습니다. 하지만 성능이 조금 더 좋습니다. 단점으로는 멀티 스레드환경에서 취약합니다.
* Array
```데이터의 집합```을 표현 가능한 자료형입니다.
{% highlight java %}
int[] odds = {1, 3, 5}

String[] weeks = new String[7]; // 사이즈 지정 선언
weeks[0] = "월";
{% endhighlight %}
* List
Array와 같이```데이터의 집합```을 표현 가능한 자료형입니다. 다른점은 선언 이후 사이즈의 변경이 가능하다는 점입니다. List는 사용방법에 따라 ArrayList, LinkedList와 같이 다양한 자료형이 있습니다.
{% highlight java %}
import java.util.ArrayList;

ArrayList pitches = new ArrayList();
pitches.add("138");
pitches.get(1);
{% endhighlight %}

generic이라는 방식은 리스트 자료형에서 사용할 자료형을 정확하게 명시하는것입니다.
{% highlight java %}
ArrayList<String> pitches = new ArrayList<>();
{% endhighlight %}
* Map
```{key, value} set```을 표현 가능한 자료형입니다. map 또한 사용법에 따라 HashMap, TreeMap등 다양한 자료형이 있습니다.
{% highlight java %}
import java.util.HashMap;

HashMap<String, String> map = new HashMap<>();
map.put("people", "사람");
map.getOrDefault("java", "자바") // 일반적인 get은 값이 없으면 null 반환
{% endhighlight %}
* Set
```집합```을 표현 가능한 자료형입니다. set 또한 사용법에 따라 HashSet, TreeSet등 다양한 자료형이 있습니다.
{% highlight java %}
import java.util.HashSet;

HashSet<Integer> set = new HashSet<>(); // wrapper class 사용
set.add(5)
{% endhighlight %}
* Enum
```상수 집합```을 표현 가능한 자료형입니다.
{% highlight java %}
enum Grades {A, B, C}
Grades.A
{% endhighlight %}

### Advance Tip
---
각각의 type들은 일반적으로 사용하는 원시 자료형에 대응하는 Wrapper class가 존재하며 multi-thread의 상황에서는 Wrapper class로 사용해야합니다.

## custom types
---
type을 custom하여 생성할 수 있습니다. 이는 class를 만드는것과 유사합니다.

{% highlight java %}
class Human {}
Human minsu;
{% endhighlight %}

## changing types
---
다음은 형변환및 포멧팅에 대한 방법입니다.

다음은 string형으로 나타낼때 사용하는 형변환입니다.

{% highlight java %}
String.format("I like %s", "apple")
{% endhighlight %}

> %s : string
> %d : decimal
> %c : char
> %f : float
> %o : 8진수
> %x : 16진수
> %% : %
> %10d : 10자리의 decimal 부족할경우 앞자리에 공백
> %-10d : 10자리의 decimal 부족할경우 뒷자리에 공백
> %.4f : 소숫점 4자리의 float

다음은 다양한 형변환을 하는 방법입니다. 이는 wrapper class를 사용하여 변환을 하며, 대부분의 형에서 사용이 가능한 폼입니다.

{% highlight java %}
Integer.parseInt(num) // string num to int num
Integer.toString(num) // int num to string num
...(Double ...)
{% endhighlight %}
