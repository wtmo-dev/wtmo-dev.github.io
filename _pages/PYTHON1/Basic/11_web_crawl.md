---
title: "웹 크롤링"
tags:
    - python
    - basic
date: "2023-08-23"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **크롤링**
---
## **기본용어**
---
**스크래핑**은 데이터를 수집하는 모든 작업

**크롤링**은 웹상에 흩어져 있는 데이터를 수집하는 행위

**파싱**은 웹상에 흩어져 있는 데이터를 선별하여 수집하는 행위

## **robots.txt**
---
해당 홈페이지가 크롤링 허용범위의 권고안을 기입해 놓은 파일

```
User-agent:* : 브라우저 전부 접근 허용
Disallow: /  : 모든 디렉토리 비허용
Allow: /$ : 첫번째 페이지는 허용
```

## **HTTP**
---
**HTTP(Hypertext Transfer Protocal)**은 서버와 클라이언트가 인터넷상에서 데이터를 주고 받는 프로토콜으로 아래의 작동방식을 가진다.

* Request : HTTP요청
    * GET : 정보를 요청하기
    * POST : 정보를 입력하기
    * PUT : 정보를 업데이트하기
    * DELETE : 정보를 상제하기
* Response : HTTP응답

**URL**은 자원의 위치를 알기위한 프로토콜

**parameter**는 시스템의 작동에 영향을 주는 데이터

## **HTML & Tag**
---
**HTML(Hypertext markup language)**은 웹페이지를 구조화하기 위한 마크업 언어이다.  
**Tag**는 html에서 사용하는 요소를 의미하고 아래와 같은 태그를 주로 활용한다.

```
<title> : 브라우저 타이틀
<head> : 문서의 속성을 설정하는 태그
<body> : 브라우저 바디의 최상위
<div> : 기본적인 구분자
<ul>(unordered list) : *으로 구분하는 리스트
<ol>(ordered list) : 숫자로 구분하는 리스트
<li> : 리스트 나열
<table> : 테이블 구조의 기본 형
<tr> : 테이블의 행을 만드는 형식
<td> : 테이블의 열을 만드는 형식
```

## **ID & Class**
---
**ID**는 일반적으로 고유의 객체를 찾을때 사용된다.  
**Class**는 일반적으로 유사한 객체들을 찾을때 사용(css에서 공통적으로 사용됨)
