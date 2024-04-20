---
title: "Llamaindex documents Advance(1)"
tags:
    - NLP
    - llamaindex
    - documents
date: "2024-03-07"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# documents loaders
---

## flat document
---
documents는 다양한 형태를 가진 파일들을 불러오는데 사용이 될 수 있으나, 단순한 파일을 불러올 수도 있습니다. 단순한 파일을 불러올때는 아래와 같이 단순한 방식이 제공됩니다.

{% highlight python %}
from llama_index.readers.file import FlatReader
from pathlib import Path

md_docs = FlatReader().load_data(Path("./test.md"))
{% endhighlight %}

## other document loader
---
[other document loader](https://docs.llamaindex.ai/en/stable/module_guides/loading/connector/modules/)

# metadata extraction usage pattern
---
다음과 같이 LLM을 사용하여 metadata를 추출해낼 수 있습니다.

{% highlight shell %}
pip install llama-index-extractors-entity
{% endhighlight %}

{% highlight python %}
import os

OPENAI_API_TOKEN = "sk-"
os.environ["OPENAI_API_KEY"] = OPENAI_API_TOKEN
llm = OpenAI(temperature=0.1, model="gpt-3.5-turbo", max_tokens=512)

from llama_index.core.extractors import (
    TitleExtractor,
    QuestionsAnsweredExtractor,
    SummaryExtractor,
    KeywordExtractor,
    BaseExtractor,
)
from llama_index.extractors.entity import EntityExtractor

class CustomExtractor(BaseExtractor):
    def extract(self, nodes):
        metadata_list = [
            {
                "custom": (
                    node.metadata["document_title"]
                    + "\n"
                    + node.metadata["excerpt_keywords"]
                )
            }
            for node in nodes
        ]
        return metadata_list

title_extractor = TitleExtractor(nodes=5)
qa_extractor = QuestionsAnsweredExtractor(questions=3)
summary_extractor = SummaryExtractor(summaries=["prev", "self","next"])
keyword_extractor = KeywordExtractor(keywords=10, llm=llm),
custom_extractor = CustomExtractor()

entity_extractor = EntityExtractor(
    prediction_threshold=0.5,
    label_entities=False,  # include the entity label in the metadata (can be erroneous)
    device="cpu",  # set to "cuda" if you have a GPU
)
{% endhighlight %}

# pipeline
---
[nodes advance(1)](./nodes advance(1).html)까지 확인 이후 pipeline을 아래와 같이 도입 가능합니다.

[document node pipeline](./pipeline.html#pipelinew-document-node)