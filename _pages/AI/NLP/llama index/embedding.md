---
title: "Llamaindex embedding"
tags:
    - NLP
    - llamaindex
    - embedding
date: "2024-03-13"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# what is embedding
---
embedding은 입력을 받은 document or node에 있어서 vector로 나타내는것입니다. 이를 통하여 코사인 유사도와 같이 문서들간의 유사성을 계산하여 문서를 효율적으로 사용할 수 있게 됩니다. llama는 기본적으로 코사인 유사도를 사용하고 있으며 아래의 방식으로 다양한 embedding을 사용해 볼 수 있습니다.

## W. OpenAI
---
OpenAI에서 사용하는 embedding을 사용하려면 아래와 같이 사용하면 됩니다. 하지만 유료인점을 참고해야합니다.

{% highlight shell %}
pip install llama-index-embeddings-openai
{% endhighlight %}

{% highlight python %}
import os

OPENAI_API_TOKEN = "sk-"
os.environ["OPENAI_API_KEY"] = OPENAI_API_TOKEN

from llama_index.embeddings.openai import OpenAIEmbedding
from llama_index.core import Settings

# global
Settings.embed_model = OpenAIEmbedding(embed_batch_size=42) # default is 10

# per-index
index = VectorStoreIndex.from_documents(documents, embed_model=embed_model)
{% endhighlight %}

## W. hugging face
---
hugging face를 사용하여 enbedding을 하는 방식은 아래와 같습니다.

{% highlight shell %}
pip install llama-index-embeddings-huggingface
{% endhighlight %}

{% highlight python %}
from llama_index.embeddings.huggingface import HuggingFaceEmbedding
from llama_index.core import Settings

Settings.embed_model = HuggingFaceEmbedding(
    model_name="BAAI/bge-small-en-v1.5"
)
{% endhighlight %}

## W. hugging face(W. ONNX)
---
hugging face를 ONNX로 사용하는 법은 아래와 같습니다.

{% highlight shell %}
pip install transformers optimum[exporters]
pip install llama-index-embeddings-huggingface-optimum
{% endhighlight %}

{% highlight python %}
from llama_index.embeddings.huggingface_optimum import OptimumEmbedding

OptimumEmbedding.create_and_save_optimum_model(
    "BAAI/bge-small-en-v1.5", "./bge_onnx"
)

Settings.embed_model = OptimumEmbedding(folder_name="./bge_onnx")
{% endhighlight %}

## W. langchain
---
langchain에서 지원하는 다양한 embedding을 사용할 수 있습니다.
[langchain embeddings list](https://python.langchain.com/docs/modules/data_connection/text_embedding/)

{% highlight shell %}
pip install llama-index-embeddings-langchain
{% endhighlight %}

{% highlight python %}
from langchain.embeddings.huggingface import HuggingFaceBgeEmbeddings
from llama_index.core import Settings

Settings.embed_model = HuggingFaceBgeEmbeddings(model_name="BAAI/bge-base-en")
{% endhighlight %}

## W. custom embedding
---
위에서 사용할 수 있는 다양한 embedding 이외에 다른 embedding을 직접 만들어서 활용하려면 아래와 같이 해볼 수 있습니다.

{% highlight python %}
from typing import Any, List
from InstructorEmbedding import INSTRUCTOR
from llama_index.core.embeddings import BaseEmbedding

class InstructorEmbeddings(BaseEmbedding):
    def __init__(
        self,
        instructor_model_name: str = "hkunlp/instructor-large",
        instruction: str = "Represent the Computer Science documentation or question:",
        **kwargs: Any,
    ) -> None:
        self._model = INSTRUCTOR(instructor_model_name)
        self._instruction = instruction
        super().__init__(**kwargs)

        def _get_query_embedding(self, query: str) -> List[float]:
            embeddings = self._model.encode([[self._instruction, query]])
            return embeddings[0]

        def _get_text_embedding(self, text: str) -> List[float]:
            embeddings = self._model.encode([[self._instruction, text]])
            return embeddings[0]

        def _get_text_embeddings(self, texts: List[str]) -> List[List[float]]:
            embeddings = self._model.encode(
                [[self._instruction, text] for text in texts]
            )
            return embeddings

        async def _get_query_embedding(self, query: str) -> List[float]:
            return self._get_query_embedding(query)

        async def _get_text_embedding(self, text: str) -> List[float]:
            return self._get_text_embedding(text)
{% endhighlight %}

## other embeddings
---
이외에도 다양한 embedding을 사용할 수 있으며 아래는 지원하는 embedding list 입니다.

[embeddings list](https://docs.llamaindex.ai/en/stable/module_guides/models/embeddings/#list-of-supported-embeddings)
