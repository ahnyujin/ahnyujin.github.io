---
title: Load Balancing
author: Yujin Ahn
date: 2020-09-20 20:59:00 +0900
categories: [Study, CS]
tags: [network]     # TAG names should always be lowercase
---
로드밸런싱 (Load Balancing)
둘 이상의 CPU or 저장장치와 같은 컴퓨터자원들에게 작업을 나눠주는 것

Scale-up
- 서버의 사양을 올린다
- 인스턴스를 업데이트 하는동안 서비스할 수 없다
Scale-out
- 서버 개수 늘린다
- 새로운 도메인 필요

로드 밸런서가 서버를 선택하는 방식
- 라운드 로빈 (Round Robin) - CPU 스케줄링의 라운드 로빈 방식 활용
- Least Connections - 연결 개수가 가장 적은 서버 선택 (특정 사용자가 항상 같은 서버로 연결되는 것을 보장)
- Source - **사용자 IP를 해싱**하여 분배 (특정 사용자가 항상 같은 서버로 연결되는 것 보장)

로드밸런서 장애 대비
서버를 분배하는 로드밸런서에 문제가 생길 수 있기 때문에 로드밸런서를 이중화하여 대비
- Active 상태 Passive상태

# 출처
- [로드밸런서(Load Balancer)의 개념과 특징](https://post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903)
- [로드 밸런싱(Load Balancing)](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/%EB%A1%9C%EB%93%9C%20%EB%B0%B8%EB%9F%B0%EC%8B%B1(Load%20Balancing).md)