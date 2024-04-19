---
title: "1. essay quality"
tags:
    - kaggle
date: "2023-10-06"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

[kaggle-linking-writing-processes-to-writing-quality](https://www.kaggle.com/competitions/linking-writing-processes-to-writing-quality)

# Overview
---
글쓰기 품질을 예측하기 위한 모델을 만드는 대회이다.  
데이터는 키스트로크 로그 데이터로 이루어져 있다.(시계열)  

# Description
---
글쓰기 과정을 정형데이터로 만들기가 쉽지 않다. 에세이별로 작성자의 특성(쉬는 타이밍, 수정법, ...)을 파악하여 품질에 영향을 줄 수 있다. 하지만 실제는 결과물만 가지고 평가를 하게 되어서 실질적인 활용에 있어서는 고려해야할 사항이 많다.  

# Evaluation
---
평가지표로는 RMSE평가지표를 기반으로 사용한다. 이번대회는 특이하게 Efficiency RMSE 평가지표도 활용하여 추가 수상의 기회가 있다.  

# Data Collection Procedure
---

## Keystroke Data Collection Procedure
---
SAT에서 사용하는 글쓰기 프롬프트를 기반으로 하여 글쓰기를 하였다. 4종류의 다른 프롬프트가 사용이되어서 편차가 발생할 수 있다.  
30분이내에 3문단에 200단어이상으로 구성한 에세이를 작성해야한다. 또한 작성자가 2분이상 활동이 없거나 프롬프트 이외의 작업을 하려고 하면 경고창이 뜨게했습니다.  

## Keystroke Logging Program
---
키스트로크 정보를 수집하기위해 JS를 이용하여 만든 프로그램을 통하여 수집을 했다. JS에서 지원하는 addEventListener를 이용하여 수집을 하여 키 입력, 마우스 조작에 대한 값을 수집하게 된다. 이벤트는 순서대로 이벤트 ID에 라벨링을 하며 값을 가지게된다. 

## Keystroke Measures
---

### Production Rate
글쓰기 생산 비율은 글쓰기 과정에서 시간을 기준으로한 특징(문자, 단어, 문장, ...)을 나타내는 비율을 나타낸다. 
* 글쓰기 과정에서 분당 특징(문자, 단어, ...)의 갯수를 나타내는 비율 
* 글쓰기가 완성된 상태에서 분당 특징(문자, 단어, ...)의 갯수를 나타내는 비율 

### Pause
일시 중지행동은 2초의 임계값을 가지는 IKI(key down 입력 간의 간격)가 있는것을 의미한다. 이러한 일시중지 활동을 활용하여 아래와 같은 해석이 가능하다. 
* 일시중시 횟수(전체, 분당) 
* 일시중지 시간 비율(전체 시간 대비) 
* 일시중지 길이(전체 일시중지 시간의 평균) 
* 특징(단어, 문장, ...)들 사이에서 일시중지 길이 또는 빈도수

### Revision
글쓰기에서 수정과 관련된 항목이다. 삭제는 어디서든 단어를 지우는 행위를 칭하며, 삽입은 글쓰기의 마지막 위치가 아닌 위치에서 진행하는 입력을 칭한다. 
* 삭제 횟수(전체, 분당) 
* 삽입 횟수(전체, 분당) 
* 삭제한 길이(단어수) 
* 삽입한 길이(단어수) 
* 삭제 시간 비율(전체 시간 대비) 
* 삽입 시간 비율(전체 시간 대비) 
* 글쓰기 완료 vs 글쓰기 진행에서 변경된 단어수의 비율 비교 
* 글쓰기 완료 후 수정이 진행된 횟수와 길이 
* 수정이 이루어진 직후 이루어진 수정의 횟수, 길이 
* 현재 지점에서 발생한 수정의 횟수 
* 다른 지점에서 발생한 수정의 횟수 

### Burst
일시 중지 및 수정없이 지속적으로 글쓰기를 진행하는것을 버스트라고 한다. P-버스트는 일시중지를 기준으로 분리가 되는것, R-버스트는 수정을 기준으로 분리가 되는 글씨기 행위이다. 
* P-버스트의 숫자(전체, 분당) 
* R-버스트의 숫자(전체, 분당) 
* P-버스트의 시간 비율(전체 시간 대비) 
* R-버스트의 시간 비율(전체 시간 대비) 
* P-버스트의 길이(단어수) 
* R-버스트의 길이(단어수) 

### Process Variance
글쓰기의 분산은 글쓰는 과정에서 작성자가 구간별로 유창하게 작성하는것을 보기 위한 기준이다. 5 또는 10과 같이 특정값을 기준으로 전체를 분할하고 분할된 구역에서 생성된 문자의 수(전체, 분당)를 의미한다. 

# simple EDA
---

**키스트로크 로그 데이터는 아래와 같이 구성이 된다.**
* id는 에세이를 구별하는 인자 
* event_id는 해당하는 에세이에서 발생하는 서순을 확인하기 위한 인자 
* down_time은 해당 키는 누르는 시점의 시간 
* up_time은 해당 키를 떼는 시점의 시간 
* action_time는 up_time - down_time 
* activity는 취한 액션이 어떠한 활동인지를 구별하는 인자 
* down_event, up_event는 어떤 키스트로크인지 구별하는 인자(단순한 문자는 q로 마스킹 처리됨) 
* text_change는 해당 event를 통하여 변경된 logs를 나타내는 인자 
* cursor_position은 깜빡이는 커서가 현재 어디 있는지 나타내는 인자 
* word_count는 작성된 단어의 갯수 

![logs](/assets/img/Project_practice/kaggle/1_essay_quality/logs.jpg){: width="100%"}

**점수 데이터는 아래와 같이 구성이 된다.**
* id는 에세이를 구별하는 인자 
* score는 에세이의 점수 

![scores](/assets/img/Project_practice/kaggle/1_essay_quality/scores.jpg)

**키스트로크 로그의 info는 아래와 같이 결측값은 없다.**

![logs_info](/assets/img/Project_practice/kaggle/1_essay_quality/logs_info.jpg)

**점수 데이터의 info는 아래와 같이 결측값은 없다.**

![scores_info](/assets/img/Project_practice/kaggle/1_essay_quality/scores_info.jpg)

**키스트로크 로그의 describe는 아래와 같다.**

![logs_describe](/assets/img/Project_practice/kaggle/1_essay_quality/logs_describe.jpg){: width="100%"}

**점수 데이터의 describe는 아래와 같다.**

![scores_describe](/assets/img/Project_practice/kaggle/1_essay_quality/scores_describe.jpg)

# keystroke EDA

## Production Rate
---
문자, 단어, 문단등의 상황에서의 갯수와 비율을 살펴본다. 

### Production Rate(character)
문자의 갯수를 따지는 행위를 보면 각 액션에서 text_change가 어떻게 되었는지를 확인하면 볼 수 있다. text_change를 살펴보면 q로 마스킹 된 값, copy&paste와 같이 여러문자를 다루는 " => "로 구분하는값, Move행위를 통하여 문자들이 이동한 값, 특이값으로 크게 4종류로 구분을 할 수 있다. 

이것이 삭제를 하는 행위인지 작성을 하는 행위인지를 확인하기 위하여 logs에 새로운 칼럼을 만드는데 remove, move, cut과 같은 행위는 삭제를 하는 행위로 취급하여 text_change의 길이를 넣고, 작성을 하는 행위는 input, move, paste와 같은 행위로 취급하여 text_change의 길이를 넣었다. move와 같은 행위는 삭제와 작성을 동시에 행하는 작업이기 때문에 두가지 종류에 같이 포함이 된다.  
위의 작업을 진행하여보면 문제가 발생하게 된다. \n과 기타 특수문자가 여러개의 문자로 인식되는것이다. 그래서 전처리고 simple_text_change라는 column을 만들어서 \n과 기타 특수문자를 q로 마스킹하는 작업을 진행하고 분류를 하는 작업을 진행하게 되었다. 

위의 문자의 변화를 구분하게 됨으로 인하여 우리는 문자의 갯수와 비율을 살펴 볼 수 있게 되었다. 하지만 아직 확장된 개념의 단어, 문단에 대한 이해는 조금 더 EDA를 진행해야 알 수 있다. 

### Production Rate(word)

## Pause
---
다른 키스트로크와 다르게 가장 직관적인 탐색이 가능한 기법이다. IKI가 2초 이상인것이 pause이기 때문에 이전의 down_time을 down shift를 행하여 현재의 down_time과 비교를 했을때 2초이상의 차이가 나면 is_pause라는 column을 추가로 생성해 True값을 넣어주면서 시작을 한다. 

### Pause(count)
생성된 is_pause columns을 sum, 시간에 대하여 섹션을 나눠서 sum을 진행하면된다. 

### Pause(rate)
event_id의 시작과 끝의 시간 차이를 통하여 실제 작업시간을 확인하고 실제작업시간으로 일시중지한 시간의 합을 나눠서 구한다. 

### Pause(length)
is_pause에 해당하는 값들의 시간을 수치적으로 분석한다(mean, max, min, ...)

### Pause(per state)
* 단어의 경우 전, 후에 q의 입력이 있는지
* 문장의 경우 전, 후에 space의 입력이 있는지
* 문단의 경우 전, 후에 \n의 입력이 있는지
위의 케이스별로 빈도수와 길이를 구한다.

## Revision
---
삭제의 경우 판단하기가 쉬우며 Production Rate단에서 생성한 삭제된 단어가 존재할 경우 is_deletion을 True로 이루어진 column을 만들면 된다.  
삽입의 경우 판단하기가 쉽지 않다. 첫번째로 알아야하는것이 현재 내 커서의 위치가 마지막이 아닌지를 확인하고 Production Rate단에서 input에 해당하는 부분이 존재하는지 확인을 하면 된다.  
하지만 이번 대회에서 데이터를 확인해본 결과 작성도중 맨뒤에 스페이스를 놔두고 그 직전에 입력을 하는 등 입력을 하는 위치가 신뢰성이 조금 떨어지는것이 확인 되어서 2가지 가설을 세워 보았다. 
* 작성자가 실수를 한것이다. 
* 맨뒤의 스페이스는 자동으로 지워지는 프롬프트를 사용한것이다.  

이것은 cumsum을 이용한 누적글자수와 현재의 커서 위치를 분석하여 커서가 어디에 위치하는지를 분석해보고 스페이스 이후에 revision이 발생하면 스페이스를 제거하는 로직을 구성해 보았으나 오히려 정상적으로 작동하지 않은것을 확인하게 되었습니다.  
이후 데이터를 수동으로 추적해본 결과 스페이스가 지워지지않음을 확인하게 되어서 작성자가 맨뒤에 스페이스가 있는것을 잊고 작업을 했음을 알 수 있었습니다. 그렇기 때문에 작성자가 실수한것을 고려하여 revision을 진행할지 아니면 고려하지 않고 진행할지 방향이 두가지로 나뉘어지게 되었습니다. 

### Revision(deletion)
is_deletion을 sum으로 전부 합한 값, per minute

### Revision(insertion)
is_insertion을 sum으로 전부 합한 값, per minute

### Revision(deletion length)
is_deletion일때 문자 삭제 columns의 수의 합

### Revision(insertion length)
is_insertion일때 문자 생성 columns의 수의 합

### Revision(deletion rate)
is_deletion일때 시간의 합을 전체시간으로 나눈값

### Revision(insertion rate)
is_insertion일때 시간의 합을 전체시간으로 나눈값

### Revision(revisioned character)
문자 생성 columns의 수의 합과 문자 제거 column의 수의 합을 column으로 생성

### Revision(revision after producted)
current_cursor의 위치가 max_character의 위치와 같으면서 최대값인 이후에 진행된 event들에서 발생한 revision들의 횟수와 길이

### Revision(revision after revision)
is_deletion or is_insertion의 이후에 연속으로 발생한 revision의 횟수, 길이

### Revision(revision in same place)
current_cursor를 down diff로 값을 받아서 값이 변경하지 않았 했으면서 event가 Nonproduction가 아닌 revision이 발생하는 경우의 횟수현재 지점에서 발생한 수정의 횟수.
하지만 직전값을 인식하는 방식의 경우 올바르게 작동하지 않을 수 있기때문에 추가적으로 확인이 필요함

### Revision(revision in different place)
current_cursor를 down diff로 값을 받아서 값이 변경을 했으면서 event가 Nonproduction(기타 키입력, 마우스 클릭) revision이 발생하는 경우의 횟수.
하지만 직전값을 인식하는 방식의 경우 올바르게 작동하지 않을 수 있기때문에 추가적으로 확인이 필요함

## Burst
---

### Burst(p number)
is_pause간의 거리가 1이상인 burst의 숫자(is_pause.sum + 1), 분당 카테고리화 하여 is_pause.sum + 1

### Burst(r number)
is_revision간의 거리가 1이상인 burst의 숫자(is_revision.sum + 1), 분당 카테고리화 하여 is_revision.sum + 1

### Burst(p rate)
is_pause의 시간의 합을 전체 시간으로 나눠준 값을 1에서 뺀값

### Burst(r rate)
is_revision의 시간의 합을 전체 시간으로 나눠준 값을 1에서 뺀값

### Burst(p length)
is_pause간의 상태에서 단어의 변화량의 합

### Burst(r length)
is_revision간의 상태에서 단어의 변화량의 합

## Process Variance
---

### Process Variance(per state)
---
글쓰기의 분산은 글쓰는 과정에서 작성자가 구간별로 유창하게 작성하는것을 보기 위한 기준이다. 5 또는 10과 같이 특정값을 기준으로 전체를 분할하고 분할된 구역에서 생성된 문자의 수(전체, 분당)를 의미한다.

# Review
