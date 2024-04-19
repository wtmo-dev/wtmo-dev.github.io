---
title: "Ollama intro"
tags:
    - NLP
    - ollama
date: "2024-04-01"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# How to start
---
우선 ollama를 설치하여 진행해야하기 때문에 아래에서 OS에 맞는 ollama를 우선 설치해야 합니다.


ollama를 설치하였다면 사용할 모델을 아래와 같이 받으면 됩니다.

{% highlight shell %}
ollama pull <model>
{% endhighlight %}

다운받을 수있는 모델은 다음 홈페이지에서 확인이 가능합니다.
[ollama](https://ollama.com/library)

## check installed model
설치한 모델을 확인하려면 다음과 같이 확인이 가능합니다.

{% highlight shell %}
ollama list
{% endhighlight %}

## check installed model info
설치한 모델의 정보를 확인하려면 다음과 같이 확인이 가능합니다.

{% highlight shell %}
ollama show <model> {--license, --modelfile, --parameters, --system, --template}
{% endhighlight %}

## copy installed model
설치한 모델을 복제하려면 다음과 같이 진행이 가능합니다.

{% highlight shell %}
ollama cp <model> <cp_model_name>
{% endhighlight %}

## run model in CLI
설치한 모델을 CLI에서 실행하려면 다음과 같이 진행이 가능합니다.

{% highlight shell %}
ollama run <model>
{% endhighlight %}

## remove installed model
설치한 모델을 삭제하려면 다음과 같이 진행이 가능합니다.

{% highlight shell %}
ollama rm <model>
{% endhighlight %}
