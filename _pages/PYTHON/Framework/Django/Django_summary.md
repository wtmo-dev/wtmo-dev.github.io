---
title: "Django init summary"
tags:
    - python
    - framework
    - Django
date: "2023-08-25"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---
# **Django**
---
* django-debug-toolbar -> 디버그 내용 확인 용이
  * INSTALLED_APPS "debug_toolbar"
  * MIDDLEWARE "debug_toolbar.middleware.DebugToolbarMiddleware"
  * INTERNAL_IPS "IP"
* djangorestframework -> restAPI 제작에 용이
* django-ninja -> 
1. djangorestframework의 느린 serializer 대신 pydantic 사용
2. swagger 지원 POSTMAN 같은것
3. Async 지원
4. api version 지원
* django-seed -> db에 임시 데이터 뿌려줌
  * INSTALLED_APPS "django_seed"
  * cmd: python manage.py seed \<app_name\> \-\-number=\<num\>

## **서버 기본 세팅**
---
{% highlight shell %}
# 프로젝트 생성 구문
django-admin startproject <project_name>
# 프로젝프 앱 생성 구문
cd <project_name>
python <project_name>/manage.py startapp <app_name>
# 프로젝프 슈퍼 유저 생성
python <project_name>/manage.py createsuperuser
# 프로젝프 기본 마이그레이션
python <project_name>/manage.py migrate
# 프로젝프 추가 제작한 마이그레이션
# (오류발생시 setting.py -> INSTALLED_APPS에 <app_name>추가)
python <project_name>/manage.py makemigrations
# 서버 구동 구문
python <project_name>\manage.py runserver
{% endhighlight %}

## **유저 테이블 제작(models)**
---
커스텀 유저 테이블을 제작하는데 있어서 직접 제작이 가능하며 아래의 방법들이 있다.

* 추상화 유저 제작

{% highlight python %}
from django.contrib.auth.models import AbstractUser

class Users(AbstractUser):
    pay_plan = models.ForeignKey(PayPlan, on_delete=models.DO_NOTHING)
{% endhighlight %}

<span style="color:red">setting.py에 AUTH_USER_MODEL = '\<app_name\>.Users' 추가해야함</span>
<br/>
* 장고 모듈 활용 유저 제작

{% highlight python %}
from django.contrib.auth.models import User as U

# class UserDetail(models.Model):
#     user = models.OneToOneField(U, on_delete=models.CASCADE)
#     pay_plan = models.ForeignKey(PayPlan, on_delete=models.DO_NOTHING)
{% endhighlight %}

<span style="color:red">두개를 모두 사용할 경우 oneToOneField의 입력이 추상화의 Users를 가르켜야한다.</span>  

## **view_html**
---

urls.py  
url 패턴을 이용하여 입력받는 주소로 부터 사용할 view단과 연결을 해준다.

{% highlight python %}
from app_test.views import index, redirect_test

urlpatterns = [
    path('', index , name='index'),
    path('redirect', redirect_test),
]
{% endhighlight %}

view.py  
urls.py에 연결된 view단을 세팅하는 부분  
base.html과 같은경우는 \<app_name\>/templates 폴더에 둔다.

{% highlight python %}
# 모델(DB)에서 참조할시 해당 모델 추가사항
from .models import Users

# 모델에서 유저정보를 받아서 보여지는 결과를 다르게 한 예시
def index(request):
    user = Users.objects.filter(username="admin").first()
    email = user.email if user else "Nooooo"
    print(email)
    print(request.user.is_authenticated)
    if not request.user.is_authenticated:
        email = "NOoooooooooooooo"
    print(email)
    return render(request, "base.html", {"welcome_msg": f"Hello {email}"})

# 재참조 형식의 view단 예시
def redirect_test(request):
    return redirect("index")
{% endhighlight %}

## **view_restAPI**
---

urls.py  
url 패턴을 이용하여 입력받는 주소로 부터 사용할 view단과 연결을 해준다.
<span style="color:purple">\<int:user_id\>는 query string 사용법</span>

{% highlight python %}
urlpatterns = [
    path('get_user/<int:user_id>', get_user),
]
{% endhighlight %}

view.py  
urls.py에 연결된 view단을 세팅하는 부분  
<span style="color:purple">csrf_exempt는 token 인증을 임시로 풀기위한것</span>  
<span style="color:purple">body가 아닌 JsonResponse는 보통 개발자들끼리 내용을 주고 받을때 사용하기도 한다.</span>

{% highlight python %}
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt

@csrf_exempt
def get_user(request, user_id):
    print(user_id)
    if request.method == "GET":
        abc = request.GET.get("abc")
        xyz = request.GET.get("xyz")
        user = Users.objects.filter(pk=user_id).first()
        return render (request, "base.html", {"user": user,  "params": [abc, xyz]})
    elif request.method == "POST":
        username = request.GET.get("username")
        if username:
            user = Users.objects.filter(pk=user_id).update(username=username)
        return JsonResponse(status=201, data=dict(msg="POST is"))
{% endhighlight %}

## **admin_handling1**
---
admin.py  
admin page에서 model을 핸들링 가능하게 해준다.

