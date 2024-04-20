---
title: "Llamaindex retriever"
tags:
    - NLP
    - llamaindex
    - retriever
date: "2024-03-15"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# what is retriever
---
retriever는 검색엔진과 같은 역활을 합니다. index에 있는 값들을 query를 이용하여 관련된 내용을 추출해 내줍니다.

# how to use retriever
---
간단하게 사용하는 방식은 아래와 같이 사용할 수 있습니다.

{% highlight shell %}
retriever = index.as_retriever()
nodes = retriever.retrieve("{question}")
{% endhighlight %}

# how to use retriever advance
---
retriever를 사용하는 고급 기법이 아래와 같이 존재합니다. 이방식은 index의 종류별로 상세하게 세팅을 하는 방법이며 [retriever modes](https://docs.llamaindex.ai/en/stable/module_guides/querying/retriever/retriever_modes/)를 참고하여 다양한 retriever를 만들어 볼 수 있습니다.

{% highlight shell %}
retriever = summary_index.as_retriever(
    retriever_mode="llm",
    choice_batch_size=5,
)
{% endhighlight %}