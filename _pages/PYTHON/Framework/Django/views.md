---
title: "Django view"
tags:
    - python
    - framework
    - Django
date: "2024-03-26"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# What is View
---

# How to use View
---
view를 사용하는 방식은 Fuction, Class 두가지 방식이 있습니다. 원래의 Django는 Fuction으로 구성되어 있었으나 OOP의 장점을 이용하는 Class 형식이 추후에 추가 되었습니다.

## FBV
---
다음은 Fuction을 사용한 View의 기본 예제입니다.

{% highlight python %}
@api_view(['GET', 'POST'])
def index(request):
	if request.method == 'POST':
    		return HttpResponse("Post method")
    	else:
    		return HttpResponse("Get method")
{% endhighlight %}

## CBV
---
다음은 class를 사용한 View의 기본 예제입니다. 이러한 방식은 상속과 같이 확장성을 가지지만 모든 상황에서 최선은 아닙니다.

{% highlight python %}
from django.views import View

class ContactView(View):
	def post(self, request):
    		return HttpResponse("Post method")
	def get(self, request):
    		return HttpResponse("Get method")
{% endhighlight %}


{% highlight python %}
# quickstart/views.py
from django.http import HttpResponse, JsonResponse
from django.views.decorators.csrf import csrf_exempt
from rest_framework.parsers import JSONParser # 그냥 json 파싱만 위해,,

@csrf_exempt
def snippet_list(request):
    """
    List all code snippets, or create a new snippet.
    """
    if request.method == 'GET':
        snippets = Snippet.objects.all()
        serializer = SnippetSerializer(snippets, many=True)
        return JsonResponse(serializer.data, safe=False)

    elif request.method == 'POST':
        data = JSONParser().parse(request)
        serializer = SnippetSerializer(data=data)
        if serializer.is_valid():
            serializer.save()
            return JsonResponse(serializer.data, status=201)
        return JsonResponse(serializer.errors, status=400)
{% endhighlight %}

# Prev(how to start)
---
[Prev](intro.html)
