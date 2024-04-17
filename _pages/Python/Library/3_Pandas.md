---
title: "Pandas"
tags:
    - python
    - library
    - pandas
date: "2023-08-31"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **Pandas(Python Data Analysis Library)**
---
정형데이터 조작에 최적화된 라이브러리
> * 행렬로 이루어진 테이블 형태구조의 데이터 연산이 뛰어나다
> * json,html,csv,xlsx,sql등등 다양한 정형화 데이터를 통일하여 표현가능

## **기본구조**
---
Pandas는 1차원 구조와 2차원 구조를 가지고 있으며 아래와 같다.
> * 1차원 구조  
> pd.Series([1,3,5,np.nan, 78])
> * 2차원 구조  
> pd.DataFrame(  
    data=np.arange(1, 49).reshape(12, 4),  
    index=np.arange(12),  
    columns=["X1","X2","X3","X4"]  
    )
>> * data= 구조를 만드는데 사용할 데이터 2차원구조 필요  
>> * index= 구조를 만드는데 사용할 인덱스명  
>> * data= 구조를 만드는데 사용할 컬럼명  

pandas의 내부 구조는 numpy array기반으로 생성해서 universal function 같은 numpy array의 기능을 사용할 수 있다.

# **Fancy indexing**
---
> * \<pd.data\>.\<columnName\> == \<pd.data\>[\<columnName\>]  
> \<pd.data\>의 해당 컬럼 기반의 시리즈 추출
> 
> * \<pd.data\>.index[\<num\>]  
> \<pd.data\>에서 \<num\>번째 인덱스이름 가져오기
>
> * \<pd.data\>.loc[\<indexName\>, \<columnName\>]  
> \<pd.data\>의 (\<indexName\>, \<columnName\>)에 해당하는 값을 추출(차원 구조로 작성시 해당 차원의 값이 전부 나옴)  
> <span style="color:red">**\<indexName\>**임이 중요하다 n을 넣으면 n-1이 아님</span>
>
> * \<pd.data\>.iloc[\<indexNum\>, \<columnNum\>]  
> loc과 작동이 같으나 Name이 아닌 Number를 기준으로 한다.

## **mask**
---
조건식을 적용하면 조건의 만족여부를 확인가능한 mask가 생성되며 해당 마스크로 데이터를 가공할 수 있다.  
> * \<pd.data\>[\<pd.data\>기반 조건]  
> \<pd.data\>에서 조건에 해당하는 데이터 추출

# **기본함수**
---
### **\<pd.data\>.index**  
\<pd.data\>의 인덱스값 추출

### **\<pd.data\>.columns**  
\<pd.data\>의 컬럼값 추출

### **\<pd.data\>.values**
\<pd.data\>의 값 추출

### **\<pd.data\>.apply(\<func\>)**
\<pd.data\>의 값을 \<func\>을 통해 가공하여 추출

### **\<pd.data\>.str.contains(pat=\<string\>, regex=Bool)**
\<pd.data\>에 \<string\>이 있는지 확인 regex=True(default)

### **\<pd.data\>[\<columnName\>]**
\<pd.data\>의 해당 컬럼 기반의 시리즈 추출

### **\<pd.data\>.head(\<num\>)**
\<pd.data\>의 인덱스 0에서 \<num\>(Null: 5)개 추출

### **\<pd.data\>.tail(\<num\>)**
\<pd.data\>의 인덱스 뒤에서 \<num\>(Null: 5)개 추출

### **\<pd.data\>.info()**
\<pd.data\>의 전반적인 정보를 제공

### **\<pd.data\>.describe()**
\<pd.data\>의 전반적인 통계치를 제공

### **\<pd.data\>.groupby(\<columns_name\>)**
\<pd.data\>에서 수치데이터를 \<columns_name\>의 기준으로 분별한다.

### **pd.to_numeric(\<pd.data\>, error=\<state\>)**
\<pd.data\>를 숫자로 변환한다.
* error="ignore": 숫자가 안되면 원본
* error="coerce": 숫자가 안되면 NaN
* error="raise": 숫자가 안되면 에러발생

### **pd.to_datetime(\<pd.data\>)**
\<pd.data\>를 시간타입의 값으로 변환한다.
* \<pd.data\>.dt.hour 과같이 원하는 값을 추출할 수 있다.

### **\<pd.data\>.sort_values(by=\<pd.columnName\>, ascending=False)**
\<pd.data\>의 값에서 \<pd.columnName\>를 기준으로 정렬  
ascending = True: 오름차순 False: 내림차순

# **Datafram 합치기**
---
### **pd.merge(\<pd.data\>, \<pd.data\>, on="A", how="outer")**
how="outer", "inner", "left", "right"
\<pd.data\>끼리 join을 이용한 합치기

### **pd.merge_asof(\<pd.data\>, \<pd.data\>, on="A", direction="backword")**
direction=  
* backword는 left에 매칭하여 빈공간없이 합치기  
* forword는 left에 매칭하여 빈공간있게 합치기  
* nearest는 left에 매칭하여 근처값으로 합치기  

### **pd.concat([\<pd.data\>, \<pd.data\>], axis=\<num\>)**
\<pd.data\>들을 \<num\>차원으로 합치기

### **\<pd.data\>.reset_index(drop=Null)**
\<pd.data\>의 인덱스를 재정의
drop= True는 기존 인덱스 삭제 False는 기존 인덱스 남겨둠

# **pivot table**
---
특정 컬럼을 기준으로 통계량을 측정하여 판다스 테이블화 하는것

> * pd.pivot_table(data=\<pd.data\>, index=[\<columnName\>], values=[\<columnName\>], aggfunc=[\<option\>,\<option\>])  
>
> index에 입력한 \<columnName\>을 인덱스로 하고 values에 입력한 \<columnName\>이 columns가 되는 테이블을 만듬  
>
> aggfunc에 있는 \<option\>에 해당하는 값으로 column을 만듬 e.x. sum, mean, count 등등...

# **unpivot**
---
pivot화 된 데이터를 풀어헤치는 행위  
stack은 기준이 없을때 melt는 기준이 있을때 용이

### **(with)stack**

stack -> columns to index / unstack -> index to columns
> * \<pd.data\>.stack(level=[0,...], dropna=True).reset_index().set_axis([], axis=1)  
> level은 columns의 최상단부터 0으로 매겨지며 해당하는 columns를 index로 보내고 인덱스를 리셋하여 다시 네이밍을 하는 방법

### **(with)melt**

> * \<pd.data\>.melt(id_Vars=None, value_vars=None, var_name=None, value_name="value")  
> id_Vars를 기준으로 데이터를 풀어헤치며 데이터를 value, columns를 variable로 분배한다.

# **외부 Datafram 불러오기**
---
### **colab**
{% highlight python %}
from google.colab imort drive
drive.mount('/content/drive')
data = pd.read_csv("/dir/data.csv")
{% endhighlight %}

### **window**
{% highlight python %}
data = pd.read_csv("/dir/data.csv")
{% endhighlight %}
