---
title: "how to set python debug"
tags:
    - VSC
    - debug
date: "2023-12-15"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# how to set debug
---
우선 아래를 참고하여 기본적인 VSC setting에 접근하는 방법을 알아야 합니다.

[how to set VSC](../setting/setting.html)

ctrl+shift+d를 입력하면 debugger 모드에 접근이 가능합니다.

처음 세팅을 하는 경우는 왼쪽 상단에 아래와 같이 나타나며 "create a launch.json file"을 클릭해주시면 됩니다.

![debug](/assets/img/vsc/python/debug.PNG)

처음 세팅하시는분이 아니라면 아래와 같이 표현이 되기도 합니다. 다음의 경우도 표시된 버튼을 눌려주시면 위와 똑같이 launch.json 파일을 생성합니다.

![debug](/assets/img/vsc/python/debug1.PNG)

## for the virtual env user debug setting
---
가상환경을 사용한다면 위의 기본적인 debug 세팅 이후에 추가적인 세팅이 필요합니다.
아래와 같이 사용하는 가상환경의 python interpreter로 구동되는 python을 연결해 주셔야 설치한 모듈들이 정상적으로 작동 되게 되어있습니다.

{% highlight shell %}
{
    "version": "0.2.0",
    "configurations": [
        {
            "python": "C:/Users/<user>/.virtualenvs/<venv>/Scripts/python",
        }
    ]
}
{% endhighlight %}

