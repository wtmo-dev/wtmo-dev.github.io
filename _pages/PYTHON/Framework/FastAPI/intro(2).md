---
title: "FastAPI intro Num.2"
tags:
    - python
    - framework
    - FastAPI
date: "2024-02-02"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# Error handling
---
API를 만드는데 있어서 Error 상황이 있을 수 있습니다. 이런경우 error 상태를 요청자에게 안내와 함께 시스템의 결과 관리를 해줘야 합니다.

## HTTPException
---
가장 일반적인 exception으로 아래와 같이 사용 가능합니다. 일반적으로 headers를 작성할 필요가 없으나 Token을 만들거나 하는 상황이나 보안적인 문제가 있을때 사용하기에 좋습니다.

{% highlight python %}
from fastapi import FastAPI, HTTPException

app = FastAPI()

items = {"foo": "The Foo Wrestlers"}

@app.get("/items/{item_id}")
async def read_item(item_id: str):
    if item_id not in items:
        raise HTTPException(
            status_code=404,
            detail="Item not found",
            headers={"X-Error": "There goes my error"},
        )
    return {"item": items[item_id]}
{% endhighlight %}

## Custom Exception
---
Exception은 다음과 같이 custom해서 사용 가능합니다.

{% highlight python %}
from fastapi import FastAPI, Request
from fastapi.responses import JSONResponse

class UnicornException(Exception):
    def __init__(self, name: str):
        self.name = name

app = FastAPI()

@app.exception_handler(UnicornException)
async def unicorn_exception_handler(request: Request, exc: UnicornException):
    return JSONResponse(
        status_code=418,
        content={"message": f"Oops! {exc.name} did something. There goes a rainbow..."},
    )

@app.get("/unicorns/{name}")
async def read_unicorn(name: str):
    if name == "yolo":
        raise UnicornException(name=name)
    return {"unicorn_name": name}
{% endhighlight %}

다음 보여드릴 방식은 기본 설정된 starlette, RequestValidation을 custom해서 추가 기능을 구현하려고 할때 활용 가능합니다.

{% highlight python %}
from fastapi import FastAPI
from fastapi.exception_handlers import (
    http_exception_handler,
    request_validation_exception_handler,
)
from fastapi.exceptions import RequestValidationError
from starlette.exceptions import HTTPException as StarletteHTTPException

app = FastAPI()

@app.exception_handler(StarletteHTTPException)
async def custom_http_exception_handler(request, exc):
    print(f"OMG! An HTTP error!: {repr(exc)}")
    return await http_exception_handler(request, exc)

@app.exception_handler(RequestValidationError)
async def validation_exception_handler(request, exc):
    print(f"OMG! The client sent invalid data!: {exc}")
    return await request_validation_exception_handler(request, exc)
{% endhighlight %}

# Routing
---
routing을 하는 방식은 크게 2가지를 볼 수 있습니다.

* use tags
{% highlight python %}
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/", tags=["items"])
async def create_item():
    return None
{% endhighlight %}

* use router
{% highlight python %}
from fastapi import FastAPI, APIRouter

app = FastAPI()

router = APIRouter(prefix='/slack', tags=["items"])
app.include_router(user.router)

@router.get("/items/")
async def create_item():
    return None
{% endhighlight %}

# JsonEncoder
---
pydantic으로 인하여 dict형이 아니거나 2개이상의 dict형을 융합하여 활용하고 싶을때 사용할 수 있는 방법입니다.

{% highlight python %}
from fastapi.encoders import jsonable_encoder
from pydantic import BaseModel

class Item(BaseModel):
    title: str
    timestamp: datetime
    description: str | None = None

@app.put("/items/{id}")
def update_item(id: str, item: Item):
    jsonable_encoder(item)
{% endhighlight %}

# Dependencies
---
Dependencies는 FastAPI가 동작하는데 있어서 종속성을 주입하는 것입니다. 이는 더욱 안정적으로 동작할 수 있게 해줍니다. pydantic으로 사용하는것을 권장하나 아래와 같이 사용할 수 도 있습니다.

# Function Dependencies
---
다음과 같이 함수형으로도 만들 수 있습니다.

{% highlight python %}
from typing import Annotated

from fastapi import Depends, FastAPI

app = FastAPI()

async def common_parameters(
    skip: int = 0, limit: int = 100
):
    return {"skip": skip, "limit": limit}

@app.get("/items/")
async def read_items(commons: Annotated[dict, Depends(common_parameters)]):
    return commons
{% endhighlight %}

## Class Dependencies
---
다음과 같이 클래스형으로 만들 수 있습니다.

{% highlight python %}
from typing import Annotated, Union

from fastapi import Depends, FastAPI

app = FastAPI()

class CommonQueryParams:
    def __init__(self, skip: int = 0, limit: int = 100):
        self.skip = skip
        self.limit = limit
        
@app.get("/items/")
async def read_items(commons: Annotated[CommonQueryParams, Depends(CommonQueryParams)]):
    return commons
{% endhighlight %}

## Path Operation Dependencies
---
다음과 같이 함수의 입력이 아니라 path operation dependency에 입력하여 값을 검증 할 수도 있습니다.

{% highlight python %}
from typing import Annotated

from fastapi import Depends, FastAPI, Header, HTTPException

app = FastAPI()

async def verify_token(x_token: Annotated[str, Header()]):
    if x_token != "fake-super-secret-token":
        raise HTTPException(status_code=400, detail="X-Token header invalid")

@app.get("/items/", dependencies=[Depends(verify_token)])
async def read_items():
    return None
{% endhighlight %}

## Global Dependencies
---
전역 Dependency도 사용할 수 있습니다. 이는 token 검증과 같은 활동에 있어서 유용합니다.

{% highlight python %}
app = FastAPI(dependencies=[Depends(verify_token), Depends(verify_key)])
{% endhighlight %}

## Dependencies using yield
---
Dependency를 사용하여 DB의 무결성도 확인이 가능합니다. 아래의 예시는 sqlalchemy를 사용하였으나 다음과 같이 구성하면 활용성을 향상시킬 수 있습니다.

{% highlight python %}
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

engine = create_engine(
    <database_url>,
    pool_pre_ping=True
)
Session = sessionmaker(autocommit=False, autoflush=False, bind=engine)

def get_db():
    db = Session()
    try:
        yield db
    finally:
        db.close()

def router(s: Annotated[Service, Depends(get_db)]):
    s.action()
{% endhighlight %}

{% highlight python %}
class MySuperContextManager:
    def __init__(self):
        self.db = DBSession()

    def __enter__(self):
        return self.db

    def __exit__(self, exc_type, exc_value, traceback):
        self.db.close()


async def get_db():
    with MySuperContextManager() as db:
        yield db
{% endhighlight %}

아래의 로직을 이해한다면 fastapi를 자유롭게 사용하는데 문제가 없다고 볼 수 있습니다.

![fastapi logic](/assets/img/python/framework/fastapi/fastapi.PNG){: width="100%"}

# Prev
---
[Prev](intro(1).html)

# Next
---
[Next](intro(3).html)