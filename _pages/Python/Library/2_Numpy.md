---
title: "Numpy"
tags:
    - python
    - library
    - numpy
date: "2023-08-30"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **Numpy(Numerical computing with Python)**
---
수치연산과 벡터 연산에 있어서 강한 이점을 가진 라이브러리

## **np.array**
---
> * 최초 선언 후 사이즈 변경이 불가능
> * 모든 원소의 데이터 타입이 동일해야한다 (homogeneous array)

## **Mixed Precision**
---
>> numpy는 아래와 같이 다양한 데이터 타입을 가지고 있다.  
>> np.int[8~64]  
>> np.uint[8~64]  
>
> **Mixed Precision**은 32비트(고용량)에서 메모리가 너무 사용될때 비트수를 내려서 메모리 부담과 속도를 관리하는 방법

## **np.arange(\<num\>)**
---
0~<num>-1 의 array 생성

## **\<np.array\>.shape**
---
\<np.array\>의 형태를 확인

## **\<np.array\>.reshape(x, y)**
---
\<np.array\>의 형태를 (x, y)로 변경
> * (x, ) 1차원 x개원소  
> * (x,1) 2차원 x개원소  
> * (-1, ) 1차원 원소 전부

## **\<np.array\> 연산**
---
연산은 벡터 연산으로 실행됨
> np.concatenate([\<np.array\>, \<np.array\>])  
> * +
> * -
> * @(dot product)

하지만 아래의 연산은 원소들 끼리 연산이됨  
> * \*  
> * /  

또다른 방법으로 연산을 붙이기 연산으로 사용하려면
> * np.concatenate([\<np.array\>, \<np.array\>], axis=\<axis\>)  
> 해당 차원(\<axis\>)의 붙이기만 가능  
>
> * np.vstack([\<np.array\>, \<np.array\>])  
> 수직적인 붙이기(axis=1)
>
> * np.hstack([\<np.array\>, \<np.array\>])  
> 수평적인 붙이기(axis=0)

## **broadcast**
---
차원이 다른 array의 연산을 할 수있는데 첫번째 차원이라도 원소의 크기가 같아야한다

### **universal Function**
broadcast의 확장적인 의미의 함수  
1 / \<np.array\>는 각각의 원소가 1로 나뉘어진 array가 나옴

## **numpy indexing**
---
python indexing과 같은 방법을 사용가능하며,  
\<np.array\>[x, y]로 \<np.array\>[x][y]를 표현 가능하다.

# Math Function
---

### **np.random.seed(0)**
---
랜덤 생성함수의 시드 고정(테스트 결과 비교할때 좋음)

### **np.random.rand(\<dimen\>)**
---
\<dimen\>에는 차원의 shape을 입력 e.x.(1,3)
0~1로 이루어진 지정 차원의 랜덤 array 생성

### **np.random.randn(\<dimen\>)**
---
\<dimen\>에는 차원의 shape을 입력 e.x.(1,3)
평균 0, 표준편차 1로 이루어진 지정 차원의 랜덤 array 생성

### **np.abs(\<np.array\>)**
절대값 생성

### **np.squre(\<np.array\>)**
제곱값 생성

### **np.sqrt(\<np.array\>)**
루트값 생성

### **np.abs(\<np.array\>)**
절대값 생성

### **np.linalg.norm(\<np.array\>)**
\<np.array\> 제곱합의 루트값 생성 (L2 norm)

### **np.linalg.eig(\<np.array\>)**
\<np.array\> eigenvalue(고유값)와 eigenvector(고유 벡터)값을 생성

### **np.sum(\<np.array\>, axis=)**
\<np.array\>의 차원에 따른 합

### **np.mean(\<np.array\>, axis=)**
\<np.array\>의 차원에 따른 평균

### **np.std(\<np.array\>, axis=)**
\<np.array\>의 차원에 따른 표준편차

### **np.min(\<np.array\>, axis=)**
\<np.array\>의 차원에 따른 최소값

### **np.max(\<np.array\>, axis=)**
\<np.array\>의 차원에 따른 최대값

### **np.argmin(\<np.array\>, axis=)**
\<np.array\>의 차원에 따른 최소값의 인덱스

### **np.argmax(\<np.array\>, axis=)**
\<np.array\>의 차원에 따른 최대값의 인덱스

### **np.sort(\<np.array\>, axis=)**
\<np.array\>의 차원에 따른 정렬(오름차순)  
np.sort(\<np.array\>, axis=)\[::-1\]\(내림차순\)

### **np.argsort(\<np.array\>, axis=)**
\<np.array\>의 차원에 따른 정렬한 값의 인덱스
