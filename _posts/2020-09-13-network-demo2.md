---
title: Network2
author: Yujin Ahn
date: 2020-09-13 00:00:00 +0900
categories: [Study, CS]
tags: [network]     # TAG names should always be lowercase
---

# 웹통신의 큰 흐름
브라우저에서 주소창에 url 입력시 어떤일이 일어나는가
    
1. 브라우저 검색창에 google.com검색
2. dns 캐시에 기록 있는지 확인, 없으면 isp (인터넷 서비스 제공업체)의 dns서버 통해서 ip찾기
3. ip주소의 서버와 TCP connection
4. 웹서버에 http요청
5. 받아온 response로 브라우저에서 display.

# HTTP Method

- POST
- GET
- PUT
- DELETE

- PUT vs POST
- PATCH vs PUT

# HTTP와 HTTPS
HTTP (Hypertext Transfer Protocol)

HTTPS (Hypertext Transfer Protocol Secure)

SSL(Secure Socket Layer)을 사용하는 통신 규약
1. 제3자가 보지 못하게 한다
2. 접속한 사이트가 믿을만한 곳인지 알 수 있게 해준다.
암호화 원리 : 공개키 암호화 방식

# TCP와 UDP
TCP/IP의 전송계층에서 사용되는 프로토콜
## TCP : 연결형 프로토콜
Transmission Control Protocol
### TCP Connection : 3-way-handshaking
1. open()을 실행한 클라이언트가 SYN을 보내고 SYN_SENT 상태로 대기
2. 서버는 SYN_RCVD 상태로 바꾸고 SYN과 ACK를 보
3. SYN과 ACK을 받은 클라이언트는 ESTABLISHED 상태로 변경하고 서버에게 ACK를 보냄
4. ACK를 받은 서버는 ESTABLISHED 상태로 변경
### TCP Disconnection : 4-way-handshaking
1. close()를 실행 클라이언트가 FIN을 보내 FIN_WAIT1상태로 대기
2. 서버는 CLOSE_WAIT으로 바꾸고 ACK 전달하고 해당 포트에 연결되어있는 어플리케이션에 close()요청
3. ACK를 받은 클라이언트 상태를 CLOSE_WAIT2로 변경
4. close() 요청을 받은 서버 어플리케이션은 종료 프로세스를 진행하고 FIN을 클라이언트에 보내 LAST_ACK 상태로 바꿈
5. FIN을 받은 클라이언트는 ACK를 서버에 다시 전송하고 TIME_WAIT으로 상태를 바꿈. TIME_WAIT에서 일정 시간이 지나면 CLOSED된다. ACK를 받은 서버도 포트를 CLOSED.
## UDP : 비연결형 프로토콜
User Datagram Protocol
- TCP보다 불안정하기는 하나 속도가 빠르다는 장점이 있음
#출처
[HTTP METHOD](https://medium.com/@lyhlg0201/http-method-d561b77df7)
[Http와 Https 이해와 차이점 그리고 오해(?)](https://jeong-pro.tistory.com/89)
[TCP 와 UDP 차이를 자세히 알아보자](https://velog.io/@hidaehyunlee/TCP-%EC%99%80-UDP-%EC%9D%98-%EC%B0%A8%EC%9D%B4)
[[TCP/UDP] TCP와 UDP의 특징과 차이](https://mangkyu.tistory.com/15)