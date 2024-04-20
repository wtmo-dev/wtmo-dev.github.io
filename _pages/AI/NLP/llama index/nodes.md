---
title: "Llamaindex nodes"
tags:
    - NLP
    - llamaindex
    - nodes
date: "2024-03-08"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# what is nodes
---
노드는 documents를 텍스트, 이미지 등등의 각 chunk로 나누는 것을 의미합니다. 이렇게 생성된 노드는 metadata정보와 관계도 정보가 포함되어 있습니다.

# how to use nodes(W. documents)
---
아래의 방식으로 node를 활용하기 위하여 documents를 사용할 수 있어야합니다. 아래의 링크를 참고해주세요.
[documents](./documents.html)

documents를 활용하여 간단하게 node를 사용하려면 다음과 같이 사용하면 됩니다.

{% highlight python %}
from llama_index.core.node_parser import SentenceSplitter

parser = SentenceSplitter()

nodes = parser.get_nodes_from_documents(documents)
{% endhighlight %}

# how to use nodes(custom text)
---
아래의 방식으로 각각의 text를 수동으로 node를 만들어 줄 수도 있습니다.(고급)

{% highlight python %}
from llama_index.core.schema import TextNode, NodeRelationship, RelatedNodeInfo

node1 = TextNode(text="<text_chunk>", id_="<node_id>")
node2 = TextNode(text="<text_chunk>", id_="<node_id>")
# set relationships
node1.relationships[NodeRelationship.NEXT] = RelatedNodeInfo(
    node_id=node2.node_id
)
node2.relationships[NodeRelationship.PREVIOUS] = RelatedNodeInfo(
    node_id=node1.node_id
)
nodes = [node1, node2]
{% endhighlight %}

또한 아래와 같이 node간의 종속적 정보를 추가 할 수 있습니다.

{% highlight python %}
node2.relationships[NodeRelationship.PARENT] = RelatedNodeInfo(
    node_id=node1.node_id, metadata={"key": "val"}
)
{% endhighlight %}

노드는 다음의 방식으로 id를 직접 주입할 수 있습니다. 이러한 id 값은 다양한 역활을 할 수 있습니다.

{% highlight python %}
node.node_id = "My new node_id!"
{% endhighlight %}

# Advance
---
[nodes advance(1)](./nodes advance(1).html)