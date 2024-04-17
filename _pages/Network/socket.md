---
title: "How to use socket"
tags:
    - socket
date: "2023-10-20"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# socket
---
통신을 위한 api

> socket
* domain 프로토콜 페밀리르 설명하는 정수
AF_INET or PF_INET이 일반적이다
* type 초기화 되는 소켓의 유형으로
TCP용 SOCK_STREAM, UDP용 SOCK_DGRAM이 일반적이다
* protocol 호출과 관련된 프로토콜을 설명
RAW 소켓이 아니면 0이된다.

> bind
* sockfd 소켓 식별 인식자
* my_addr 로컬 주소
* addrlen 로컬 주소의 길이

> accept
* sockfd 소켓 식별 인식자
* serv_addr 원격 주소
* addrlen 로컬 주소의 길이

---

> listen
서버에서 연결 큐를 작성하며 TCP의 사용방법이다.
* sockfd 소켓 식별 인식자
* backlog 큐의 길이

> accept
서버에서 클라이언트의 연결 요청을 기다리는 프로세스.
* sockfd 소켓 식별 인식자
* sockaddr 클라이언트 주소
* addrlen 클라이언트 주소 길이

---

> send
* sockfd 소켓 식별 인식자
* buffer 데이터 버퍼
* length 보내는 옥텟의 수
* flag 옵션 선택

> write
* sockfd 소켓 식별 인식자
* buffer 데이터 버퍼
* length 보내는 옥텟의 수

> sendto
UDP용
* sockfd 소켓 식별 인식자
* buffer 데이터 버퍼
* length 보내는 옥텟의 수
* flag 옵션 선택
* to 원격 주소
* tolen 원격 주소 길이

---

> recv
* sockfd 소켓 식별 인식자
* buffer 데이터 버퍼
* length 보내는 옥텟의 수
* flag 옵션 선택

> read
* sockfd 소켓 식별 인식자
* buffer 데이터 버퍼
* length 보내는 옥텟의 수

> recvfrom
UDP용
* sockfd 소켓 식별 인식자
* buffer 데이터 버퍼
* length 보내는 옥텟의 수
* flag 옵션 선택
* from 원격 주소
* fromlen 원격 주소 길이

---

> close
* sockfd 소켓 식별 인식자

> shutdown
* sockfd 소켓 식별 인식자
* how 종료 옵션