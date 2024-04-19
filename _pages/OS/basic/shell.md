---
title: "basic shell command"
tags:
    - shell
date: "2023-10-05"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# shell command
---
whild card * can use with regex's [] format  

## cd
---
{% highlight shell %}
cd <dir>
cd ..
cd ~
{% endhighlight %}

* 디렉토리 이동  
* 디렉토리 앞으로 가기  
* 메인 디렉토리로 가기  

<br/>

## mkdir  
---
{% highlight shell %}
mkdir <dir_name>
{% endhighlight %}
* \<dir_name\> 폴더 만들기

<br/>

## touch
---
{% highlight shell %}
touch <file_name>
{% endhighlight %}
* \<file_name\> 파일 만들기

<br/>

## cat
---
{% highlight shell %}
cat <file_name>
{% endhighlight %}
* \<file_name\> 파일 내용보기

<br/>

## mv
---
{% highlight shell %}
mv <file_name> <to_dir>
mv <file_name> <to_dir>/<file_name_change>
{% endhighlight %}
* \<file_name\>을 \<to_dir\>로 이동
* \<file_name\>을 \<file_name_change\>로 이름바꿔서 \<to_dir\>로 이동

<br/>

## cp
---
{% highlight shell %}
cp <file_name> <to_dir>
cp <file_name> <to_dir>/<file_name_copy>
{% endhighlight %}
* \<file_name\>을 \<to_dir\>로 복사
* \<file_name\>을 \<file_name_change\>로 이름바꿔서 \<to_dir\>로 복사

<br/>

## rm
---
{% highlight shell %}
rm <file_name>
{% endhighlight %}
* \<file_name\>을 삭제

<br/>

## vim
---
{% highlight shell %}
vim <file_name>
{% endhighlight %}
* insert mode #i
* insert mode+1 #a
* visual mode #v
    * h - 왼쪽
    * j - 아래
    * k - 위
    * l - 오른쪽
* normal mode #esc
    * dd - delete
    * p - copy
    * :q - quit
    * :q! - force quit
    * :wq - write and quit