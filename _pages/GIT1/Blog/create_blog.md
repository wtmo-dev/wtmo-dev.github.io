---
title: "GitHub blog"
tags:
    - blog
    - git
date: "2023-07-25"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# 깃허브 레포지토리 만들기
---
우선 깃허브의 계정 또는 조직(organization)을 생성을 한다.

아래와 같이 레포지 토리 생성을 시작한다.
![Image](/assets/img/git/blog/1.png){: width="100%"}
위의 사진에서 초록색 버튼을 클릭하고<br/><br/>
![Image](/assets/img/git/blog/2.png){: width="100%"}
위의 사진에서 \<name>에 계정이름 또는 조직이름을 기입한다.  
이름을 해당 방식과 다르게 제작할 경우 \<name>.github.io이 기본 도메인이 되지않고 \<name>.github.io/\<other> 이 기본 도메인이 된다.  
설정후 초록색 버튼을 클릭한다.<br/><br/>
![Image](/assets/img/git/blog/3.png){: width="100%"}
상단오른쪽의 settings로 들어간다.<br/><br/>
![Image](/assets/img/git/blog/4.png){: width="100%"}
왼쪽바에서 Pages로 들어가서 Branch를 /(root)가 되게 설정한다.<br/><br/>

# jekyll 설치하기
---
jekyll는 다양한 사이트 테마를 지원하며 수정하기 용이한 폼을 가진다.

## ruby 설치하기
---
ruby는 gem이라는 패키지 관리자를 지원하며 jekyll를 사용하기 위해 jekyll에서 추천하는 프로그래밍 언어이다.

[다운로드 사이트](https://rubyinstaller.org/downloads/){: width="100%"}

ruby를 설치하고 사용하려면 c, c++ 등을 추가적으로 사용하기 위한 Mingw가 필요하며 이는 ruby+Devkit을 다운받으면 MSYS2를 추가적으로 다운로드 받으며 같이 다운로드 받을 수 있다. 하지만 기존에 Mingw를 다운받았을 경우 MSYS2를 다운로드 받고 추가 다운로드를 진행하지 않아도 된다.<br/><br/>
![Image](/assets/img/git/blog/5.png){: width="100%"}
위와 같이 설정하여 다운받으면 마지막에 아래와 같이 뜨게 된다.<br/><br/>
![Image](/assets/img/git/blog/6.png){: width="100%"}
여기서 체크하고 다음으로 넘어가면 자동으로 MSYS2까지 다운이 받아진다. 만일 자동적으로 안될경우 안내문에 나와 있듯이 ruby prompt에서 ridk install을 입력하면 다운로드 창이 뜨게된다. 여기서 Mingw가 설치된 사람은 1 설치가 안된사람은 3을 선택하여 MSYS2를 설치하면 된다.

3을 선택하여 설치해도 Mingw가 설치가 안될 수있는데 이럴경우 부득이하게도 인터넷에서 직접설치해야한다.<br/><br/>

설치완료 후에는 아래와 같이 환경변수 설정이 되었는지 확인한다. 디렉토리 주소는 설치시 본인의 설치방식에 따라 다를 수 있다.

![Image](/assets/img/git/blog/7.png){: width="100%"}

설치 및 환경변수 설정이 완료 되었다면 cmd 창을 켜서

{% highlight shell %}
gem -v
gcc -v
g++ -v
ruby -v
{% endhighlight %}

를 입력 후 출력이 잘 나오는지 확인한다.
잘 나온다면 모든 설치가 잘 되었다는 의미이며 잘 되지 않을경우 ruby, gem은 루비설치 gcc, g++은 Mingw의 설치가 잘안되었음을 알 수 있다.<br/><br/>

이제 거의 다왔습니다.<br/><br/>

ruby prompt를 켜서

{% highlight shell %}
gem install jekyll bundler
{% endhighlight %}

을 입력하여 jekyll과 bundler를 다운받습니다. jekyll는 테마사용 bundler는 markdown 작성 후 동작확인을 위해 사용됩니다.<br/><br/>

![Image](/assets/img/git/blog/8.png){: width="100%"}
다시 깃허브로 돌아와서 블로그를 관리할 폴더를 생성 후 해당 폴더에 cmd를 통하여

{% highlight shell %}
git clone <address>
{% endhighlight %}

로 내려 받은 후 해당 폴더의 위치에 ruby prompt를 이용하여

{% highlight shell %}
jekyll new ./
{% endhighlight %}

를 입력하여 새 jekyll 사이트를 설치한다.<br/><br/>
ruby prompt로

{% highlight shell %}
bundle exec jekyll serve
{% endhighlight %}

입력하여 bundle로 jekyll를 실행 후 http://127.0.0.1:4000/에 접속하여 다운받은 jekyll가 정상 작동되는지 확인한다.
그럼 기본적인 설정은 완료가 되며 다음의 사이트에서 테마를 찾아본 후 사이트에서 지원하는 방법대로 나의 jekyll 사이트에 덮어씌우면 된다.

[사이트1](http://jekyllthemes.org/)  
[사이트2](https://jekyllthemes.io/free)  
[사이트3](https://jekyll-themes.com)  
[사이트4](https://jamstackthemes.dev/ssg/jekyll/)  