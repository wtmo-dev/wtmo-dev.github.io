---
title: "FastAPI types"
tags:
    - python
    - framework
    - FastAPI
date: "2024-02-06"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# Enum
---
Enum 클래스는 다음과 같이 사용할 수 있습니다.

{% highlight python %}
from enum import Enum

class ModelName(str, Enum):
    alexnet = "alexnet"
    resnet = "resnet"
    lenet = "lenet"
{% endhighlight %}

값을 사용하는 방식은 다음과 같이 사용 가능합니다.
* model.value
* Model.\<key\>

{% highlight python %}
app = FastAPI()

@app.get("/models/{model_name}")
async def get_model(model_name: ModelName):
    if model_name is ModelName.alexnet:
{% endhighlight %}

# Optional
---
Optional type의 경우 None일 수 있는 데이터를 의미하며 다음과 같이 작성할 수 있습니다.

{% highlight python %}
from typing import Optional

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id: Optional[int]):
    return {"item_id": item_id}
{% endhighlight %}

# httpUrl
---
httpUrl type의 경우 url형식을 받을 수 있는 형식입니다.

{% highlight python %}
from fastapi import FastAPI
from pydantic import BaseModel, HttpUrl

app = FastAPI()

class Image(BaseModel):
    url: HttpUrl
    name: str

@app.put("/items")
async def update_item(image: Image):
    results = {"image": image}
    return results
{% endhighlight %}

# output type
---
output type의 경우 일반적인 방식으로 활용이 가능합니다. 
* ```response_model=None```은 2종류 이상의 타입이 가능할경우 pydantic의 규제를 피할때 사용할 수 있습니다.
* ```response_model_exclude_unset=True```은 output을 넘겨줄때 pydantic의 default value는 무시하는 방법입니다.
* ```response_model_exclude={""}```은 output을 넘겨줄때 넘겨주지 않을 value를 지정하는 방법입니다.

{% highlight python %}
from fastapi import FastAPI, Response
from fastapi.responses import RedirectResponse

app = FastAPI()

@app.get("/portal", response_model=None, response_model_exclude_unset=True, response_model_exclude={"tax"})
async def get_portal(teleport: bool = False) -> Response | dict:
    if teleport:
        return RedirectResponse(url="https://www.youtube.com/watch?v=dQw4w9WgXcQ")
    return {"message": "Here's your interdimensional portal."}
{% endhighlight %}

# and others
---
이외에도 다양한 data type이 존재하며 다음과 같습니다.

* datetime.datetime
* datetime.date
* datetime.time
* datetime.timedelta
* frozenset
* bytes
* Decimal

# schema examples
---
pydantic으로 형식을 만들때는 다음과 같이 예시문을 만들 수 있습니다. 예시문을 활용하면 docs에서 예시문을 확인할 수 있습니다.

{% highlight python %}
class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    tax: float | None = None

    model_config = {
        "json_schema_extra": {
            "examples": [
                {
                    "name": "Foo",
                    "description": "A very nice Item",
                    "price": 35.4,
                    "tax": 3.2,
                }
            ]
        }
    }
{% endhighlight %}

pydantic이 아닐경우는 Body, Query, ...에서 직접 예시문을 작성할 수도 있습니다.

{% highlight python %}
Body(
    examples=[
        {
            "name": "Foo",
            "description": "A very nice Item",
            "price": 35.4,
            "tax": 3.2,
        }
    ],
),
{% endhighlight %}