{% highlight python %}
from .models import PayPlan

# Register your models here.
admin.site.register(PayPlan)
{% endhighlight %}

## **django original login setting**
---
urls.py 세팅

* views.py
{% highlight python %}
from django.contrib.auth import authenticate, login
from .forms import RegisterForm

def register(request):
    if request.method == "POST":
        form = RegisterForm(request.POST)
        msg = "not valid data"
        if form.is_valid():
            form.save() # db에 저장(commit=False로 임시저장가능)
            username = form.cleaned_data.get("username")
            raw_password = form.cleaned_data.get("password1")
            user = authenticate(username= username, password= raw_password) # 인증
            login(request, user) # 로그인
            msg = "login"
        return render(request, "register.html", {"form": form, "msg": msg})
    else:
        form = RegisterForm()
    return render(request, "register.html", {"form": form})
{% endhighlight %}

* forms.py
{% highlight python %}
from django import forms
from django.contrib.auth.forms import UserCreationForm
from .models import Users

class RegisterForm(UserCreationForm):
    username = forms.CharField(max_length=20, required=True, help_text="name", label="이름")
    email = forms.EmailField(max_length=20, required=False, help_text="email", label="이메일")
    
    class Meta:
        model = Users
        fields = (
            "username",
            "email",
            "password1",
            "password2",
        )
{% endhighlight %}

## **paginator**
---
views.py  
페이지 분할 제작법

{% highlight python %}
from django.core.paginator import Paginator

def a(request):
    page = int(request.GET.get("page", 1))
    <data> = <>.objects.all().order_by("-id") # 정렬해야 "-"내림차순
    paginator = Paginator(<data>, 5)
    <datas> = paginator.get_page(page)

    return render(request, ".html", {"args": <datas>})
{% endhighlight %}

## **login_required**
---
setting.py  
LOGIN_URL ="/\<\>"  

views.py  
로그인 필수 페이지 세팅

{% highlight python %}
from django.contrib.auth.decorators import login_required

@login_required
def a(request):
{% endhighlight %}

## **template tags**
---
탬플렛을 제작하는데 있어서 조건이나 데이터 활용등을 위한 태그

* {\% csrf_token \%}  
    * csrf token을 필요로 하다는것을 나타낼때 사용
* {\% cycle "a" "b" \%}  
    * iter적인 상황에서 각 순서마다 서로 다른 영향을 주려고 할때 사용
* {\% extends "<filename>.html" \%}  
    * 한 html에서 다른 html을 확장하여 사용할때 사용  
    * 자식페이지에 최상단에 필요하며 <filename>은 부모파일이다.
* {\% block <name> \%} {\% endblock \%}  
    * 한 html에서 다른 html을 확장하여 사용할때 사용  
    * 부모페이지에서 자식을 넣을공간에, 자식페이지에서 넣을 내용을 감싼다.
* {\% if \%}{\% elsif \%}{\% else \%}{\% endif \%}
    * 조건문을 사용할때 사용
* {\% for i in items \%}{\% endfor \%}
    * for문을 사용할때 사용
        * forloop.counter 루프의 인덱스(1시작)
        * forloop.counter0 루프의 인덱스(0시작)
        * forloop.first 루프의 첫번째 True
        * forloop.last 루프의 마지막 True
* {\% includes "\<filename\>.html" \%}
    * html에서 html 파일을 사용할때 사용할 \<filename\>을 작성
    * extends보다 느리다.(랜더링이 느리다.)
* {\% url "\<namespace\>" \%}
    * \<namespace\>로 이동하게 할때 사용
* {\% static "\<filepath\>" \%}
    * \<filepath\>에 있는 static 파일 사용
        * \<app_name\>/static/\<filepath\>으로 구성
        * {\% load static \%}을 최상단에 작성해야함

## **custom tags**
---
탬플렛을 제작하는데 있어서 

* \<app_name\>/templatetags/custom_tags.py
{% highlight python %}
from django import template
from django.utils.html import mark_safe

register = template.Library()

@register.simple_tag(name=<tag_name>, takes_context=True)
def tags_test(context): # context에는 해당 페이지 정보가 있으며 상세히 다룰 수 있다.
    tag_html = "<span class='badge text-bg-primary'>태그</span>"

    # mark_safe는 html로 사용해도 안전함을 알려줌 사용안하면 string으로 사용
    return mark_safe(tag_html)
{% endhighlight %}

* {\% load custom_tags \%}  
태그 사용할 html 최상단에 적용  
* {\{data|\<tag_name\>}\}  
태그 사용할 html 코드에 사용

## **custom filter**
---
탬플렛을 제작하는데 있어서 원하는 내용만 보여주기 위하여 사용

* \<app_name\>/templatetags/custom_filters.py
{% highlight python %}
from django import template

register = template.Library()

@register.filter(name=<filter_name>)
def email_masker(value):
    email_split = value.split("@")
    return f"{email_split[0]}@******.***"
{% endhighlight %}

* {\% load custom_filters \%}  
필터 사용할 html 최상단에 적용  
* {\{data|\<filter_name\>}\}  
필터 사용할 html 코드에 사용
