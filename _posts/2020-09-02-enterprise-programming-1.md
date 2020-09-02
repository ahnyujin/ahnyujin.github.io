---
title: Enterprise Programming 1
author: Yujin Ahn
date: 2020-09-02 13:45:00 +0900
categories: [2020FallSemester, EnterpriseProgramming]
tags: [etc]     # TAG names should always be lowercase
---

## 앞으로 공부할 것

1. Java Script
2. React
3. AWS Lambda
    - https://serverless-stack.com/#table-of-contents
4. Authentication

## OT
#### 간략한 웹의 동작 방식
```
[Application user] <-> [WebClient] <-> [WebServer] <-> [Database]
```

user가 웹 클라이언트에(ex 크롬) 요청하면 웹 클라이언트가 웹 서버에 요청하고 response받아오는 형식이다.

이때 response는 object형태로 html을 포함하고 있다.

HTML을 발전시켜서 CSS를 넣고(style에 관한), javascript(action에 관한)를 넣을 수 있게 되었다.

#### 프론트엔드와 백엔드
규모가 커져 클라이언트 측 프로그램과 서버 측 프로그램을 나눔.

프론트엔드(보여주는 쪽) html,css,js / 백엔드 webserver 뒷단

웹서버는 동시접속자 해결하기 위해 concurrent하게 programming하게 되었다.

접속자가 이전에 언제 접속했는지 모르는 **stateless**한 성질이 있음.

서버는 다양한 request에 대한 url을 두었고, 각 url에 대한 처리를 하게 됨. = 라우팅

stateless한 성질 때문에 db를 사용하게 됨.
#### 프레임워크

프레임워크란

"소프트웨어의 구체적인 부분에 해당하는 설계와 구현을 재사용이 가능하게끔 일련의 협업화된 형태로 클래스들을 제공하는 것"

ex ) java의 spring, python의 flask django, js 

원래 자바스크립트는 프론트 언어였는데, node.js 플랫폼을 사용해 웹브라우저가 아닌 서버에서 돌게 할 수 있음.

node.js의 프레임워크는 express가 있음.

프론트엔드
html, css, js, jQuery

HTML, CSS, JS 프레임워크
- BootStrap
    - 자주 사용하는 style을 제공. 모바일로도 작동 가능하다.

Java Script의 프레임워크
- Ajax
    - js를 사용한 비동기 통신, 클라이언트와 서버간의 XML데이터를 주고받는 기술
- Angular.js, Vue.js, React.js

#### P.S.
강의내용을 요약한 것이라 흐름이 매끄럽지 않습니다. 부족한 내용은 다음 post에 차근차근 채워나가겠습니다 :)

#### 출처
프레임워크의 정의 https://jokergt.tistory.com/89