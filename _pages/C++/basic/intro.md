---
title: "c++ intro"
tags:
    - c++
    - basic
date: "2024-04-10"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# how to install c++
---
c++을 사용하기 위하여 IDE는 VSC를 설치하면 됩니다. 하지만 compile을 위하여 추가적으로 설치가 필요한 요인들이 있습니다. 이는 아래를 참고하여 설정하여 주세요.

[setting](./setting.html)

# default form
---
아래는 가장 기본적인 c++의 형태를 나타냅니다. 

{% highlight c++ %}
#include <iostream>
#include <cstdlib>

using std::cout; // namespace 요약
using std::endl;

int main(int argc, char *argv[])
{
    std::cout << "Hello, world!" << std::endl;
    return EXIT_SUCCESS; // 0과 같은 값을 반환
}
{% endhighlight %}

# compile
---
아래는 c++을 동작하기 위하여 compile 하는 방식입니다. 아래의 방식 이외에도 IDE에서 구동하여 확인 할 수 있습니다. 

* Debug mode
{% highlight shell %}
g++ -Wall -W -m64 --save-temps -std=c++2a -g -D_DEBUG -o <out_file> <file>.cpp
{% endhighlight %}

* Release mode
{% highlight shell %}
g++ -Wall -W -m64 --save-temps -std=c++2a -O2 -o <out_file> <file>.cpp
{% endhighlight %}

* W. MAKE file
아래와 같이 make file을 만들어서 명령어로 동작할 수 있습니다.
{% highlight shell %}
SHELL=/bin/sh
MAKE=make -f Makefile.gcc.linux.x86_64.5.4.0
MAKEINSTALL=$(MAKE) install
MAKECLEAN=$(MAKE) clean
MAKEUNINSTALL=$(MAKE) uninstall

CXX = g++
CC = gcc

SUBS = lib \
    bin

all:
    -for c in $(SUBS); do echo "=== $$c =="; (cd $$c; $(MAKE) "CXX=$(CXX)" "CC=$(CC)") done

clean:
    -for c in $(SUBS); do echo "=== $$c =="; (cd $$c; $(MAKECLEAN) "CXX=$(CXX)" "CC=$(CC)") done

install:
    -for c in $(SUBS); do echo "=== $$c =="; (cd $$c; $(MAKEINSTALL) "CXX=$(CXX)" "CC=$(CC)") done

uninstall:
    -for c in $(SUBS); do echo "=== $$c =="; (cd $$c; $(MAKEUNINSTALL) "CXX=$(CXX)" "CC=$(CC)") done
{% endhighlight %}

# type of JAVA
---
[link](./type.html)
