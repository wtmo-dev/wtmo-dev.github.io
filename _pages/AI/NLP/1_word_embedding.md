---
title: "1. Word embedding"
tags:
    - NLP
    - word embedding
date: "2023-12-11"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# Word2Vec
---
중심 단어와 주변 단어를 통한 예측 기반의 학습법  
* 유사어 구별이 힘듬
* 단어의 빈도수에 영향을 많이 받음
* 새로운 단어학습시 전체학습이 필요
* 사전의 크기가 학습시간에 영향이 큼

## CBOW
---
주변 단어를 보고 중심 단어를 예측하는 방법

## Skip-gram
---
중심 단어를 보고 주변 단어를 예측하는 방법(학습 횟수가 많음)

# FastText
---
<>으로 단어를 구분하고 n-gram을 통하여 단어를 나눠서 학습한다  
skip-gram과 유사한 학습법  
sub word들을 학습해 유사한 단어학습이 가능

# GloVe(Global Vectors for Word Representation)
---
기존의 LSA(Latent Semantic Analysis)는 문서에서 단어의 빈도를 기준으로 차원축소를 하는 방법론 -> 단어 의미 유추에 약함  
새로운 방법을 제안함(단어의 유사도를 고려)  
1. 윈도우 기반 동시 등장 행렬  
앞뒤로 등장한 단어들을 테이블화 하여 행렬로 만듬  
2. 동시 등장확률  
해당 행의 전체값에서 해당하는 값을 나눈값
3. 손실함수
동시 등장확률과 유사하게 나올 수 있게 함

konlpy
gensim
