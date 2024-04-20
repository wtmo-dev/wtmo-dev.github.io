---
title: "Llamaindex pipeline"
tags:
    - NLP
    - llamaindex
    - pipeline
date: "2024-03-14"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# pipeline(W. document, node)
---
documentd와 node를 하나의 pipeline으로 엮어서 사용하는 방식을 말합니다.

{% highlight python %}
import re
from llama_index.core import Document
from llama_index.embeddings.openai import OpenAIEmbedding
from llama_index.core.node_parser import SentenceSplitter
from llama_index.core.ingestion import IngestionPipeline
from llama_index.core.schema import TransformComponent


class TextCleaner(TransformComponent):
    def __call__(self, nodes, **kwargs):
        for node in nodes:
            node.text = re.sub(r"[^0-9A-Za-z ]", "", node.text)
        return nodes

# use in a pipeline
pipeline = IngestionPipeline(
    transformations=[
        SentenceSplitter(chunk_size=25, chunk_overlap=0),
        TextCleaner(),
        OpenAIEmbedding(),
    ],
)

nodes = pipeline.run(documents=[Document.example()])
{% endhighlight %}

# pipeline(W. document, node, index)
---
{% highlight python %}
from llama_index.core import VectorStoreIndex
from llama_index.core.extractors import (
    TitleExtractor,
    QuestionsAnsweredExtractor,
)
from llama_index.core.ingestion import IngestionPipeline
from llama_index.core.node_parser import TokenTextSplitter

transformations = [
    TokenTextSplitter(chunk_size=512, chunk_overlap=128),
    TitleExtractor(nodes=5),
    QuestionsAnsweredExtractor(questions=3),
]

# global
from llama_index.core import Settings

Settings.transformations = [text_splitter, title_extractor, qa_extractor]

# per-index
index = VectorStoreIndex.from_documents(
    documents, transformations=transformations
)
{% endhighlight %}