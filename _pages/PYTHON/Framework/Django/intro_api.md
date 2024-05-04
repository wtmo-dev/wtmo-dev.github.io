---
title: "Django rest api"
tags:
    - python
    - framework
    - Django
date: "2024-03-21"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# How to start Django restfulAPI
---
Django를 활용하여 REST API를 만드는데 최적화 되어 있는 모듈입니다. 다음의 방식으로 다운받을 수 있습니다.

{% highlight shell %}
pip install djangorestframework
pip install markdown       # Markdown support for the browsable API.
pip install django-filter  # Filtering support
{% endhighlight %}

* setting.py
{% highlight python %}
INSTALLED_APPS = [ # default setting
    ...,
    'rest_framework',
]
REST_FRAMEWORK = [ # additional pagination setting
    'DEFAULT_PAGINATIOM_CLASS': 'rest_framework.pagination.pageNumberPagination',
    'PAGE_SIZE': 50
]
{% endhighlight %}

# Next step
---
[models](models.html)

[serializers](serializers.html)

[views](views.html)

# Prev(how to start)
---
[Prev](intro.html)
