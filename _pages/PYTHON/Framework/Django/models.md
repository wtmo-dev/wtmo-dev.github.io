---
title: "Django models"
tags:
    - python
    - framework
    - Django
date: "2024-03-22"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# What is model
---
Django에서 model은 DB의 구조를 나타내어집니다.

# How to use model
---
model의 사용법은 다음과 같습니다.

* \<app-name\>.models.py 생성
{% highlight shell %}
from django.contrib.auth.models import User
from django.db import models

class UserDetail(models.Model):
    user = models.ForeignKey(
        User, verbose_name="user 정보", on_delete=models.DO_NOTHING
    )
    user_email = models.IntegerField(verbose_name="user email", null=False, primary_key=True)
    
    class Meta:
        db_table = "userdetail"
        managed = True
        verbose_name = "user 상세 정보"
        verbose_name_plural = "user 상세 정보 목록"
{% endhighlight %}

* \<app-name\>.admin.py 추가(case 1)
{% highlight shell %}
from django.contrib import admin
from .models import Cart

class CartAdmin(admin.ModelAdmin): # admin 페이지에 표기할 column 지정
    list_display = ('<column-name>', '<column-name>')

admin.site.register(Cart, CartAdmin) # admin page에 등록
{% endhighlight %}

* \<app-name\>.admin.py 추가(case 2)
{% highlight shell %}
from django.contrib import admin
from .models import Cart

@admin.register(Cart) # admin page에 등록
class CartAdmin(admin.ModelAdmin): # admin 페이지에 표기할 column 지정
    list_display = ('<column-name>', '<column-name>')
{% endhighlight %}

# Field of model
---
model의 column들을 정의 하는 field는 다음과 같이 사용할 수 있습니다.

## ID Field
---

|Field 타입|설명|
|---|---|
|AutoField|1에서 부터 자동적으로 증가합니다.|
|BigAutoField|1 ~ 9223372036854775807까지 1씩 자동으로 증가하는 필드입니다.|
|UUIDField|UUID 전용 필드입니다.|

## String Field
---

|Field 타입|설명|
|---|---|
|CharField|적은 문자열을 저장하는 필드입니다.|
|TextField|많은 문자열을 저장하는 필드입니다.|
|URLField|URL을 저장하는 필드입니다.|
|EmailField|E-mail을 저장하는 필드입니다.|

## String Field
---

|Field 타입|설명|
|---|---|
|CharField|적은 문자열을 저장하는 필드입니다.|

## Data Field
---

|Field 타입|설명|
|---|---|
|BinaryField|Binary 데이터를 저장하는 필드입니다.|
|DecimalField|Decimal 데이터를 저장하는 필드입니다.|
|IntegerField|Interger 데이터를 저장하는 필드입니다.|
|PositiveIntegerField|양수만 취급하는 Interger 데이터를 저장하는 필드입니다.|
|FloatField|Float 데이터를 저장하는 필드입니다.|
|BooleanField|참/거짓 데이터를 저장하는 필드입니다.|
|NullBooleanField|Null값이 가능한 참/거짓을 저장하는 필드입니다.|

## Time Field
---

|Field 타입|설명|
|---|---|
|DateField|날짜 데이터를 저장하는 필드입니다.|
|TimeField|시간 데이터를 저장하는 필드입니다.|
|DateTimeField|날짜와 시간 데이터 모두 저장할 수 있는 필드입니다.|

## File Field
---

|Field 타입|설명|
|---|---|
|ImageField|이미지 데이터를 저장하는 필드입니다.|
|FileField|파일 업로드 데이터를 저장하는 필드입니다.|
|FilePathField|파일 경로 데이터를 저장하는 필드입니다.|

## Relation Field
---

|Field 타입|설명|
|---|---|
|OneToOneField|일대일 관계를 저장하는 필드입니다.|
|ForeignKey|일대다 관계를 저장하는 필드입니다.|
|ManyToManyField|다대다 관계를 저장하는 필드입니다.|

더 많은 정보는 다음에 포함되어 있습니다.
[relations](relations.html)

## Field Option
---
Field의 옵션은 다음과 같으며 모든 Field가 모든 옵션을 사용할 수는 없습니다.

|Field 옵션|설명|기본값|
|---|---|---|
|default|필드의 기본값을 설정합니다.|-|
|help_text|도움말 텍스트를 설정합니다.|-|
|null|Null 값 허용 유/무를 설정합니다.|False|
|blank|비어있는 값 허용 유/무를 설정합니다.|False|
|unique|고유 키 유/무를 설정합니다.|False|
|primary_key|기본 키 유/무를 설정합니다. (null=False, unique=True와 동일)|False|
|editable|필드 수정 유/무를 설정합니다.|False|
|max_length|필드의 최대 길이를 설정합니다.|-|
|auto_now|개체가 저장될 때마다 값을 설정합니다.|False|
|auto_now_add|개체가 처음 저장될 때 값을 설정합니다.|False|
|on_delete|개체가 제거될 때의 동작을 설정합니다.|-|
|db_column|데이터베이스의 컬럼의 이름을 설정합니다.|-|

## Meta Option
---
Meta 옵션은 다음과 같습니다.

|Meta 옵션|설명|기본값|
|abstract|추상 클래스 유/무를 설정합니다.|False|
|db_table|모델에 사용할 데이터베이스 테이블의 이름을 설정합니다.|-|
|managed|데이터베이스의 생성, 수정, 삭제 등의 권한을 설정합니다.|True|
|ordering|객체를 가져올 때의 정렬 순서를 설정합니다.|-|
|verbose_name|사람이 읽기 쉬운 객체의 이름을 설정합니다. (단수형으로 작성)|-|
|verbose_name_plural|사람이 읽기 쉬운 객체의 이름을 설정합니다. (복수형으로 작성)|-|

# model manager
---
model은 기본적으로 objects를 manager로 가지게 되어있습니다. 하지만 아래와 같이 override할 수 있습니다.

{% highlight shell %}
class DeletedManager(models.Manager):
    use_for_related_fields = True # default manager로 사용시 관계에서 모두 활용 가능

    def deleted(self, **kwargs):
        return self.filter(is_deleted=False, **kwargs)

    def get_queryset(self):
        return super().get_queryset().filter(is_deleted=False)
{% endhighlight %}

{% highlight shell %}
class Post(models.Model):
    objects = DeletedManager()

{% endhighlight %}

# structure of model
---
구조는 위에 나열한 Field를 추가하여 주면 되며, Meta를 사용한 abstract기능을 True로 해주면 상속을 할 수 있는 상태가 됩니다. 아래는 default로 있는 User정보의 abstract를 활용한 예시입니다. Mixedin은 2개이상의 상속을 받을때 사용하며, abstract와 같으나 명칭만 다릅니다.

{% highlight python %}
class User(AbstractBaseUser, PermissionsMixin):
    objects = UserManager()

    USERNAME_FIELD = 'email'
    REQUIRED_FIELDS = ['nickname', ]

    class Meta:
        ordering = ('-date_joined',)

    def __str__(self): # object 호출시 지정할 명칭
        return self.nickname

{% endhighlight %}

# migration
---
migration은 DB와 코드간의 상태를 확인하는 작업입니다. 아래의 코드는 migration을 하는데 있어 주로 사용되는 코드입니다.

{% highlight shell %}
python manage.py showmigrations # migration의 상태확인
python manage.py makemigrations # migration 생성
python manage.py migrate # migration 적용
python manage.py --fake <app-name> zero # <app-name>의 migration 초기화
python manage.py --fake-initial # fake migration 생성
{% endhighlight %}
