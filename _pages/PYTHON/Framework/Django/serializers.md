---
title: "Django serializer"
tags:
    - python
    - framework
    - Django
date: "2024-03-25"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# What is serializer
---
Django의 serializer는 많은 역활을 담당합니다. 그중 대표적인 사용처는 json <-> dict 형태로의 치환을 주로 해주게 됩니다. 이러한 이유는 rest api에서 사용하는 형식과 python에서 사용하는 형식이 다르기 때문입니다.

# normal serializer
---
일반적인 seriallizer는 ```serializers.Serializer```의 상속을 받아 아래와 같이 작성하게 됩니다.

{% highlight python %}
class UserSerializer(serializers.Serializer):
    id = serializers.IntegerField(read_only=True)
    name = serializers.CharField(required=False, allow_blank=True, max_length=10)

    def create(self, validated_data):
        return models.User.objects.create(**validated_data)
{% endhighlight %}

위와 같은 방식은 model과 상관없이 serializer를 설정하고 싶을때 사용할 수 있으며, model을 활용하여 사용하는 방법도 있습니다.

# model serializer
---
model seriallizer는 ```serializers.ModelSerializer```의 상속을 받아 아래와 같이 작성하게 됩니다. 아래의 방식은 model이 선언되어 있을때 사용하기 용이하며 코드를 간편하게 해줍니다.

{% highlight python %}
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = models.User
        fields = ['id', 'name']
{% endhighlight %}

# method field
---
method field는 다른 field를 활용하여 재가공하여 사용하는 방식입니다. 대표적으로 id값이 있고 id의 길이를 확인하는 방법입니다.

{% highlight python %}
class UserSerializer(serializers.ModelSerializer):
    is_long = serializers.SerializerMethodField()
    
    class Meta:
        model = models.User
        fields = ['id', 'name']

    def get_is_long(self, instance: CheckedCrn):
        if len(instance.id) > 2:
            return "long"
        else:
            return "short"
{% endhighlight %}

# dict -> json -> dict
---
때에 따라서는 데이터의 형태가 계속 변경이 되어야 할 수 있습니다. 그에따라 형변환을 하는 법을 나타냅니다.

{% highlight python %}
import io

from rest_framework.renderers import JSONRenderer

content = JSONRenderer().render(serializer.data) # json

stream = io.BytesIO(content)
data = JSONParser().parse(stream)

serializer = UserSerializer(data=data)
serializer.is_valid()
serializer.validated_data # check data
serializer.save()
serializer.data # dict
{% endhighlight %}

# nested serializer
---

## N in (1:N)
---
1:N 의 형식에서 N의 입장은 다음과 같이 바로 활용이 가능합니다.

* seriallizer
{% highlight python %}
class GroupOnlySerializer(serializers.ModelSerializer):
    class Meta:
        model = Group
        fields = "__all__"

class UserWithGroupSerializer(serializers.ModelSerializer):
    product = GroupOnlySerializer(read_only=True)

    class Meta:
        model = User
        fields = "__all__"
{% endhighlight %}

* view
{% highlight python %}
class UserListAPIView(generics.ListAPIView):
    """
    - User GET ALL API
    """
    queryset = User.objects.all().order_by("-id")
    serializer_class = UserWithGroupSerializer
{% endhighlight %}

## 1 in (1:N)
---
1:N 의 형식에서 1의 입장은 역참조를 해야 하기 때문에 조금은 복잡합니다.

### Read case
---

* seriallizer
{% highlight python %}
class GroupSerializer(serializers.ModelSerializer):
    class Meta:
        model = Group
        fields = "__all__"

class UserSerializer(serializers.ModelSerializer):
    product = GroupSerializer(read_only=True, many=True)

    class Meta:
        model = User
        fields = "__all__"
{% endhighlight %}

* view
{% highlight python %}
class UserListAPIView(generics.ListAPIView):
    """
    - User GET ALL API
    """
    queryset = User.objects.all().order_by("-id")
    serializer_class = UserSerializer
{% endhighlight %}

### Write case
---
write case에서는 원래 read만 가능하기 때문에 create를 override하여 새로이 구성해줘야 합니다.

* seriallizer
{% highlight python %}
class GroupSerializer(serializers.ModelSerializer):
    class Meta:
        model = Group
        fields = "__all__"

class UserSerializer(serializers.ModelSerializer):
    product = GroupSerializer(read_only=True, many=True)

    class Meta:
        model = User
        fields = "__all__"
{% endhighlight %}

* view
{% highlight python %}
class UserListAPIView(generics.ListAPIView):
    """
    - User GET ALL API
    """
    queryset = User.objects.all().order_by("-id")
    serializer_class = UserSerializer

    def create(self, validated_data):
        groups = validated_data.pop('group')
        user = User.objects.create(**validated_data)
        for group in groups:
            Group.objects.create(user=user, **group)
        return user
{% endhighlight %}

# Prev(how to start)
---
[Prev](intro.html)
