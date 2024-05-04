---
title: "mysql password"
tags:
    - mysql
date: "2023-02-23"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# How to change password in mysql
---

{% highlight shell %}
mysql.server stop # mysql 종료
{% endhighlight %}

{% highlight shell %}
mysql.server start --skip-grant-tables # mysql 권한없이 접근 허용
{% endhighlight %}

{% highlight shell %}
mysql -u root # mysql root로 접근
{% endhighlight %}

{% highlight shell %}
update mysql.user set authentication_string=null where user='root'; # 임시로 password 삭제
flush privileges; # 권한 적용
{% endhighlight %}

{% highlight shell %}
mysql.server restart; # mysql 재실행
{% endhighlight %}

{% highlight shell %}
mysql -u root; # mysql 접근
{% endhighlight %}

{% highlight shell %}
alter user 'root'@'localhost' identified with caching_sha2_password by '<password>'; # 비밀번호 변경
{% endhighlight %}

* 권한 문제로 안될때
{% highlight shell %}
SHOW VARIABLES LIKE 'validate_password%'; # 권한 확인
SET GLOBAL <policy-name>=<VALUE>; # 권한 변경
{% endhighlight %}
