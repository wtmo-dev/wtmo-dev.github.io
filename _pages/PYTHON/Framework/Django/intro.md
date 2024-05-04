---
title: "Django intro"
tags:
    - python
    - framework
    - Django
date: "2024-03-20"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# What is Django
---
Django python으로 구현된 web framework입니다.

## Getting start
---
다음은 아주 기본적인 django 의 실행방식입니다.

{% highlight shell %}
pip install Django # Django 설치
python -m django --version # Django 설치 확인

django-admin startproject <proj-name> # <proj-name> 프로젝트 생성

cd <proj-name>
python manage.py runserver # <proj-name> 프로젝트 실행
{% endhighlight %}

다음은 ```startproject```로 생성되는 파일의 구조입니다.
> - \<proj-name\>/
>     - manage.py
>     - \<proj-name\>/
>         - \_\_init\_\_.py
>         - settings.py
>         - urls.py
>         - asgi.py
>         - wsgi.py

## Creating App
---
다음은 django에서 App을 만들고 연결하는 방법입니다.

{% highlight shell %}
python manage.py startapp <app-name> # create App
{% endhighlight %}

다음은 startapp으로 생성되는 dir의 구조 입니다.

> - \<app-name\>/
>     - \_\_init\_\_.py
>     - admin.py
>     - apps.py
>     - migrations/
>         - \_\_init\_\_.py
>     - models.py
>     - tests.py
>     - urls.py
>     - views.py

* \<app-name\>/views.py
{% highlight python %}
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
{% endhighlight %}

* \<app-name\>/urls.py
{% highlight python %}
from django.urls import path

from . import views

urlpatterns = [
    path("", views.index, name="index"),
]
{% endhighlight %}

* \<proj-name\>/urls.py
{% highlight python %}
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path("<app-name>/", include("<app-name>.urls")),
    path("admin/", admin.site.urls),
]
{% endhighlight %}

## Setting database
---
다음은 django에서 database를 세팅하는 방법입니다. Django는 기본으로 SQLite를 활용하지만 설정을 변경하여 수정이 가능합니다.

### mysql
---
다음은 mysql 예시입니다.

* 필수 모듈 설치
{% highlight shell %}
pip install mysqlclient
{% endhighlight %}

* \<proj-name\>.settings.py에 DB 옵션변경
{% highlight python %}
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': '<schema-name>',
        'USER': '',
        'PASSWORD': '',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
{% endhighlight %}

### postgre
---
다음은 postgre 예시입니다.

* 필수 모듈 설치
{% highlight shell %}
pip install psycopg2
{% endhighlight %}

* postgre setting
{% highlight shell %}
sudo su - postgres # postgre 실행
psql

CREATE DATABASE django_test; # postgre 유저 및 DB 생성
CREATE USER django_user WITH PASSWORD 'django_pass';
ALTER ROLE django_user SET client_encoding TO 'utf8';
ALTER ROLE django_user SET default_transaction_isolation TO 'read committed';
ALTER ROLE django_user SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE django_test TO django_user;
\q
{% endhighlight %}

* \<proj-name\>.settings.py에 DB 옵션변경
{% highlight python %}
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': '<schema-name>',
        'USER': '',
        'PASSWORD': '',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
{% endhighlight %}

# Next(Web page)
---
[Next](intro_web.html)

# Next(Rest API)
---
[Next](intro_api.html)
