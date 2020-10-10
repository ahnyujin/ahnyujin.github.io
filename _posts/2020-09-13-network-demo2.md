---
title: Network2
author: Yujin Ahn
date: 2020-09-13 00:00:00 +0900
categories: [CS, Network]
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

- GET : 정보를 요청하기 위해 사용 (SELECT)
- POST : 정보를 밀어넣기 위해 사용 (INSERT)
- PUT : 정보를 업데이트하기 위해 사용 (UPDATE)
- DELETE : 정보를 삭제하기 위해 사용 (DELETE)
- HEAD : (HTTP)헤더 정보만 요청. // 해당 자원이 존재하는지 혹은 서버에 문제가 없는지를 확인하는 용
- OPTIONS : 웹서버가 지원하는 메서드의 종류를 요청
- TRACE : 클라이언트의 요청을 그대로 반환. // 서버 상태를 확인하기 위한 목적

- PUT vs POST
- PATCH vs PUT

# HTTP와 HTTPS
### HTTP (Hypertext Transfer Protocol)
- 서버와 클라이언트가 인터넷상에서 데이터를 주고 받기 위한 프로토콜
- **Stateless** (무상태) 프로토콜 : 응답 후 연결을 끊어버리기 때문에 클라이언트가 바로 다음것을 요청한다 하더라도 이전 상황 알 수 없음.
  - 장점 : 불특정 다수를 대상으로 하는 서비스에 적합하다.
  - 단점 : 클라이언트가 이전에 뭘 했는지 알 수 없다. ( 쿠키와 같은 기술 등장 )
### URL
- URL (Uniform Resource Locator)
  - 웹상에서 문서와 다른 자원들의 위치를 나타내기 위해 사용
  - 프로토콜 종류://IP 주소 또는 도메인/ 자원의 위치
  - 물리적인 컴퓨터를 찾은 후에 해당 컴퓨터 안에 등장하는 소프트웨어 서버를 찾기 위해서는 포트값이 필요하다.
### HTTPS (Hypertext Transfer Protocol Secure)

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