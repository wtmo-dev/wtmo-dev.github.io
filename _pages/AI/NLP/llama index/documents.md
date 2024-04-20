---
title: "Llamaindex documents"
tags:
    - NLP
    - llamaindex
    - documents
date: "2024-03-06"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# what is documents
---
documents는 다양한 NLP process에서 사용할 문서를 불러오는 방식을 말합니다.

# How to use documents tutorial
---
documents를 사용하는데 있어서 가장 기초적인 예시는 아래와 같습니다.

{% highlight python %}
from llama_index.core import Document, VectorStoreIndex

document = Document.example()

# build index
index = VectorStoreIndex.from_documents(documents)
{% endhighlight %}

# read documents
---
documents를 사용하는방법은 다양하게 존재합니다. 다음은 documents를 만드는 두가지 방법을 나타냅니다.

## Directory Reader
---
다음의 방식은 directory에 있는 문서들을 읽는 방식입니다. 해당방식은 지정한 폴더에 있는 문서는 읽을 수 있으나 하위 폴더에 있는 문서를 읽을 수는 없습니다.

{% highlight python %}
from llama_index.core import SimpleDirectoryReader

documents = SimpleDirectoryReader("./data").load_data()
{% endhighlight %}

## custom setting
---
다음의 방식은 사용자가 직접 지정한 문서들을 입력하는 방식입니다. 이는 text를 하나씩 지정해야하는 방식입니다.

{% highlight python %}
from llama_index.core import Document

text_list = [text1, text2, ...]
documents = [Document(text=t) for t in text_list]
{% endhighlight %}

# documents metadata
---
문서들은 다양한 metadata를 가지게 됩니다. 해당하는 metadata는 NLP process에서 중요한 역활을 하게 되며 해당하는 값들을 상세히 지정하는것은 중요합니다.

## add metadata(pre read)
---
document constructor를 만들기 이전에 metadata를 지정하는 방식은 다음과 같습니다.

### W. dir reader
---
다음과 같이 dir reader를 사용하면서 metadata들을 지정 할 수 있습니다.

{% highlight python %}
from llama_index.core import SimpleDirectoryReader

filename_fn = lambda filename: {"file_name": filename}

# automatically sets the metadata of each document according to filename_fn
documents = SimpleDirectoryReader(
    "./data",
    file_metadata=filename_fn,
    filename_as_id=True,
).load_data()
{% endhighlight %}

### W. custom reader
---
다음과 같이 custom reader를 사용하면서 metadata들을 지정 할 수 있습니다.

{% highlight python %}
document = Document(
    text="text",
    metadata={
        "filename": "<doc_file_name>",
        "category": "<category>",
        "doc_id": "<id>"},
)
{% endhighlight %}

## add metadata(after read)
---
document constructor를 만든 이후에 잘못된 metadata를 변경하는 방식은 다음과 같습니다.

{% highlight python %}
document.metadata = {"filename": "<doc_file_name>"}
document.doc_id = "My new document id!"
{% endhighlight %}

## advance metadata setting
---
다양한 metadata는 NLP process에 다양한 강점을 가질 수 있지만, 오히려 과한 정보로 혼란을 줄 수 있습니다. 이럴 경우 필요없는 정보를 배제할 수 있습니다.

다음은 LLM이 metadata를 활용하는지 설정하는것입니다.
{% highlight python %}
document.excluded_llm_metadata_keys = ["file_name"]
{% endhighlight %}

다음은 embedding 과정에서 metadata를 활용하는지 설정하는것입니다.
{% highlight python %}
document.excluded_embed_metadata_keys = ["file_name"]
{% endhighlight %}

다음은 위에서 설정한 metadata 배제를 한 이외의 값이 어떻게 보여지는지 확인하는 방법입니다.
{% highlight python %}
from llama_index.core.schema import MetadataMode

print(document.get_content(metadata_mode=MetadataMode.LLM))
print(document.get_content(metadata_mode=MetadataMode.EMBED))
{% endhighlight %}

이외에도 metadata의 format을 설정 가능합니다. 다음 예시에서는 format을 사용한 전체적인 사용법을 나타냅니다.

## advance metadata setting example
---
{% highlight python %}
from llama_index.core import Document
from llama_index.core.schema import MetadataMode

document = Document(
    text="This is a super-customized document",
    metadata={
        "file_name": "super_secret_document.txt",
        "category": "finance",
        "author": "LlamaIndex",
    },
    excluded_llm_metadata_keys=["file_name"],
    metadata_seperator="::",
    metadata_template="{key}=>{value}",
    text_template="Metadata: {metadata_str}\n-----\nContent: {content}",
)

print(
    "The LLM sees this: \n",
    document.get_content(metadata_mode=MetadataMode.LLM),
)
print(
    "The Embedding model sees this: \n",
    document.get_content(metadata_mode=MetadataMode.EMBED),
)
{% endhighlight %}

# Advance
---
[documents advance(1)](./documents advance(1).html)