---
title: "Django relations"
tags:
    - python
    - framework
    - Django
date: "2024-03-28"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# How to use relations in Django
---
relation은 모델을 더욱 유연하고 연결성이 좋게 만들 수 있습니다. 잘못 설정할 경우 오히려 복잡해지기도 하며, 아래의 방식을 참조하여 정확하게 설정해야 합니다.

Django에서는 다음 방식의 relation key가 있습니다.

* Foriegn Key(many to one)
일반적으로 가장 흔하게 사용되는 관계입니다. 다중값을 가져와야하여 query로 값이 나오게 됩니다.
* one to one
1대1로 매칭이 되는 상황에서 사용이 가능하며 object를 바로 가져오는 방식이 가능합니다.
* many to many
관계가 종속적이라기 보다 상호관계를 가지게 되는 형태로 가장 일반적이지 못한 형태입니다.

# Field of model
---
model의 column들을 정의 하는 field는 다음과 같이 사용할 수 있습니다.

## Field Option
---
Field의 옵션은 다음과 같으며 모든 Field가 모든 옵션을 사용할 수는 없습니다.

|Field 옵션|설명|
|---|---|
|to|필드의 기본값을 설정합니다.|
|related_name|추상 모델에서 관계를 정의할 때 사용될 이름을 의미합니다.|
|on_delete|개체가 제거될 때의 동작을 설정합니다.|
|db_column|데이터베이스의 컬럼의 이름을 설정합니다.|
|limite_choices_to|json형식으로 데이터베이스의 컬럼의 옵션을 추가해 filter를 적용합니다.|

다음은 on_delete일때 외래키의 작동요건을 나타냅니다.

|on_delete|의미|
|---|---|
|models.CASCADE|외래키를 포함하는 행도 함께 삭제|
|models.PROTECT|해당 요소가 함께 삭제되지 않도록 오류 발생 (ProtectedError)|
|models.SET_NULL|외래키 값을 NULL 값으로 변경 (null=True일 때 사용 가능)|
|models.SET(func)|외래키 값을 func 행동 수행 (func는 함수나 메서드 등을 의미)|
|models.DO_NOTHING|아무 행동을 하지 않음|

외래키는 정규참조와 역참조로 이루어지는데 일반적인 방식의 반대가 역참조입니다. 역참조는 일반참조와 달리 사용방법이 달라집니다. ```related_name```이 선언되어 있지 않으면 (1)와 같이 역참조가 가능하며 선언되어 있으면 (2)와 같이 참조가 가능합니다. (2)번 방식이 일반적으로 선호됩니다. 혹시나 2개이상의 참조를 하는 경우 (1)번 방식은 동작을 하지 않기 때문입니다.

* (1)
{% highlight shell %}
job1   = <related_table>.objects.get(id = 1)
people = job1.<relate_table>_set.all()
{% endhighlight %}

* (2)
{% highlight shell %}
job1   = <related_table>.objects.get(id = 1)
people = job1.<related_name>.all()
{% endhighlight %}
