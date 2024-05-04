---
title: "JAVA setting"
tags:
    - JAVA
    - basic
date: "2024-04-02"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# How to set JAVA
---
JAVA를 설정하는 방법은 다음과 같습니다.

## Window
---
우선 JAVA가 설치되었는지 확인을 위하여 powershell에서 다음을 입력합니다.

{% highlight shell %}
java -version # java 버전 확인

[System.Environment]::GetEnvironmentVariable("JAVA_HOME") # java path가 설정되었는지 확인
[System.Environment]::GetEnvironmentVariable("PATH") # java path가 설정되었는지 확인
{% endhighlight %}

위의 설정확인 이후에 설정이 안되어 있는 파트를 아래에서 설치 밑 설정하면 됩니다.

[java download](https://www.oracle.com/java/technologies/downloads/#java17)

JAVA 환경설정을 위하여 powershell에서 다음을 입력합니다. 경로의 경우 다운 받으면서 설치한 위치를 입력하면 됩니다.

{% highlight shell %}
[System.Environment]::SetEnvironmentVariable("JAVA_HOME", "<java_path>") # ex) C:/Program Files/Java/jdk-17

[System.Environment]::SetEnvironmentVariable("PATH", $env:Path + ";%JAVA_HOME%\bin") # path 설정
{% endhighlight %}

## Mac
---
우선 JAVA가 설치되었는지 확인을 위하여 terminal에서 다음을 입력합니다.

{% highlight shell %}
java -version # java 버전 확인

which java # java 설치 위치 확인
{% endhighlight %}

[java download](https://www.oracle.com/kr/java/technologies/downloads/#jdk17-mac)

설치 이후 또는 동작하다가 경로의 문제로 동작이 안될 수 있습니다. 그럴 경우에 path를 설정해주면 됩니다.

{% highlight shell %}
vi ~/.zsh_profile # zsh_profile 열기, 아래 내용 추가 후 저장

JAVA_HOME=<path> # ex) /Library/Java/JavaVirtualMachines/jdk-11.jdk/Contents/Home
PATH=$PATH:$JAVA_HOME/bin
export JAVA_HOME
export PATH

source ~/.zsh_profile # zsh_profile 적용
{% endhighlight %}


## Linux
---
우선 JAVA가 설치되었는지 확인을 위하여 terminal에서 다음을 입력합니다.

{% highlight shell %}
java -version # java 버전 확인

which java # java 설치 위치 확인
{% endhighlight %}

설치가 안되어 있으면 아래의 방식으로 설정해주면 됩니다.

{% highlight shell %}
sudo yum list | grep jdk # 설치 가능한 jdk 확인

sudo yum install java-1.8.0-openjdk # 설치하고자 하는 버전 설치

which java # 설치한 위치 확인
readlink -f <java_path> # 위에서 확인한 위치의 정확한 위치 확인

cd etc/
vim profile

export JAVA_HOME=<real_java_path> # ex) /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.372.b07-1.el7_9.x86_64/jre/
export PATH=$JAVA_HOME/bin:$PATH
export CLASS_PATH=$JAVA_HOME/lib:$CLASS_PATH

source /etc/profile # 작성 옵션 적용
reboot # reboot
{% endhighlight %}
