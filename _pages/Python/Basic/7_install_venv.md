---
title: "파이썬 설치 및 가상환경 설정"
tags:
    - python
    - basic
date: "2023-08-17"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **python**
---
## **With. Window**
---
[다운로드 페이지](https://www.python.org/downloads/)

win+r → python → ok!

## **With. Mac**
---
[다운로드 페이지](https://www.python.org/downloads/macos/)

command+space → terminal → python3 → ok!

# **VSCode**
---
## **With. Window IDE setting**
---
[다운로드 페이지](https://code.visualstudio.com/)

## **With. Mac IDE setting**
---
[다운로드 페이지](https://code.visualstudio.com/)

# **virtual env**
---
## **With. Window**
---
{% highlight shell %}
python -m venv <env_name> → create venv

<env_name>\Scripts\activate → activate venv

pip list → pkg list

pip install <pkg_name>

deactivate
{% endhighlight %}
## **With. Mac**
---
{% highlight shell %}
python3 -m venv <env_name> → create venv

source ./<env_name>/Scripts/activate → activate venv

deactivate
{% endhighlight %}
