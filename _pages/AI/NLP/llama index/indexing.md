---
title: "Llamaindex index"
tags:
    - NLP
    - llamaindex
    - index
date: "2024-03-12"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# what is index
---
index는 RAG와 같이 검색을 하는 구조에서 빠르게 검색하기 위한 구조입니다. 추가적인 활용처로는 채팅봇과 같이 QA로 사용할 수 있습니다.

## vector store index
---
index 기법에서 가장 흔하게 사용이 되는 방법입니다. 이는 vector store를 활용하여 indexing을 하는 방법입니다.

아래와 같이 [document](./documents.html)을 바로 활용하는 방법과 [node](./nodes.html)를 활용하는 방법 2가지로 이루어져 있습니다.

{% highlight python %}
from llama_index.core import VectorStoreIndex

index = VectorStoreIndex.from_documents(documents)
{% endhighlight %}

{% highlight python %}
from llama_index.core.schema import TextNode

node1 = TextNode(text="<text_chunk>", id_="<node_id>")
node2 = TextNode(text="<text_chunk>", id_="<node_id>")
nodes = [node1, node2]
index = VectorStoreIndex(nodes)
{% endhighlight %}

default vectorstore이외에도 다양한 [custom vectorstore](https://docs.llamaindex.ai/en/stable/module_guides/storing/vector_stores/)를 사용할 수 있으며 아래는 간단한 예시를 나타냅니다.

{% highlight python %}
import pinecone
from llama_index.core import (
    VectorStoreIndex,
    SimpleDirectoryReader,
    StorageContext,
)
from llama_index.vector_stores.pinecone import PineconeVectorStore

# init pinecone
pinecone.init(api_key="<api_key>", environment="<environment>")
pinecone.create_index(
    "quickstart", dimension=1536, metric="euclidean", pod_type="p1"
)

# construct vector store and customize storage context
storage_context = StorageContext.from_defaults(
    vector_store=PineconeVectorStore(pinecone.Index("quickstart"))
)

# Load documents and build index
documents = SimpleDirectoryReader(
    "../../examples/data/paul_graham"
).load_data()
index = VectorStoreIndex.from_documents(
    documents, storage_context=storage_context
)
{% endhighlight %}

## other index guides
---
vector store가 가장 흔한 indexing 기법이지만 그 이외에도 아래와 같이 다양한 기법들이 있습니다.
[other index guides](https://docs.llamaindex.ai/en/stable/module_guides/indexing/modules/)

# W. other embedding module
---
기본적으로 llama에서 제공하는 embedding으로 동작이 되지만 다른 embedding을 사용하고 싶으면 아래를 참고하여 변경이 가능합니다.

[embedding module](./embedding.html)

# pipeline
---
[documents advance(1)](./documents advance(1).html)와 [nodes advance(1)](./nodes advance(1).html)까지 확인 이후 pipeline을 아래와 같이 도입 가능합니다.

[document node index pipeline](./pipeline.html#pipelinew-document-node-index)