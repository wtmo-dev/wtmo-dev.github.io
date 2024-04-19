---
title: "3. 종합탐색(1)"
tags:
    - crawling
date: "2023-09-14"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **개요**
---
지금까지 파이썬을 이용한 몇몇가지 기능들을 공부했고 내용을 확립하기 위하여 간단한 프로젝트를 진행하기로 했다.  
시리와 같은 AI 봇은 아니지만 pandas, tts, stt, 크롤링까지 지금까지 배운것들을 토대로 간단하게 챗봇느낌의 프로그램을 제작해보았다.

## **내용**
---
자료 파트에서 참고하여 보면 아래와 같이 구성이 되어있다.
> proj  
> |  
> |--- main.py  
> |--- const.py  
> |--- bip.mp3  
> |--- /module  
> --- |--- api.py  
> --- |--- data_search.py  
> --- |--- speech_service.py  

기본적인 프로세스는 main.py에 변동성이 없는 데이터는 const.py에 그외 중복적으로 작동되는 함수들은 사용처 별로 정리하여 module폴더에 구성하였다.

main/Timo/waitInput
> stt를 활용하기 때문에 입력을 받아서 컨트롤하는 함수가 필요함을 느껴서 만들게 되었으며, bip이라는 인자를 이용해서 stt의 입력을 받을 준비가 되어 있는지 사용자가 알 수 있게 만들었습니다.

main/Timo/sst_classifier
> 로직을 관장하는 주된 함수로 제작하였으며, 로그인, 로그아웃, 검색, 날씨, 미세먼지, 게임, 수위 조사에 접근하여 핸들링하는 것을 가능하게 한다. 검색, 날씨 미세먼지의 경우 XX 검색 또는 검색XX와 같이 사용자에 따라서 사용법이 다를 수 있기에 두가지 모두 가능하게 했습니다. 검색의 경우는 조금 더 나아가 XXX XX 검색과 같이 여러 키워드 검색을 지원합니다.

main/Timo/__sst_classifier_error
> sst_classifier를 통하여 분류가 되지 않을때 접근하게 되며 다시 명령을 기다리는 상태가 된다.

main/Timo/__sst_data_error
> api와 crawling과 같은 데이터 검색을 진행할때 서버오류나 기타 오류들이 발생하면 접근하게 되며 맨처음 상태로 돌아가게 됩니다.

main/Timo/login
> 로그인을 하게 되면 접근하게 되며 추가적인 핸들링이 필요할 경우를 대비하여 함수화 하였습니다.

main/Timo/logout
> 로그아웃을 하게 되면 접근되며 추가 핸들링이 필요하면 작성하게된다.

main/Timo/naver_search
> 네이버 크롤링을 사용하여 검색결과를 제공하여 준다.

main/Timo/weather_search
> 날씨를 검색하여 주는 함수로 현재시간을 기준으로 해당 지역의 기상정보를 제공해준다.

main/Timo/pm_search
> 미세먼지를 검색하여 주는 함수로 검색 방식에는 여러가지로 나뉘게 된다. 단순히 서울에 대한 검색도 가능하며 서울 강남구와 같은 세부 지역도 가능하다. 로직으로는 지명을 토대로 좌표를 구하여 좌표를 기준으로 해당하는 지역의 지역번호를 받게되며, 해당 지역번호로 미세먼지 정보를 받아서 상세분류 작업을 통하여 사용자에게 제공하게 된다.

main/Timo/follow_up_game
> 끝말 잇기 게임으로 컴퓨터와 단어를 주고 받게 되는데 단어는 일부 제한량을 두어서 컴퓨터도 패배할 수 있게 제작했다.

main/Timo/dam_check
> 요즘 기습적인 폭우와 같은 문제로 인하여 침수사고가 많이 발생하고 있어 댐정보를 통하여 비교적 미리 확인이 가능하지 않을까 해서 제작을 하게 되었으며, 댐마다 실시간 저수율과 방류량을 알 수있다.

module/api/Request
> html, api 정보를 받아서 json의 형태로 변환시켜준다.

module/api/SgisApi/geoCoding
> 지역명을 받아서 해당지역을 좌표화해 반환해준다.

module/api/SgisApi/transformation
> 좌표계가 사용하고자 하는좌표계와 다를경우 좌표계를 변조할 필요가 있는데 해당 변조를 도와준다.

module/api/MetroApi
> 미세먼지 정보를 받아서 돌려주는 함수이다.

module/api/KorDictApi
> 사전에 단어가 있는지, 해당하는 글자로 시작하는 단어가 있는지 확인해주는 함수이다.

module/api/DamApi
> 댐정보를 받아오기 위한 함수이다.

module/data_search/Searching/bs_search
> bs를 반복적으로 사용하기위하여 만든 함수이다.

module/data_search/Searching/selenium_search
> 셀레니움을 사용할 것을 대비하여 만든 함수이다.

module/speech_service/SpeechService/stt
> stt를 제공하는 함수이다. bip 인자를 통해 bip음을 출력하기도 한다.

module/speech_service/SpeechService/tts
> tts를 제공하는 함수이다.


## **자료**
---
[링크](https://github.com/gitwtmo/webcrwaling1)
