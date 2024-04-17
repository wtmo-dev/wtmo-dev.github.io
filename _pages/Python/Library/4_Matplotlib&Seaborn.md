---
title: "Matplotlib & Seaborn"
tags:
    - python
    - library
    - Matplotlib
    - Seaborn
date: "2023-09-01"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---
# **Matplotlib**
---
파이썬 시각화 라이브러리로 matlab을 참고하여 제작함.
주로 논문에서 figure를 작성할때 사용함.
> * pyplot  
> 빠르고 간단하게 그래프를 그릴때 사용  
> * OOP-style  
> 구체적으로 요소들을 손봐서 그래프를 그릴때 사용

## **pyplot**
---
아래 3개와 같이 기본적인 형이 존재하며 추가적인 속성들을 변경하여 그래프를 그린다.

* 단일 plot 생성

{% highlight python %}
plt.figure()  
plt.plot()  
plt.show()  
{% endhighlight %}

* 단일 plot에 그래프들 겹치기

{% highlight python %}
plt.figure()  
plt.plot()  
plt.plot()  
plt.show()  
{% endhighlight %}

* 다중 plot 작성

{% highlight python %}
plt.figure()  
plt.subplot(<axis0 size>,<axis1 size>,<position num>)
plt.subplot(<axis0 size>,<axis1 size>,<position num>)
plt.show()  
{% endhighlight %}

다음과 같은 데이터가 있을때  

{% highlight python %}
x = ["data1", "data2", "data3", "data4"]  
y = [111, 156, 487, 445]  
z = [50, 549, 450, 42]  
{% endhighlight %}

아래와 같은 그래프들을 그릴 수 있으며

{% highlight python %}
plt.bar(<data1>, <data2>, *arg)  
plt.barh(<data1>, <data2>, *arg)  
plt.plot(<data1>, <data2>, *arg)  
plt.scatter(<data1>, <data2>, *arg)  
{% endhighlight %}

아래와 같은 옵션들을 사용이 가능하다

{% highlight python %}
plt.figure(figsize=(10,5))  
plt.plot(x,y, label="plot", width=0.2, color="red", marker="^")  
plt.title("Title", fontdict={'fontsize': 10}, loc="center")  
plt.xlabel("menu", fontdict={'fontsize': 10}, loc="left")  
plt.ylabel("data", fontdict={'fontsize': 10}, loc="bottom")  
plt.legend(loc="upper right")  
plt.yticks([1,2,5,50,100,200])  
plt.ylim(0, 1000)  
plt.grid(alpha=1, color="red", linewidth=10)  
{% endhighlight %}

# **Seaborn(Statisical Data Visualization library based on Matplotlib)**
---
Matplotlib를 참고하여 제작하였으나 파이썬의 라이브러리에 더 친화적이다.  
pandas의 dataframe을 사용하는데 용이함  
기본적인 세팅은 plt와 같으며 아래와 같이 제공하는 데이터를 불러올 수 있다.

{% highlight python %}
data = sns.load_dataset("penguins")
{% endhighlight %}

NaN 데이터는 아래와 같이 정리가 가능하며

{% highlight python %}
data = data.dropna()  
data.isnull()  
data[data.isnull().any(axis=1)]
{% endhighlight %}

plt외에도 아래와 같은 세팅도 가능하다.

{% highlight python %}
sns.set_palette("bone")
{% endhighlight %}

## **히스토그램**
---
{% highlight python %}
sns.histplot(data=data, x="body_mass_g", bins=15, hue="species", multiple="stack")
{% endhighlight %}

## **밀도표**
---
{% highlight python %}
sns.displot(data=data, kind="kde", x="body_mass_g", hue="species", col="island")
{% endhighlight %}

## **막대그래프**
---
confidence interval(Default: 에러영역)를 가짐

{% highlight python %}
sns.barplot(data=data, x="species", y="body_mass_g", hue="sex", ci="sd")
sns.barplot(data=data, x="body_mass_g", y="species")
{% endhighlight %}

## **갯수표**
---
{% highlight python %}
sns.countplot(data=data, x="sex")
{% endhighlight %}

## **박스 그래프**
---
outlier를 확인할 수있음

{% highlight python %}
sns.boxplot(data=data, x="sex", y="bill_depth_mm")
{% endhighlight %}

## **violin 그래프**
---
분포를 확인하는데 효과적임
sns.violinplot(data=data, x="species", y="bill_depth_mm")

## **라인 그래프**
---
경향성과 confidence interval(Default: 에러영역)를 가짐

{% highlight python %}
sns.lineplot(data=data, x="body_mass_g", y="bill_depth_mm")
{% endhighlight %}

## **포인트 그래프**
---
경향성과 confidence interval(Default: 에러영역)를 가짐

{% highlight python %}
sns.pointplot(data=data, x="body_mass_g", y="bill_depth_mm")
{% endhighlight %}

## **분산도 그래프**
---
{% highlight python %}
sns.scatterplot(data=data, x="body_mass_g", y="bill_depth_mm")
{% endhighlight %}

## **페어 그래프**
---
numeric value들의 비교표들 모음

{% highlight python %}
sns.pairplot(data=data, hue="species")
{% endhighlight %}

## **히트맵 그래프**
---
상관관계를 색상으로 나타냄  
상관계수 파악을 위해 corr matrix 생성하여 만듬  

{% highlight python %}
corr = data.corr(numeric_only = True)

sns.heatmap(data=corr, square=True, cmap="Blues", annot=True, fmt=".4f")
{% endhighlight %}
