---
title: "FastAPI intro Num.1"
tags:
    - python
    - framework
    - FastAPI
date: "2024-02-01"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# What is FastAPI
---
FastAPI는 python으로 구현된 web framework입니다. FastAPI는 빠르게 개발이 가능하고 python으로 구현된 web framework중 가장 빠르다고 이야기 되고 있습니다.
type check를 해주는 [pydantic](https://docs.pydantic.dev/latest/)과 Asynchronous Server Gateway interface로 구현된 [starlette](https://www.starlette.io/)가 구성되어 있습니다. 그에 따라 다음과 같은 장점을 가지게 됩니다.
* type check
* 비동기적 작업 지원

## fast to create docs
---
FastAPI는 docs를 자체적으로 지원을 해줘서 빠른 문서작업이 가능해집니다.

* FastAPI는 [Swagger UI](https://github.com/swagger-api/swagger-ui)를 기반으로한 API docs를 지원해줍니다. 해당 자료는 FastAPI를 구동하면 ```https://localhost:port/docs```에서 확인을 할 수 있습니다.
* FastAPI는 [ReDoc](https://github.com/Redocly/redoc)을 기반으로한 API docs 또한 지원을 해줍니다. 해당 자료는 FastAPI 구동이후 ```https://localhost:port/redoc```에서 확인을 할 수 있습니다.

# How to start FastAPI
---
FastAPI를 사용하기 위하여 우선 두가지 모듈을 다운 받아야합니다.

{% highlight shell %}
pip install fastapi
pip install uvicorn
{% endhighlight %}

이후 실행을 위하여 아래의 코드 작성 및 실행이 필요합니다.

* main.py
{% highlight python %}
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def root():
    return {"message": "Hello World"}
{% endhighlight %}

* you should run in cli
{% highlight shell %}
uvicorn main:app --reload
{% endhighlight %}
main:app은 main.py에 있는 app을 실행한다는 의미입니다.

# Input Datas
---
API의 데이터 입출력을 위하여 다양한 방식의 input data가 존재합니다. 아래는 해당 값들을 순차적으로 설명드리겠습니다.

## Path Parameters
---
경로 파라미터라고 불리는 것으로 아래의 코드에서 ```item_id```를 의미합니다. FastAPI는 type에 있어서 매우 엄격합니다. 그래서 아래의 코드와 같이 type hint(or pydantic)가 없거나 일치 하지 않을 경우 작동하지 않습니다. 주소창에 입력하는 값으로보면 숫자를 입력해도 문자로 보일 수 있으나 type hint에 따라서 숫자로 인식됩니다.

{% highlight python %}
@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id}
{% endhighlight %}

위와 같은 주소체계를 사용할때 주의 할점은 ```"/items/item"```이라고 만약 새로운 주소체계를 선언할 경우 path parameter로 구성된 주소체계보다 상단에 존재하여야합니다. 이는 중복된 입력으로 판단이 될 수 있기 때문입니다.

Path Parameter가 ```"/"```와 같이 경로 데이터가 포함이 되어있을 경우 starlette에서 지원해주는 type check 기능으로 ```:path```를 추가해 아래와 같이 활용 가능합니다.

{% highlight python %}
@app.get("/items/{item_id:path}")
async def read_item(item_id: str):
    return {"item_id": item_id}
{% endhighlight %}

Path Parameter는 아래와 같이 상세한 유효성 검사를 지원하며 사용법은 다음과 같습니다.
* gt: 보다 크다.
* ge: 크거나 같다.
* lt: 보다 작다.
* le: 작거나 같다.

{% highlight python %}
from typing import Annotated

from fastapi import FastAPI, Path

app = FastAPI()

@app.get("/items/{item_id}")
async def read_items(
    q: str, item_id: Annotated[int, Path(title="The ID of the item to get")]
):
    results = {"item_id": item_id}
    if q:
        results.update({"q": q})
    return results
{% endhighlight %}

## Query Parameters
---
Path Parameter이외에 입력값을 작성하면 Query Parameter로 인식됩니다. url로 값을 직접 전송하려면 ```URL/?data=data```와 같이 전송이 가능합니다.
Query Parameter의 경우 default값을 제공해주지 않거나 [Ellipsis](https://docs.python.org/3/library/constants.html#Ellipsis)를 주면 필수 입력 조건으로 사용이됩니다.

Query Parameter는 다음과 같이 유효성 검사를 추가적으로 진행 할 수 있습니다. 이것이 의미하는 바는 q는 str인데 None일 수 있으며 최대 글자수가 50이 넘으면 안되는 기본값 None을 가진 parameter라고 볼 수 있습니다.

{% highlight python %}
from typing import Annotated

from fastapi import FastAPI, Query

app = FastAPI()

@app.get("/items/")
async def read_items(q: Annotated[str | None, Query(max_length=50)] = None):
    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}
    if q:
        results.update({"q": q})
    return results
{% endhighlight %}

Query에는 다음과 같이 다양한 입력을 줄 수 있습니다.
* alias: 입력 명칭을 변경
* deprecated: 사용 가능 여부
* include_in_schema: 문서에 표현 여부

{% highlight python %}
Query(
    alias="item-query",
    title="Query string",
    description="Query string for the items to search in the database that have a good match",
    min_length=3,
    max_length=50,
    pattern="^fixedquery$",
    deprecated=True,
    include_in_schema=False
),
{% endhighlight %}

## Body
---
다중 입력값이 존재할경우 흔하게 사용되는 방식입니다. fastapi에서 지원하는 Request를 사용해도 가능하지만 pydantic을 이용하는것이 무결성에 있어서 안전합니다.

{% highlight python %}
from fastapi import FastAPI
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    tax: float | None = None

app = FastAPI()

@app.post("/items/")
async def create_item(item: Item):
    return item
{% endhighlight %}

### Single Body
---
Body를 사용하는데 있어서 단일값일 경우 아래와 같이 사용이 가능합니다.

{% highlight python %}
from typing import Annotated
from fastapi import Body, FastAPI

app = FastAPI()

@app.put("/items")
async def update_item(
    importance: Annotated[int, Body()]
):
    return {"importance": importance}
{% endhighlight %}

### Body Field
---
body도 query와 같이 Field를 사용하여 추가적인 무결성 검사를 할 수 있습니다.

{% highlight python %}
from typing import Annotated

from fastapi import Body, FastAPI
from pydantic import BaseModel, Field

app = FastAPI()

class Item(BaseModel):
    price: float = Field(gt=0, description="The price must be greater than zero")
    tax: float

@app.put("/items")
async def update_item(item: Annotated[Item, Body(embed=True)]):
    results = {"item_id": item_id, "item": item}
    return results
{% endhighlight %}

## Cookie
---
Cookie 데이터가 있을경우 아래와 같이 사용할 수 있습니다.

{% highlight python %}
from typing import Annotated, Union

from fastapi import Cookie, FastAPI

app = FastAPI()

@app.get("/items/")
async def read_items(ads_id: Annotated[Union[str, None], Cookie()] = None):
    return {"ads_id": ads_id}
{% endhighlight %}

## Header
---
Header 데이터를 사용할 수 있습니다. Header의 경우 ```"-"```이 ```"_"```으로 자동 치환이 되기때문에 원본을 사용하려면 옵션을 추가해줘야 합니다.

{% highlight python %}
from typing import Annotated, Union

from fastapi import FastAPI, Header

app = FastAPI()

@app.get("/items/")
async def read_items(user_agent: Annotated[Union[str, None], Header(convert_underscores=False)] = None):
    return {"User-Agent": user_agent}
{% endhighlight %}

## Form
---
Form data의 경우 우선 ```pip install python-multipart```를 필요로 합니다. Form data는 아래와 같이 활용이 가능합니다.

{% highlight python %}
from typing import Annotated

from fastapi import FastAPI, Form

app = FastAPI()

@app.post("/login/")
async def login(username: Annotated[str, Form()], password: Annotated[str, Form()]):
    return {"username": username}
{% endhighlight %}

## File
---
File data의 경우 우선 ```pip install python-multipart```를 필요로 합니다. File data는 2가지 방식으로 활용 가능합니다.
* bytes: 이미지의 원본을 binary값으로 가져옵니다.
* UploadFile: 이미지의 관련 정보들을 가져옵니다.
    * filename
    * content_type
    * file
        * read
        * write
        * seek
        * close


{% highlight python %}
from typing import Annotated

from fastapi import FastAPI, File, UploadFile

app = FastAPI()

@app.post("/files/")
async def create_file(file: Annotated[bytes, File()]):
    return {"file_size": len(file)}

@app.post("/uploadfile/")
async def create_upload_file(file: Annotated[UploadFile, File()]):
    return {"filename": file.filename}
{% endhighlight %}

# Next
---
[Next](intro(2).html)
