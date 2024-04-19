---
title: "2. 멜론차트"
tags:
    - crawling
date: "2023-09-07"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

웹크롤링을 연습하기 위해서 멜론 1~50위의 내역을 추출해 csv파일로 저장하여 보았다.

{% highlight python %}
import requests
from bs4 import BeautifulSoup as BS
import pandas as pd

headers = {'User-Agent':'Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36'}
url = "https://www.melon.com/chart/index.htm"

data = requests.get(url=url, headers=headers)
soup = BS(data.text,'html.parser')
datas = soup.select(".service_list_song .wrap_song_info a")

rows=[]
columns=[]
for index, i in enumerate(datas):
    if index / 4 < 50:
        if index % 4 == 0:
            print(f"순위: {int(index / 4)+1}")
            print(f"제목: {i.text}")
            columns.append(str(int(index / 4)+1)+"위")
            columns.append(i.text)
        elif index % 4 == 1:
            print(f"가수: {i.text}\n")
            columns.append(i.text)
        elif index % 4 == 2:
            rows.append(columns)
            columns=[]
data = pd.DataFrame(columns=["순위", "제목", "가수"],data=rows)
data.to_csv("melon_rank.csv", encoding="utf-8-sig", index=False)
{% endhighlight %}

웹크롤링을 연습하기 위해서 셀레니움을 이용하여 월별로 멜론 1~50위의 내역을 추출해보았다.

{% highlight python %}
from bs4 import BeautifulSoup as BS
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

url = "https://www.melon.com/chart/month/index.htm"

if __name__ == "__main__":
    driver = webdriver.Chrome()
    driver.get(url)
    WebDriverWait(driver, 10).until(EC.presence_of_element_located((By.CSS_SELECTOR, '#conts > div.calendar_prid > div')))
    a = driver.find_element(By.CSS_SELECTOR, value='#conts > div.calendar_prid > div')
    a.click()
    a = driver.find_elements(By.CSS_SELECTOR, value='#conts > div.calendar_prid > div > div > dl > dd.month_calendar > ul > li')
    for month_index, month in enumerate(a):
        month.click()
        time.sleep(2)
        data_raw = driver.page_source
        soup = BS(data_raw, 'html.parser')
        title_datas = soup.select("#lst50 > td:nth-child(6) > div > div > div.ellipsis.rank01 > span > a")
        singer_datas = soup.select("#lst50 > td:nth-child(6) > div > div > div.ellipsis.rank02 > span")
        real_singer_datas = []
        for singer_data in singer_datas:
            b=singer_data.select('a')
            a=""
            try:
                a = b.text
            except:
                for i in b:
                    a += f"{i.text}, "
                real_singer_datas.append(a)
            else:
                real_singer_datas.append(a)
        for index, i in enumerate(title_datas):
            print(f"{month_index+1}월 {index+1}위 노래: {i.text} 가수: {real_singer_datas[index]}")
    time.sleep(5)
    driver.quit()
{% endhighlight %}
