---
title: "How to use Git"
tags:
    - git
date: "2023-08-08"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# 깃 글로벌 셋팅
---
{% highlight shell %}
git config --global core.autocrlf input # mac
git config --global core.autocrlf true # win
git config --global user.name "name"
git config --global user.email "email"
git config --global core.editor "vim" # editor를 vim으로 세팅
git config --global core.pager "cat" # pager를 cat으로 세팅
git config --global --list
{% endhighlight %}

autocrlf 문자 개행 세팅(줄바꿈)
shell에서 vim ~/.gitconfig로 수동 변경가능

# 깃 원격지 설정
---
{% highlight shell %}
git remote add <origin_name> <git_repo>
git remote -v
{% endhighlight %}

* 원격지 세팅
* 원격지 종류 확인

# 깃 작업 내역 확인
---
{% highlight shell %}
git status
{% endhighlight %}

# 파일 내부 작성자 확인
---
{% highlight shell %}
git blame <file_name>
{% endhighlight %}

# 깃 clone
---
{% highlight shell %}
git clone <url>
git clone <url> <dir>
{% endhighlight %}

* 깃 가져오기
* 깃 \<dir\>에 가져오기

# 깃 다음 버전에서 팔로우업 할 파일 추가
---
{% highlight shell %}
git add <file_name>
{% endhighlight %}

# 깃에 팔로우업한 파일 기준으로 새로운 버전을 생성 및 설명추가
---
{% highlight shell %}
git commit -m "<message>"
git commit --amend
{% endhighlight %}

* 깃 easy 커밋
* 직전 커밋 수정

# 현재 깃의 버전 로그 확인
---
{% highlight shell %}
git log
git reflog
{% endhighlight %}

* 전체 로그확인
* 하드 리셋한 로그까지 확인

# 깃 브랜치 관리
---
{% highlight shell %}
git branch
git branch -a
git branch <name>
git branch -d <name>
git branch -r
{% endhighlight %}

* 브랜치 리스트
* 브랜치 원격지 포함 리스트
* 브랜치 생성
* 브랜치 삭제
* 원격지 브랜치 확인

# 깃 브랜치 변경
---
{% highlight shell %}
git checkout <name>
git checkout -t <origin_name>
{% endhighlight %}

* 브랜치 변경
* 원격지 브랜치로 변경

# 깃 병합
---
{% highlight shell %}
git merge <name>
{% endhighlight %}

\<name\>을 현재 브랜치로 합치기

# 깃 리셋
---
{% highlight shell %}
git reset --hard HEAD~<num>
git reset --hard <commit_name>
{% endhighlight %}

* HEAD를 \<num\>횟수만큼 되돌아간다.
* HEAD를 \<commit_name\>으로 되돌아간다.

# 깃 복구
---
{% highlight shell %}
git reset --hard ORIG_HEAD
{% endhighlight %}

* HEAD를 기존의 ORIG_HEAD로 되돌린다.

# 깃 태그 관리
---
{% highlight shell %}
git tag <tag_name>
git tag <tag_name> <commit_id>
git push origin <tag_name>
git push --tags
git tag -d <tag_name>
git push origin :tags/<tag_name>
git tag -l "<tag_name>"
{% endhighlight %}

* 태그 생성
* 특정 커밋에 태그 생성
* 특정 태그 원격에 업로드
* 태그 전체 원격에 업로드
* 로컬 특정 태그 삭제
* 원격 특정 태그 삭제
* 태그 확인

# conventional commit  
---

[example](https://www.conventionalcommits.org/ko/v1.0.0)

1. commit 제목은 구나 절의 형태로 나타내기
2. capitalize 중요
3. prefix(type) 달기
    - feat : 기능 개발 관련
    - fix : 오류 개선, 버그 패치
    - docs : 문서화 작업
    - test : test관련
    - conf : 환경설정 관련
    - build : 빌드 작업 관련
    - ci : continuous integration 관련
    - chore : 패키지 매니저, 스크립트
    - style : 코드 포매팅 관련
    - refactor : refactoring 작업

example

> {type}:{description} 작업단위 축약(if ! after type mean breaking change happen)  
> {body} 작업 상세 기술  
> {footer} 부가정보(ex) BREAKING CHANGE:drop social login support

## pre-commit
---
commit을 하는데 있어서 통일 된 규격의 파일을 원격지에 올리기 위한 방법

{% highlight shell %}
pip install pre-commit

pre-commit sample-config > .pre-commit-config.yaml
cat .pre-commit-config.yaml

pre-commit run

pre-commit run -a

pre-commit install
{% endhighlight %}
