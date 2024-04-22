---
title: "FastAPI intro Num.3"
tags:
    - python
    - framework
    - FastAPI
date: "2024-02-05"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# Security
---
API를 만드는데 있어서 보안사항은 매우 중요합니다. 아래의 순서를 따라 보안을 설정할 수 있습니다.

{% highlight shell %}
pip install python-jose # jwt token module
pip install passlib[bcrypt] # password hashing module
{% endhighlight %}

만약 ```(trapped) error reading bcrypt version```과 같은 문제가 발생하면 아래의 코드를 작동시켜야 합니다.

{% highlight shell %}
pip install bcrypt==4.0.1
{% endhighlight %}

아래의 방법은 보안을 설정하는 방법들을 제안합니다.

{% highlight python %}
from datetime import datetime, timedelta, timezone
from typing import Annotated, Union

from fastapi import Depends, FastAPI, HTTPException, status
from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm
from jose import JWTError, jwt
from passlib.context import CryptContext
from pydantic import BaseModel

# to get a string like this run:
# openssl rand -hex 32
SECRET_KEY = "09d25e094faa6ca2556c818166b7a9563b93f7099f6f0f4caa6cf63b88e8d3e7"
ALGORITHM = "HS256"
ACCESS_TOKEN_EXPIRE_MINUTES = 30

fake_users_db = {
    "johndoe": {
        "username": "johndoe",
        "full_name": "John Doe",
        "email": "johndoe@example.com",
        "hashed_password": "$2b$12$EixZaYVK1fsbw1ZfbX3OXePaWxn96p36WQoeG6Lruj3vjPGga31lW",
        "disabled": False,
    }
}

class Token(BaseModel):
    access_token: str
    token_type: str

class TokenData(BaseModel):
    username: Union[str, None] = None

class User(BaseModel):
    username: str
    email: Union[str, None] = None
    full_name: Union[str, None] = None
    disabled: Union[bool, None] = None

class UserInDB(User):
    hashed_password: str

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

app = FastAPI()

def verify_password(plain_password, hashed_password):
    return pwd_context.verify(plain_password, hashed_password)

def get_password_hash(password):
    return pwd_context.hash(password)

def get_user(db, username: str):
    if username in db:
        user_dict = db[username]
        return UserInDB(**user_dict)

def authenticate_user(fake_db, username: str, password: str):
    user = get_user(fake_db, username)
    if not user:
        return False
    if not verify_password(password, user.hashed_password):
        return False
    return user

def create_access_token(data: dict, expires_delta: Union[timedelta, None] = None):
    to_encode = data.copy()
    if expires_delta:
        expire = datetime.now(timezone.utc) + expires_delta
    else:
        expire = datetime.now(timezone.utc) + timedelta(minutes=15)
    to_encode.update({"exp": expire})
    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
    return encoded_jwt

async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):
    credentials_exception = HTTPException(
        status_code=status.HTTP_401_UNAUTHORIZED,
        detail="Could not validate credentials",
        headers={"WWW-Authenticate": "Bearer"},
    )
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        username: str = payload.get("sub")
        if username is None:
            raise credentials_exception
        token_data = TokenData(username=username)
    except JWTError:
        raise credentials_exception
    user = get_user(fake_users_db, username=token_data.username)
    if user is None:
        raise credentials_exception
    return user

async def get_current_active_user(
    current_user: Annotated[User, Depends(get_current_user)],
):
    if current_user.disabled:
        raise HTTPException(status_code=400, detail="Inactive user")
    return current_user

@app.post("/token")
async def login_for_access_token(
    form_data: Annotated[OAuth2PasswordRequestForm, Depends()],
) -> Token:
    user = authenticate_user(fake_users_db, form_data.username, form_data.password)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Incorrect username or password",
            headers={"WWW-Authenticate": "Bearer"},
        )
    access_token_expires = timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)
    access_token = create_access_token(
        data={"sub": user.username}, expires_delta=access_token_expires
    )
    return Token(access_token=access_token, token_type="bearer")

@app.get("/users/me/", response_model=User)
async def read_users_me(
    current_user: Annotated[User, Depends(get_current_active_user)],
):
    return current_user

