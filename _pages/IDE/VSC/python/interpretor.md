---
title: "how to set python interpreter"
tags:
    - VSC
    - interpreter
date: "2023-12-14"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# how to set interpreter
---
우선 아래를 참고하여 기본적인 VSC setting에 접근하는 방법을 알아야 합니다.

[how to set VSC](../setting/intro.html)

이후 json 파일에서 default interpreter를 아래와 같이 각자 python 위치를 활용하여 작성해줍니다.

{% highlight shell %}
"python.defaultInterpreterPath": "%path%\\python.exe"
{% endhighlight %}

위의 세팅이 완료된 이후에 ```ctrl+shift+p```를 입력후 Python: Select Interpreter를 선택합니다.
default로 선택한 interpreter가 바로 보일경우 필요한 워크스페이스를 선택하여도 되며, 아닐경우 맨아래 select at workspace level을 선택하여 더 세부적인 interpreter를 선택할 수 있습니다.

select at workspace level을 누르셨다면, 자체적으로 잡히는 Venv를 선택해도 됩니다. 또는 Enter interpreter path를 통하여 직접 interpreter를 찾아서 선택해 주어도 됩니다.

위의 세팅이 전부 완료된 이후 ```ctrl+shift+` ```를 입력하여 새로운 터미널을 열게 되면 interpreter가 적용된것을 알 수 있습니다.