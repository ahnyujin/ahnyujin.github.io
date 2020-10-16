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
