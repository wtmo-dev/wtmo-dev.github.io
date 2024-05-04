---
title: "Django advance"
tags:
    - python
    - framework
    - Django
date: "2024-03-27"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# Advance
---

* HttpRequest
HttpRequest.headers # request의 headers 객체
HttpRequest.body  	# request의 body 객체
HttpRequest.COOKIES # 모든 쿠키를 담고 있는 딕셔너리 객체
HttpRequest.method 	# reqeust의 메소드 타입
HttpRequest.FILES	# <input type='file'> 로 보낸 UploadFile!
HttpRequest.META	# HTTP 헤더가 포함하는 모든 접근 가능한 정보를 담고 있는 dict, 메타 정보는 (당연히) web-server에 영향을 받는다.
HttpRequest.GET 	# GET 파라미터를 담고 있는 QueryDict instance
HTTpRequest.POST 	# POST 파라미터를 담고 있는 QueryDict instance

[queryDict instance](https://engineer-mole.tistory.com/121)

# Query Expression
---

## F function
---
python에서 핸들링 하는것이 아닌 Query로 만들어서 database에서 핸들링을 할 수 있는 방법입니다.

{% highlight python %}
User.objects.all().update(user_id=F('user_id') + 1) # Base

company = Company.objects.annotate(chairs_needed=F('num_employees') - F('num_chairs')) # annotate same field

from django.db.models import DateTimeField, ExpressionWrapper, F

Ticket.objects.annotate(
    expires=ExpressionWrapper(
        F('active_at') + F('duration'), 
        output_field=DateTimeField()
    )
) # annotate different field
{% endhighlight %}

[Docs](https://docs.djangoproject.com/ko/5.0/topics/db/queries/#using-f-expressions-in-filters)

## Func function
---
Func 방식은 Django에서 구현되지 않은 query의 구문을 사용하고자 할때 활용 가능합니다.

{% highlight python %}
class UNNEST(Func):
    function = 'UNNEST'

temp = Test.objects.annotate(user=UNNEST('user'))
{% endhighlight %}

[Func](https://brownbears.tistory.com/496)

## Q function
---
Q 방식은 Django에서 구현되어 있는 구현체로 조건들을 활용할때 사용하기 좋습니다.

{% highlight python %}
Product.objects.filter(Q(category='A') & Q(sub_category='AB'))
{% endhighlight %}

## Value function
---
Value는 기본적인 형태로 단순한 값을 의미합니다.

{% highlight python %}
User.objects.filter("user", Value("_"), "id")
{% endhighlight %}

## annotate function
---
annotate는 별칭을 주는것과 같으며 nested와 같은 구조에서 명칭이 복잡할때 사용 가능합니다.

{% highlight python %}
logs = OrderLog.objects.annotate(
   name=F("product__name"),
   price=F("product__price")
   ).values(
   'created', 'name', 'price'
   )
{% endhighlight %}

## subquery function
---
subquery는 query를 사용하여 query를 만드는 복잡한 형태의 query를 구성할때 사용합니다.

{% highlight python %}
from django.db.models import OuterRef, Subquery
newest = Comment.objects.filter(post=OuterRef('pk')).order_by('-created_at')
Post.objects.annotate(newest_commenter_email=Subquery(newest.values('email')[:1]))
{% endhighlight %}

# Transaction
---
database에서 일관적으로 한번에 작업이 되어야하는 단위를 transaction 이라합니다. 이를 통하여 안정된 서비스를 구현할 수 있으나 과도한 transaction은 오히려 서비스를 느리게 만들 수 있습니다.

{% highlight python %}
from django.db import transaction

@transaction.atomic()
def update_user(user_id: int, updated_company_name: str):
    Profile.objects.filter(user__id=user_id).update(company_name=updated_company_name)  
	User.objects.filter(id=user_id).update(company_name=updated_company_name)
{% endhighlight %}

* commit()
transaction을 종료하며 저장합니다.

* rollback()
transaction을 종료하며 처음으로 돌아갑니다.

* on_commit()
transaction commit 종료 이후에 동작이 되야할 경우 사용

* savepoint()
transaction 도중에 savepoint를 지정하여 commit 또는 rollback같은 작업을 할 수 있습니다.

# Signal
---
signal은 main logic과 별개로 실행해야하는 작업이 있을때 사용할 수 있습니다. 하지만 비동기적으로 작동되는 로직이 아니라서 [celery](https://velog.io/@qlgks1/Django-Celery-%ED%9A%A8%EA%B3%BC%EC%A0%81%EC%9D%B8-%EB%94%94%EB%B2%84%EA%B9%85-%EB%AA%A8%EB%8B%88%ED%84%B0%EB%A7%81-Logging-Flower-Prometheus-Grafanawith-Loki-Promtail)와 같은것을 활용하는것을 추천합니다.

{% highlight python %}
# 우선 signals.py 를 특정 앱(여기선 user) 안에 만든다.

from django.db.models.signals import post_save
from django.contrib.auth.models import User

def create_profile(sender, instance, created, **kwargs):
	if created == True:
    	user = instance
        profile = Profile.objects.create(
        	owner = user,
            user_name = user.username,
            email = user.email,
            name = user.first_name,
        )

post_save.connect(create_profile, sender=User)
# 아래에서 더 자세히 보겠지만, connect를 쓰기 싫으면, 아래 app config를 진행하면 된다.

# signal의 코드 분리를 위해 app config에서, app이 load 될 때 signal을 import하게 한다. 
# (user) apps.py
class UserConfig(AppConfig):
    name = 'user'

    def ready(self) -> None:
        # DB signal 
        import app.user.signals
        return super().ready()
{% endhighlight %}