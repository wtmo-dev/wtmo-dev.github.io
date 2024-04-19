---
title: "가상환경 설정"
tags:
    - python
    - env
date: "2023-09-05"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# venv(normal setting, makedir it self)
---
{% highlight shell %}
python -m venv \<venv_name\>
source \<venv_name\>/bin/activate # mac
source \<venv_name\>/Script/activate # git bash with window
Scripts\activate.bat # cmd with window
deactivate
{% endhighlight %}

# pipenv(not makedir it self)
---
{% highlight shell %}
pip install pipenv
python -m pipenv --python \<version\>
python -m pyenv versions # 여기에 버전들 깔림
python -m pipenv shell
exit
{% endhighlight %}

* pipenv --venv  
* pipenv --py  
* pipenv run python # 가상환경으로 파이썬 실행하기  

## jupyter setting
---
{% highlight shell %}
pip install jupyter
pip install ipykernel
python -m ipykernel install — user — name 가상환경이름
jupyter kernelspec list
jupyter kernelspec uninstall 가상환경이름
{% endhighlight %}