---
title: "Celery"
tags:
    - python
    - framework
    - Celery
date: "2024-02-19"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---
# What is Celery
---
Celery는 일종의 worker와 같습니다. worker는 broker라는 매개체를 이용하여 작업을 분산적으로 동작하게 해줍니다. broker는 redis나 RabbitMQ와 같은것들을 활용하여 동작됩니다.

# How to use Celery
---
celery는 다음의 순서로 실행이 가능합니다.

{% highlight shell %}
pip install -U Celery # install celery
{% endhighlight %}

이후의 다양한 [bundles](https://github.com/celery/celery?tab=readme-ov-file#bundles)이 존재하기 때문에 필요 상황에 맞게 다운 받아서 사용하면 됩니다. 아래는 기초적인 사용 예시를 첨부하였습니다.

{% highlight python %}
from celery import Celery

app = Celery('hello', broker='amqp://guest@localhost//')

@app.task
def hello():
    return 'hello world'
{% endhighlight %}

{% highlight python %}
celery -A <proj-name> worker
{% endhighlight %}