---
title: "c++ intro"
tags:
    - c++
    - basic
date: "2024-04-10"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# types
---
다음은 c++에서 사용되는 자료형들을 나타냅니다. 자료형은 기본자료형과 사용자 정의 자료형이 있습니다. 사용법은 둘다 같으나 최적화가 조금 다릅니다. 아래는 기본적인 자료형을 나타내는 법과 자료형에서 사용되는 키워드를 나타냅니다.

{% highlight c++ %}
bool b; // boolean 자료형
char c; // character 자료형
int n; // integer 자료형
double d; // double-precision floating point 자료형
{% endhighlight %}

* extern
extern을 키워드로 사용한 자료형은 전역변수로 사용됩니다.(cpp, cpp간의 공유 가능)

* static
static 키워드로 사용한 자료형은 객체들끼리 공유하며 사용됩니다.(cpp간의 공유 불가)

* const
const를 키워드로 사용한 자료형은 값을 변경할 수 없는 변수로 사용됩니다.

* volatile
volatile를 키워드로 사용한 자료형은 값을 가변 변수로 사용됩니다.

* register
register를 키워드로 사용한 자료형 cpu의 register에 저장 요청하여 빠르게 동작하는 변수로 사용됩니다.

* constexpr
constexpr를 키워드로 사용한 자료형은 compile시에 값을 결정하는 변수입니다. 복잡하거나 변경이 될 수 있는 경우 무시되거나 오류가 생길 수 있습니다.

## primitive data types
---
최적화 되어 있는 기본 자료형은 아래와 같습니다.

{% highlight c++ %}
bool b; // boolean 1byte
char c; // character 1byte(ASCII CODE)
wchar_t c; // character 4byte(UTF-8 CODE)
int n; // integer 4byte
long n; // integer 8byte
double d; // double-precision floating point 8byte
float f; // precision floating point 4byte
void; // null
{% endhighlight %}

## user defined types
---
사용자 정의 자료형은 다음과 같이 있으며, 또한 아래와 같이 선언하여 생성할 수도 있습니다.

{% highlight c++ %}
enum class COLOR { RED, GREEN, BLUE };

class MyClassType {
  public:
    MyClass() = default;
    ~MyClass() = default;
    int nID_;
};

struct MyStructType {
  int nNumber;
  std::string strName;
};
{% endhighlight %}

## type alias
---
타입은 다음과 같이 별칭을 정하여 사용할 수 있습니다.

{% highlight c++ %}
typedef unsigned int uint;
using uchar = unsigned char;
{% endhighlight %}

## type change
---
타입을 컴파일 할때 변경하는 법은 아래와 같이 있습니다.

{% highlight c++ %}
auto n = 10; // 컴파일시 자료형 결정
decltype(n) d = 3; // 자료형 참조하여 자료형 결정
{% endhighlight %}






{% highlight c++ %}

{% endhighlight %}








{% highlight c++ %}
{% endhighlight %}