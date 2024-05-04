---
title: "redis"
tags:
    - redis
date: "2024-02-21"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# what is redis
---
우dd

# How to install redis
---
우dd


## Window
---
wsl을 설정 후 wsl에서 세팅이 가능합니다.

* 설치
{% highlight shell %}
curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list

sudo apt-get update
sudo apt-get install redis
{% endhighlight %}

* 실행
{% highlight shell %}
sudo service redis-server start
{% endhighlight %}

* 동작확인
{% highlight shell %}
redis-cli
ping
{% endhighlight %}