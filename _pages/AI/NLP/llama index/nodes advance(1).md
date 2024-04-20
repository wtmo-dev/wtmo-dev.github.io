---
title: "Llamaindex nodes Advance(1)"
tags:
    - NLP
    - llamaindex
    - nodes
date: "2024-03-11"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# create node by async
---
node를 만들때 다음과 같이 비동기로 만들 수 있습니다.

{% highlight python %}
from llama_index.core.node_parser import SentenceSplitter

node_parser = SentenceSplitter(chunk_size=512)

nodes = await node_parser.acall(documents)
{% endhighlight %}

# file base node parser
---
노드를 생성하는데 있어서 document들이 다양한 형태의 데이터를 가질 수 있으며, 각 데이터에 최적화된 node parser를 사용하는것이 성능에 영향을 미칠 수 있습니다.

## simple file
---
가장 기본적인 형태의 txt와 같은 파일에 적절한 파서입니다. 이는 [flat document](./documents advance(1).html#flat-document) 와 같이 활용하기에 적합합니다.

{% highlight python %}
from llama_index.core.node_parser import SimpleFileNodeParser

parser = SimpleFileNodeParser()
md_nodes = parser.get_nodes_from_documents(md_docs)
{% endhighlight %}

## html file
---
HTML 파일을 사용하는데 최적화된 파서입니다. tag들을 기본적으로 제공하며 custom tag를 세팅할 수 있습니다.

{% highlight python %}
from llama_index.core.node_parser import HTMLNodeParser

parser = HTMLNodeParser(tags=["p", "h1"])  # optional list of tags
nodes = parser.get_nodes_from_documents(html_docs)
{% endhighlight %}

## json file
---
JSON 파일을 사용하는데 최적화된 파서입니다.

{% highlight python %}
from llama_index.core.node_parser import JSONNodeParser

parser = JSONNodeParser()
nodes = parser.get_nodes_from_documents(json_docs)
{% endhighlight %}

## markdown file
---
markdown 파일을 사용하는데 최적화된 파서입니다.

{% highlight python %}
from llama_index.core.node_parser import MarkdownNodeParser

parser = MarkdownNodeParser()
nodes = parser.get_nodes_from_documents(markdown_docs)
{% endhighlight %}

# text base node parser
---
노드를 생성하는데 있어서 text를 기반으로 생성이 필요한 경우 아래의 방식을 사용할 수 있습니다.

## code splitter
---
code 파일을 사용하는데 최적화된 파서입니다. 지원되는 code 목록은 다음과 같습니다.
[available code file](https://github.com/grantjenks/py-tree-sitter-languages#license)

{% highlight python %}
from llama_index.core.node_parser import CodeSplitter

splitter = CodeSplitter(
    language="python",
    chunk_lines=40,  # lines per chunk
    chunk_lines_overlap=15,  # lines overlap between chunks
    max_chars=1500,  # max chars per chunk
)
nodes = splitter.get_nodes_from_documents(documents)
{% endhighlight %}

## langchain splitter
---
langchain에서 사용하는 textsplitter를 사용할 수 있는 파서입니다.

{% highlight python %}
from langchain.text_splitter import RecursiveCharacterTextSplitter
from llama_index.core.node_parser import LangchainNodeParser

parser = LangchainNodeParser(RecursiveCharacterTextSplitter())
nodes = parser.get_nodes_from_documents(documents)
{% endhighlight %}

지원하지 않는 langchain parser의 경우 아래와 같이 생성하여 사용할 수 있습니다.

[create langchain parser](https://docs.llamaindex.ai/en/stable/api_reference/node_parsers/langchain/)

## sentence splitter
---
문장과 문장의 끊어짐을 보장하며 분할을 할 수 있는 파서입니다.

{% highlight python %}
from llama_index.core.node_parser import SentenceSplitter

splitter = SentenceSplitter(
    chunk_size=1024,
    chunk_overlap=20,
)
nodes = splitter.get_nodes_from_documents(documents)
{% endhighlight %}

## sentence window splitter
---
[sentence splitter](#sentence-splitter)와 유사하지만 해당 노드 주변의 window_size만큼의 값을 가지게 됩니다. 이것은 다음 예시와 같이 활용이 가능합니다. [MetadataReplacementNodePostProcessor](https://docs.llamaindex.ai/en/stable/examples/node_postprocessor/MetadataReplacementDemo/)

{% highlight python %}
import nltk
from llama_index.core.node_parser import SentenceWindowNodeParser

node_parser = SentenceWindowNodeParser.from_defaults(
    # how many sentences on either side to capture
    window_size=3,
    # the metadata key that holds the window of surrounding sentences
    window_metadata_key="window",
    # the metadata key that holds the original sentence
    original_text_metadata_key="original_sentence",
)
{% endhighlight %}

## semantic splitter
---
고정된 크기의 chunk로 node가 구성이 되지만, embedding을 활용하여 유사성을 고려한 방식으로 효과적인 방식입니다.

{% highlight python %}
from llama_index.core.node_parser import SemanticSplitterNodeParser
from llama_index.embeddings.openai import OpenAIEmbedding

embed_model = OpenAIEmbedding()
splitter = SemanticSplitterNodeParser(
    buffer_size=1, breakpoint_percentile_threshold=95, embed_model=embed_model
)
{% endhighlight %}

## token splitter
---
token 크기에 기반하여 chunking을 하는 방식입니다.

{% highlight python %}
from llama_index.core.node_parser import TokenTextSplitter

splitter = TokenTextSplitter(
    chunk_size=1024,
    chunk_overlap=20,
    separator=" ",
)
nodes = splitter.get_nodes_from_documents(documents)
{% endhighlight %}

# relation base node parser
---
노드를 생성하는데 있어서 관계성을 기반으로 생성이 필요한 경우 아래의 방식을 사용할 수 있습니다.

## hierarchical splitter
---
계층 구조로 chunking을 진행하여, 하위 레벨의 node는 상위 레벨의 node와 같이 활용 되어 좋은 결과를 도출할 수 있습니다. 다음의 예시와 같이 활용하면 적절합니다. [AutoMergingRetriever](https://docs.llamaindex.ai/en/stable/examples/retrievers/auto_merging_retriever/)

{% highlight python %}
from llama_index.core.node_parser import HierarchicalNodeParser

node_parser = HierarchicalNodeParser.from_defaults(
    chunk_sizes=[2048, 512, 128]
)
{% endhighlight %}

# pipeline
---
[documents advance(1)](./documents advance(1).html)까지 확인 이후 pipeline을 아래와 같이 도입 가능합니다.

[document node pipeline](./pipeline.html#pipelinew-document-node)