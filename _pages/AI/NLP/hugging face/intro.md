---
title: "Hugging face intro"
tags:
    - NLP
    - hugging face
date: "2024-03-04"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# How to start
---
우선 허깅페이스에 가입을 해야합니다.
[Hugging face](https://huggingface.co/)

가입을 하고나면 아래와 같은 설명이 나옵니다.
![hugging face info](/assets/img/ai/nlp/hugging_face/hugging_face.PNG){: width="100%"}

## Authentication
---
홈페이지 가입이후 이메일의 인증을 해줘야하며, 인증을 완료하면 아래과 같이 organization을 설정할 수 있다. 이미 존재하는 organization에 가입하거나 직접 만들어주면 된다.
![hugging face info](/assets/img/ai/nlp/hugging_face/hugging_face1.PNG){: width="100%"}

이메일 인증 이후 setting에서 Authentication에 접근하면 아래와 같이 세팅을 할 수 있다. 2FA 세팅에는 google에서 제공하는 Authentication 어플을 활용하여 진행이 가능하다. 

![hugging face info](/assets/img/ai/nlp/hugging_face/hugging_face2.PNG){: width="100%"}

## create personal repository
---
홈페이지에서 관리할 수 있지만 CLI를 통하여 아래와 같이 관리가 가능하다. 홈페이지 setting에서 Access Tokens에 접근하면 token을 생성할 수 있습니다. token은 읽기용 쓰기용 2가지로 나뉘어 진다. 서버에서 가져와서 활용할때는 read, 서버에 등록할때는 write를 활용하면 됩니다.

{% highlight shell %}
pip install huggingface_hub

huggingface-cli login

huggingface-cli repo create <repo_name> --type {model, dataset, space}
{% endhighlight %}

## use personal repository
---
개인 레포지토리를 사용하려면 아래와 같이 가져와서 git과 같이 활용하면 됩니다.

{% highlight shell %}
git lfs install

git clone https://huggingface.co/<username>/<repo_name>
{% endhighlight %}

# use hugging face model
---
코드상으로 huggingface를 활용하려면 아래와 같은 폼을 활용하면 활용이 가능하다. 자세한 방법은 각각의 모델과 토크나이저를 업로드한 organization을 확인하면 됩니다.

{% highlight shell %}
from transformers import AutoModelForCausalLM, AutoTokenizer

REPO_ID = ""
FILENAME = ""
model_id = f"{REPO_ID}/{FILENAME}"

model = AutoModelForCausalLM.from_pretrained(model_id)
tokenizer = AutoTokenizer.from_pretrained(model_id)
{% endhighlight %}



