---
title: "basic window setting"
tags:
    - window
date: "2024-02-13"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# env setting
---

환경변수 정보 가져오는 방법입니다.
"User" 사용시 사용자 환경변수, 없애면 시스템 환경변수를 가져옵니다.
{% highlight shell %}
[System.Environment]::GetEnvironmentVariable(<var>, "User")
{% endhighlight %}

{% highlight shell %}
$userenv = "" # userenv라는 명칭의 변수사용

$env:path # system path

$env:userprofile # user root path

$env:<variable-name> # other variables
{% endhighlight %}

환경변수를 지정해주는 방법입니다.
{% highlight shell %}
[System.Environment]::SetEnvironmentVariable("PATH", $userenv + ";C:\Users\Administrator\Ubuntu", "User")
{% endhighlight %}

환경변수를 제거해주는 방법입니다.
{% highlight shell %}
$removePath = "<path>" # 삭제할 path 설정

$regexRemovePath = [regex]::Escape($removePath) # 삭제할 path 규격화

$arrPath = $env:Path -split ';' | Where-Object {$_ -notMatch 
"^$regexRemovePath\\?"} # 삭제할 path 제외하고 정렬

$env:Path = $arrPath -join ';' # 정렬한 path 적용

{% endhighlight %}

