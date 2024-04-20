---
title: "Llamaindex intro"
tags:
    - NLP
    - llamaindex
date: "2024-03-05"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# How to start
---
라마 인덱스를 활용하는 방법은 3가지가 있습니다. 첫번째는 initial setting, 두번째는 custom setting, 세번째는 source에서 직접 설치하는 방법입니다.

## init install
---
기초적인 설치방법으로 OpenAI와 같이 대표적인 LLM을 활용하는데 있어서 적절합니다.

{% highlight shell %}
pip install llama-index
{% endhighlight %}

## custom install
---
개별적 모델을 활용하기 위한 설치방법으로 OpenAI와 같이 대표적인 LLM 이외에도 다양한 모델을 Ollama 또는 huggingface등에서 가져와서 활용이 가능합니다.

{% highlight shell %}
pip install llama-index-core llama-index-readers-file llama-index-llms-ollama llama-index-embeddings-huggingface
{% endhighlight %}

## source install
--- 
위 두가지 설치가 작동이 되지 않거나, source에서 직접 원하는것들만 설치를 하고 싶을때 사용할 수 있습니다.

{% highlight shell %}
git clone https://github.com/jerryjliu/llama_index.git

pip install -e llama-index-integrations/llms/llama-index-llms-ollama
{% endhighlight %}

# simple start example
---
아래의 예시는 RAG를 활용한 예시입니다. ./data/paul_graham/ 폴더를 생성하여 RAG에 사용할 txt 데이터를 넣으면 됩니다. 또는 아래의 코드를 통하여 공식적인 예시 데이터를 사용할 수 있습니다.

{% highlight shell %}
mkdir -p 'data/paul_graham/'
wget 'https://raw.githubusercontent.com/run-llama/llama_index/main/docs/docs/examples/data/paul_graham/paul_graham_essay.txt' -O 'data/paul_graham/paul_graham_essay.txt'
{% endhighlight %}

## W. OpenAI
---
OpenAI를 사용하여 활용을 하려면 우선 아래와 같이 환경설정이 필요합니다.

{% highlight shell %}
export OPENAI_API_KEY=XXXXX # linux
set OPENAI_API_KEY=XXXXX # window
{% endhighlight %}

이후 아래의 코드로 간단하게 활용이 가능합니다.

{% highlight python %}
import os

from llama_index.core import (
    VectorStoreIndex,
    SimpleDirectoryReader,
    StorageContext,
    load_index_from_storage,
)

# check if local storage already exists
PERSIST_DIR = "./storage"
if not os.path.exists(PERSIST_DIR):
    # load the documents and create the index
    documents = SimpleDirectoryReader("./data/paul_graham/").load_data()
    index = VectorStoreIndex.from_documents(documents)
    # store it for later
    index.storage_context.persist(persist_dir=PERSIST_DIR)
else:
    # load the existing index
    storage_context = StorageContext.from_defaults(persist_dir=PERSIST_DIR)
    index = load_index_from_storage(storage_context)

# Either way we can now query the index
query_engine = index.as_query_engine()
response = query_engine.query("{Question}")
print(response)
{% endhighlight %}

## W. Custom model(ollama)
---
ollama를 사용하기 위하여 기본 설치 및 사용법을 알아야합니다. 사용법은 아래를 참고하면 됩니다.
[how to use ollama](../ollama/intro.html)

ollama 사용법 숙지 이후 사용할 모델을 다운 받고 아래의 코드로 진행이 가능합니다.

{% highlight python %}
from llama_index.core import VectorStoreIndex, SimpleDirectoryReader, Settings
from llama_index.core.embeddings import resolve_embed_model
from llama_index.llms.ollama import Ollama

documents = SimpleDirectoryReader("./data/paul_graham/").load_data()

# bge embedding model
Settings.embed_model = resolve_embed_model("local:BAAI/bge-small-en-v1.5")

# ollama
Settings.llm = Ollama(model=<model>, request_timeout=30.0)

index = VectorStoreIndex.from_documents(
    documents,
)

query_engine = index.as_query_engine()
response = query_engine.query("{Question}")
print(response)
{% endhighlight %}

## W. Custom model(hugging face)
---
hugging face를 사용하기 위하여 기본 설치 및 사용법을 알아야합니다. 사용법은 아래를 참고하면 됩니다.
[how to use hugging face](../hugging face/intro.html)

hugging face 사용법 숙지 이후 추가적으로 아래의 필요 모듈을 다운받아야 합니다.
{% highlight shell %}
pip install llama-index-llms-huggingface
pip install llama-index
{% endhighlight %}

이후 아래의 코드로 실행해 볼 수 있습니다.

{% highlight python %}
# setup prompts - specific to StableLM
from llama_index.core import VectorStoreIndex, SimpleDirectoryReader, Settings, PromptTemplate
from llama_index.llms.huggingface import HuggingFaceLLM
import torch

# load documents
documents = SimpleDirectoryReader("./data/paul_graham/").load_data()

# This will wrap the default prompts that are internal to llama-index
# taken from https://huggingface.co/Writer/camel-5b-hf
query_wrapper_prompt = PromptTemplate(
    "Below is an instruction that describes a task. "
    "Write a response that appropriately completes the request.\n\n"
    "### Instruction:\n{query_str}\n\n### Response:"
)

llm = HuggingFaceLLM(
    context_window=2048,
    max_new_tokens=256,
    generate_kwargs={"temperature": 0.25, "do_sample": False},
    query_wrapper_prompt=query_wrapper_prompt,
    tokenizer_name="Writer/camel-5b-hf",
    model_name="Writer/camel-5b-hf",
    device_map="auto",
    tokenizer_kwargs={"max_length": 2048},
    # uncomment this if using CUDA to reduce memory usage
    # model_kwargs={"torch_dtype": torch.float16}
)

Settings.chunk_size = 512
Settings.llm = llm

index = VectorStoreIndex.from_documents(documents)

# set Logging to DEBUG for more detailed outputs
query_engine = index.as_query_engine()
response = query_engine.query("What did the author do growing up?")

print(response)
{% endhighlight %}

## streaming service
---
스트리밍 서비스로 작동을 하기 위하여 index.as_query_engine()에서 부터 아래와 같이 변경을 해주면 됩니다.

{% highlight python %}
query_engine = index.as_query_engine(streaming=True)

# set Logging to DEBUG for more detailed outputs
response_stream = query_engine.query("What did the author do growing up?")

# can be slower to start streaming since llama-index often involves many LLM calls
response_stream.print_response_stream()

# can also get a normal response object
response = response_stream.get_response()
print(response)
{% endhighlight %}