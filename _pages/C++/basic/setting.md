---
title: "c++ setting"
tags:
    - c++
    - basic
date: "2024-04-11"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# How to set c++
---
c++를 설정하는 방법은 다음과 같습니다.

## Window
---
[wsl](/OS/Window/WSL/intro.html)을 활용하여 wsl상에서 linux를 참고하여 설정을 하거나 MinGW을 설치하여 직접 사용할 수 있습니다.

[MinGW](https://www.mingw-w64.org/downloads/#mingw-builds)에서 최신버전을 설치합니다.

* 환경 변수 설정
{% highlight shell %}
[System.Environment]::GetEnvironmentVariable("PATH") # mingw64가 있는지 확인

[System.Environment]::SetEnvironmentVariable("PATH", $env:Path + ";C:\mingw64\bin") # path 설정
{% endhighlight %}

IDE 세팅은 각각의 IDE의 세팅을 사용하면 됩니다.

## Mac
---
mac의 경우 세팅이 쉽습니다.

{% highlight shell %}
xcode-select --install
{% endhighlight %}

IDE 세팅은 각각의 IDE의 세팅을 사용하면 됩니다.

## Linux
---
linux의 경우에도 세팅이 쉽습니다.

{% highlight shell %}
gcc -v # 설치 확인

sudo apt-get update # apt update
sudo apt-get install build-essential gdb # 설치
{% endhighlight %}

IDE 세팅은 각각의 IDE의 세팅을 사용하면 됩니다.
