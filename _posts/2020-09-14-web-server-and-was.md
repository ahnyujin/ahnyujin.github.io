---
title: 웹서버와 WAS의 차이
author: Yujin Ahn
date: 2020-09-14 20:00:00 +0900
categories: [Study, CS]
tags: [web]     # TAG names should always be lowercase
---
# 웹서버
웹서버 소프트웨어
- 클라이언트가 요청한 html문서나 각종 리소스를 전달한다.
- 요청한 리소스를 반환
- 웹브라우저나 웹크롤러가 요청하는 리소스는 정적 데이터이거나 동적인 결과가 될 수 있다.
- 기본적으로 정적 컨텐츠 제공
  - WAS를 거치지 않고 바로 자원 제
- 동적 컨텐츠 제공을 위한 요청 전달
  - 클라이언트의 요청을 WAS에 보내고, WAS에서 처리한 결과를 클라이언트에게 전달
- Apache, Nginx, Microsoft, Google 웹서버

# WAS
WAS(Web Application Server)
일종의 미들웨어로 웹 클라이언트의 요청 중 웹 애플리케이션이 동작하도록 지원하는 목적
- Tomcat, JBoss

WAS도 미들웨어
1. 프로그램 실행환경과 데이터 베이스 접속 기능
2. 여러개의 트랜잭션 관리
3. 업무를 처리하는 비즈니스 로직 처리.

## 웹서버가 WAS 앞단에 있으면 좋은 이유
- 웹서버 상대적으로 간단하게 구성할 수 있다.
- 대용량 웹어플리케이션인 경우 서버가 여러개일 수 있다. 
- WAS에 오류가 발생하면 앞단의 웹서버에서 먼저 해당 WAS를 이용하지 못하게 하고 무중단으로 사용자 WAS 재시작 할 수 있다
- 해당 웹어플리케이션을 이용하는 사람은 was에 문제가 있는지 모르게 할 수 있다. = 장애 극복 기능

- 기능을 분리하여 서버 부하 방지
- 물리적으로 분리하여 보안강화
- 여러대의 WAS를 연결 가능
  - 로드밸런싱 역할 및 fail over, fail back처리에 유리
- 여러 웹어플리케이션을 서비스 가능

## WAS만으로 구동 가능?
- 웹서버 없이 와스만 있어도 정적 동적 컨텐츠 모두 제공.
- 옛날에는 웹서버보다 정적 데이터를 성능이 안좋았을때도 있으나 현재는 성능 비슷
- 보안 때문에 웹서버를 두는 이유도 있음. 

## 동적 데이터 없다면 웹서버만으로 가능?

# 정적 데이터 동적 데이터
정적 데이터
- 이미지, html, css, js
- 컴퓨터에 저장되어 있는 파일
동적 데이터
- 웹서버에 의해 실행되는 프로그램을 통해 만들어진 결과

# 미들웨어
등장 배경
- dbms의 등장과 dbms에 직접 접근하는 클라이언트 프로그램 유행
- 클라이언트의 로직이 많아져 크기가 커진다는 문제점이 있다.
- 또한 클라이언트의 로직이 변경되면 클라이언트를 업데이트해주어야함.
- 보안도 나쁨 
클라이언트와 dbms사이에 또식 다른 서버를 두는 방식
미들웨어에서 대부분의 로직을 수행한다.
```
many 클라이언트 - 미들웨어 - dbms
```
프로그램 로직이 변경된다 하더라도 미들웨어만 변경해주면 된다.

# 웹 크롤러란?
네이버나 구글 같은 검색사이트에서 다른 웹사이트 정보를 읽어갈떄 사용하는 소프트웨어

# DBMS
DBMS(database management system)
- 데이터베이스 관리하는 시스템
- 이전에는 파일로 데이터를 관리, dbms
- mysql,mariaDB를
- 보통 서버형태로 서비스 제공

# 추가
CGI? (Common Gateway Interface) 외부 프로그램과 통신하는 방법을 정의한다. 웹사이트에서 동적인 페이지를 만드는 가장 흔하고 간단한 방법이다.
WAS(Web Application Server)는 CGI 표준을 따르는 구현 기술들을 실행할 수 있는 서버
자바에 웹 서비스를 위해 지원하는 기술로는 JSP(Java Server Pages)가 있습니다.

# 출처
- [부스트코스, 웹서버](https://www.edwith.org/boostcourse-web-be/lecture/58946/)
- [부스트코스, was](https://www.edwith.org/boostcourse-web-be/lecture/58947/)
- [아파치 투토리얼: CGI를 사용한 동적 페이지 생성](https://httpd.apache.org/docs/trunk/howto/cgi.html)
- [CGI와 WAS, 무슨차이인가요?](https://www.slipp.net/questions/197)
- [WSGI, WAS, CGI 이해](https://brownbears.tistory.com/350)