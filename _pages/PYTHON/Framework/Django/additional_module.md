---
title: "Django additional module"
tags:
    - python
    - framework
    - Django
date: "2024-03-21"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# What is Django debug toolbar
---
Django의 webpage들에서 debug 정보를 바로 확인하기 위한 middleware입니다.

## How to setting
---
다음은 Django debug toolbar를 설치하는 방법입니다.

* django-debug-toolbar 설치
{% highlight shell %}
pip install django-debug-toolbar
{% endhighlight %}

* \<proj-name\>.settings.py에서 확인, 추가
{% highlight python %}
INSTALLED_APPS = [
    # ...
    "django.contrib.staticfiles",
    # ...
]

STATIC_URL = "static/"
{% endhighlight %}

* \<proj-name\>.settings.py에서 확인, 추가
{% highlight python %}
TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",
        "APP_DIRS": True,
        # ...
    }
]
{% endhighlight %}

* \<proj-name\>.settings.py에 추가
{% highlight python %}
INSTALLED_APPS = [
    # ...
    "debug_toolbar",
    # ...
]
{% endhighlight %}

* \<proj-name\>.urls.py에 추가
{% highlight python %}
from django.conf import settings

if settings.DEBUG:
    import mimetypes
    mimetypes.add_type("application/javascript", ".js", True)
    import debug_toolbar
    urlpatterns += [
        path(r'^__debug__/', include(debug_toolbar.urls)),
    ]
{% endhighlight %}

* \<proj-name\>.settings.py에 추가
{% highlight python %}
MIDDLEWARE = [
    # ...
    "debug_toolbar.middleware.DebugToolbarMiddleware",
    # ...
]
{% endhighlight %}

* \<proj-name\>.settings.py에 추가
{% highlight python %}
INTERNAL_IPS = [
    # ...
    "127.0.0.1",
    <any other urls you need>
    # ...
]
{% endhighlight %}

위의 방식을 전부 완료하고 나서 Django proj를 실행하면 오른쪽에 debug toolbar가 보여집니다. 혹시나 보여지지 않으시다면 아래의 코드를 추가해주세요.

* \<proj-name\>.urls.py에 추가
{% highlight python %}
import mimetypes
mimetypes.add_type("application/javascript", ".js", True)
{% endhighlight %}

# What is Django celery
---
Django에서 celery를 활용하여 worker와 broker를 사용하는 기능입니다.

## How to setting
---
다음은 Django celery(W.redis)를 설치하는 방법입니다.


* \<proj-name\>.celery.py 생성
{% highlight python %}
import os

from celery import Celery

# Set the default Django settings module for the 'celery' program.
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')

app = Celery('projs')

# Using a string here means the worker doesn't have to serialize
# the configuration object to child processes.
# - namespace='CELERY' means all celery-related configuration keys
#   should have a `CELERY_` prefix.
app.config_from_object('django.conf:settings', namespace='CELERY')

# Load task modules from all registered Django apps.
app.autodiscover_tasks()


@app.task(bind=True, ignore_result=True)
def debug_task(self):
    print(f'Request: {self.request!r}')
{% endhighlight %}

* \<proj-name\>.settings.py에 추가
{% highlight python %}
CELERY_BROKER_URL = 'redis://127.0.0.1:6379/0'
CELERY_RESULT_BACKEND = 'redis://127.0.0.1:6379/0'
CELERY_ACCEPT_CONTENT = ['application/json']
CELERY_RESULT_SERIALIZER = 'json'
CELERY_TASK_SERIALIZER = 'json'
CELERY_TIMEZONE = 'Asia/Seoul'
CELERY_BROKER_CONNECTION_RETRY_ON_STARTUP = True
{% endhighlight %}

* \<proj-name\>.\_\_init\_\_.py에 추가
{% highlight python %}
from .celery import app as celery_app

__all__ = ('celery_app',)
{% endhighlight %}

* shared_task 데코레이터를 사용한 함수 delay로 실행
{% highlight python %}
from celery import shared_task
{% endhighlight %}

위와 같이 코드를 완성하고 나서 다음의 코드로 celery를 구동시키면 사용이 가능합니다.

{% highlight shell %}
celery -A <proj-name> worker -l INFO
{% endhighlight %}