@app.get("/users/me/items/")
async def read_own_items(
    current_user: Annotated[User, Depends(get_current_active_user)],
):
    return [{"item_id": "Foo", "owner": current_user.username}]
{% endhighlight %}

# Middleware
---
미들웨어는 다양한 작동에 있어서 중간에 행동을 하는 행동입니다. 현재 fastapi는 http protocol이 진행되는 시점의 middleware만 사용이 가능합니다. 사용방법은 다음 두가지 방법을 활용할 수 있습니다.

{% highlight python %}
class CustomMiddleware(BaseHTTPMiddleware):

    def __init__(self, app):
        super().__init__(app)

    async def dispatch(self, request, call_next):
        response = await call_next(request)
        return response
    
app.add_middleware(CustomMiddleware)
{% endhighlight %}

{% highlight python %}
@app.middleware("http")
async def add_process_time_header(request: Request, call_next):
    start_time = time.time()
    response = await call_next(request)
    process_time = time.time() - start_time
    response.headers["X-Process-Time"] = str(process_time)
    return response
{% endhighlight %}

[advance middleware](https://fastapi.tiangolo.com/advanced/middleware/)

# CORS
---
CORS는 Cross-Origin-Resource-sharing의 약자로 API를 호출하는 사용자의 ip를 관리하는 방법입니다.

{% highlight python %}
from fastapi.middleware.cors import CORSMiddleware
origins = [
    "http://localhost",
    "http://localhost:8080",
]

app.add_middleware(
    CORSMiddleware,
    allow_origins=origins,
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
{% endhighlight %}

# Background Task
---
main logic이 진행되는 것과 별개로 Background Task를 동작시킬 수 있습니다. 이렇게 동작되면 main logic에 영향을 주지 않는 동작을 빠르게 실행 할 수 있습니다.

{% highlight python %}
from fastapi import BackgroundTasks, FastAPI

app = FastAPI()

def write_log(message: str):
    with open("log.txt", mode="a") as log:
        log.write(message)

@app.post("/send-notification/{email}")
async def send_notification(
    email: str, background_tasks: BackgroundTasks
):
    message = f"message to {email}\n"
    background_tasks.add_task(write_log, message)
    return {"message": "Message sent"}
{% endhighlight %}

# Info
---
fastapi는 기본적인 info를 지정 할 수 있습니다. 이는 docs를 통하여 보여지며 아래와 같이 작성이 가능합니다.

{% highlight python %}
app = FastAPI(
    title="ChimichangApp",
    description=description,
    summary="Deadpool's favorite app. Nuff said.",
    version="0.0.1",
    terms_of_service="http://example.com/terms/",
    contact={
        "name": "Deadpoolio the Amazing",
        "url": "http://x-force.example.com/contact/",
        "email": "dp@x-force.example.com",
    },
    license_info={
        "name": "Apache 2.0",
        "identifier": "MIT",
    },
)
{% endhighlight %}

# static files
---
fastapi로 static file을 사용할 수 있습니다. 이러한 기능을 통하여 간단한 소개글이나 홈페이지 같은것도 제작이 가능해집니다.

{% highlight python %}
from fastapi import FastAPI
from fastapi.staticfiles import StaticFiles

app = FastAPI()

app.mount("/static", StaticFiles(directory="static"), name="static")
{% endhighlight %}

# API Test
---
fastapi를 작성하고나면 정상적으로 작성이 되었는지 걱정이 될 수 있습니다. 이럴때 test를 해볼 수 있는 기능을 지원합니다. 아래와 같이 작성 후 ```pytest```를 통하여 확인을 해볼 수 있습니다.

* test_*.py
{% highlight python %}
from fastapi import FastAPI
from fastapi.testclient import TestClient

app = FastAPI()

@app.get("/")
async def read_main():
    return {"msg": "Hello World"}

client = TestClient(app)

def test_read_main():
    response = client.get("/")
    assert response.status_code == 200
    assert response.json() == {"msg": "Hello World"}
{% endhighlight %}

# run uvicorn(W. code)
---
다음과 같이 코드상에서 uvicorn을 작동하면 코드를 관리하는데 더욱 장점을 가질 수 있습니다.

{% highlight python %}
import uvicorn
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def root():
    return {"value": "hello world"}

if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
{% endhighlight %}

# Prev
---
[Prev](intro(2).html)