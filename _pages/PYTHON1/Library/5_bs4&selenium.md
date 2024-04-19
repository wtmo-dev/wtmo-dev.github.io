---
title: "bs4 & selenium"
tags:
    - python
    - library
    - bs4
    - selenium
date: "2023-09-04"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **requests**
---
python에서 가장 원형적인 파싱의 방법  

{% highlight python %}
import requests
import json

data = requests.get("https://jsonplaceholder.typicode.com/comments")
data = json.loads(data.text)
{% endhighlight %}

# **bs4**
---
html과 같은 정적인 페이지에서 데이터를 분류하기 위한 라이브러리

## **import**
---

{% highlight python %}
from bs4 import BeautifulSoup
{% endhighlight %}

## **request from homepage**
---
홈페이지에서 데이터가져오기

{% highlight python %}
request_data = requests.get("https://naver.com")
{% endhighlight %}

## **html parsing**
---
가져온 데이터 html형태로 파싱하기

{% highlight python %}
soup = BeautifulSoup(request_data.text,'html.parser')
{% endhighlight %}

## **select from parsing data**
---
* 파싱한 데이터에서 title 태그의 값들 가져오기

{% highlight python %}
result = soup.select('title')[0].text
{% endhighlight %}

* tag1에 속한 자손(tag2) 가져오기

{% highlight python %}
result = soup.select("tag1 tag2").text
{% endhighlight %}

* tag1에 속한 자식(직계 tag2) 가져오기

{% highlight python %}
result = soup.select("tag1 > tag2").text
{% endhighlight %}

* class1 가져오기

{% highlight python %}
result = soup.select(".class1").text
{% endhighlight %}

* id1 가져오기

{% highlight python %}
result = soup.select("#id1").text
{% endhighlight %}

* tag1에 href 속성을 가진것 가져오기

{% highlight python %}
result = soup.select("tag1[href]").text
{% endhighlight %}

* tag1 태그요소 중 \<num\>번째 요소 선택

{% highlight python %}
result = soup.select("tag1:nth-child(<num>)").text
{% endhighlight %}

* 파싱한 데이터에서 title 태그의 첫번째 텍스트 가져오기

{% highlight python %}
result = soup.select_one('title').text
{% endhighlight %}

## **header**
---
홈페이지에서 크롤링을 막을때 홈페이지 접근이 정상적인것 처럼할때 넣는다.  

{% highlight python %}
headers = {'User-Agent':'Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36'}
data = requests.get("https://jsonplaceholder.typicode.com/comments", headers=headers)
{% endhighlight %}

# **selenium**
---
js와 같이 동적인 기능이 활용된 페이지에서 데이터를 분류하기 위한 라이브러리  
(지도와 같이 변동성이 클경우 사용)

## **import**
---

{% highlight python %}
# 가장 원형의 드라이버를 가져온다
from selenium import webdriver
# 셀레니움 4에서 문법이 변경되면서 selector등을 사용할때 사용
from selenium.webdriver.common.by import By
# 키보드로 값을 넣을때 사용
from selenium.webdriver.common.keys import Keys
# 로딩중일때 어떠한 요소가 나올때까지 대기 가능하게 함
from selenium.webdriver.support.ui import WebDriverWait
# 로딩중일때 except문을 작성하기 위해 필요함
from selenium.webdriver.support import expected_conditions as EC
{% endhighlight %}

## **driver handling**
---
* 크롬을 이용하여 드라이버를 구동한다.

{% highlight python %}
driver = webdriver.Chrome()
{% endhighlight %}

* 드라이버를 이용해서 주소에 접속한다.

{% highlight python %}
driver.get(<url>)
{% endhighlight %}

* 해당 페이지를 전부 불러온다.(string type)  

{% highlight python %}
  <raw_source> = driver.page_source
{% endhighlight %}

* \<css_selector\>에 해당하는 첫 요소를 가져온다.

{% highlight python %}
  <element> = driver.find_element(By.CSS_SELECTOR, value=<css_selector>)
{% endhighlight %}

* \<css_selector\>에 해당하는 요소들을 가져온다.

{% highlight python %}
  <elements> = driver.find_elements(By.CSS_SELECTOR, value=<css_selector>)
{% endhighlight %}

* 해당하는 요소들을 클릭한다.

{% highlight python %}
  <element>.click()
{% endhighlight %}

* 드라이버를 종료시킨다.

{% highlight python %}
driver.quit()
{% endhighlight %}

## **WebDriverWait**
---
홈페이지가 로딩이 될때까지 기다리기 위한 구문
* \<time\>을 최대 대기 시간으로 하여 \<css_selector\>가 식별될때까지 기다린다.

{% highlight python %}
WebDriverWait(driver, <time>).until(EC.presence_of_element_located((By.CSS_SELECTOR, <css_selector>)))
{% endhighlight %}
