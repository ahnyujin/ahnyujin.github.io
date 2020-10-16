---
title: Network
author: Yujin Ahn
date: 2020-09-11 00:00:00 +0900
categories: [CS, Network]
tags: [network]     # TAG names should always be lowercase
---
# 용어 정리
- 네트워크
  - 컴퓨터를 두 대 이상 연결하여 서로 데이터를 전송할 수 있는 통신망이다.
- 인터넷
  - TCP/IP 프로토콜을 사용하는 세계 최대 규모의 네트워크
  - 전 세계의 컴퓨터를 서로 연결하여 정보를 교환할 수 있도록 만든 하나의 거대한 컴퓨터 통신망이다.
  
  | 이름 | 프로토콜 | 포트 | 기능 |
  |---|:---:|---:|---:|
  | `WWW` | HTTP | 80 | 웹서비|
  | `Email` | SMTP/POP3/IMAP | 25/110/114 | 이메일 서비스|
  | `FTP` | FTP |21 |파일 전송 서비스|
  | `DNS` | TCP/UDP | 53 |네임 서비스|
  | `NEWS` | NNTP | 119 |인터넷 뉴스 서비스|
  
- ISP(Internet Service Provider)
  - 인터넷에 접속하는 수단을 제공하는 주체다. 일반 사용자, 기업체, 기관, 단체 등이 인터넷에 접속하여 인터넷을 이용할 수 있도록 돕는 사업자이다. (KT, U+ )
- DNS(Domain Name System)
  - url을 ip주소로 변환하는 서비스(시스템)

## LAN과 WAN
- LAN (Local Area Network : 근거리 통신망)
  - 비교적 가까운 거리의 집, 사무실 등 가까운 지역을 연결하는 네트워크이다.
  - 속도가 빠르며 오류 발생 확률이 낮다
- WAN (Wide Area Network : 원거리 통신)
  - 랜을 다시 하나로 묶는 거대한 네트워크이다. 도시, 국가와 같이 넓은 범위
  - 전기 통신 사업자가 제공하는 서비스를 사용하며 구축된 속도가 느리고 오류가 발생하기 쉽다
 
## 기업의 네트워크
- 기업의 서버는 온프레미즈나 클라우드 중 하나로 운영되고 있다.
  - 온프레미즈(on-premise)
    - 사내 서버 또는 데이터센터
  - 클라우드
- DMZ(DeMilitarized Zone)
  - 공개 서버
  - 네트워크 구성 중에서 일반적으로 인터넷인 외부 네트워크와 내부 네트워크 사이에 위치한 중간 지대(서브넷)
  - 네트워크의 보안 영역으로 외부 공격자가 내부 네트워크에 침투하는 것을 막는 역할을 한다.
- VPN(Virtual Private Network)
  - 가상 사설망
  - 가상 통신 터널을 만들어 기업 본사나 지사와 같은 거점 간을 연결하여 통신하거나 외부에서 인터넷으로 사내에 접속하는 것을 말한다.

# OSI 7계층
국제표준화기구 ISO가 네트워크의 기본 구조를 일곱 개의 계층으로 나눠서 표준화한 통신 규약
### 왜 분류하였을까?
단계별로 파악하면 이해하기도 쉽고, 특정부분에 이상이 있을 경우 다른 단계를 건드리지 않고 고칠 수 있음

- 7 Layer - Application Layer
  - 응용 프로세스와 직접 관계하여 응용 서비스 수
  - 최종 목적지로 HTTP, FTP, SMTP, POP3, IMAP, Telnet 등과 같은 프로토콜이 있다.
- 6 Layer - Presentation Layer
  - 데이터 표현이 상이한 응용프로세스의 독립성 제공, 암호화
- 5 Layer - Session Layer
  - 데이터가 통신하기 위한 논리적인 연결
  - 양 끝단의 응용 프로세스가 통신을 관리하기 위한 방법 제공
- 4 Layer - Transport Layer
  - TCP 또는 UDP 프로토콜 이용해 포트 열기
  - 패킷생성 및 전송
- 3 Layer - Network Layer
  - 경로를 선택하고 주소(IP)를 정하여 경로에 따라 패킷을 전달해주는 역할
  - 라우터
- 2 Layer - Data Link Layer
  - 브릿지나 스위치를 통해 맥 주소를 가지고 물리계층에서 받은 정보 전달
  - 에러검출/재전송/흐름제어
- 1 Layer - Physical Layer
  - 통신 케이블에 비트 단위의 데이터 전송
  - 통신 케이블, 리피터, 허브

# TCP/IP 모델 4계층 (= 인터넷 모델)
- Application
- Transport
- Internet
- Network Interface

## 출처
- [OSI 7 계층이란?, OSI 7 계층을 나눈 이유](https://shlee0882.tistory.com/110)


