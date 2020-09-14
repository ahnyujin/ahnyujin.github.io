---
title: 브라우저의 동작방법
author: Yujin Ahn
date: 2020-09-14 19:00:00 +0900
categories: [Study, CS]
tags: [web]     # TAG names should always be lowercase
---

# 브라우저 동작방법

```
사용자 인터페이스 → 브라우저 엔진 → 렌더링 엔진 → 통신 || UI 백엔드 || 자료 저장
               ㄴ데이터저장소
```
- 사용자 인터페이스
  - 주소 표시줄, 북마크 등 사용자가 활용하는 서비스들// 브라우저 창 제
- 브라우저 엔진
  - 브라우저 SW를 동작시키는 엔진 
  - 소스코드를 실행해서 화면에 보여줌
  - 일부 정보를 캐싱해서 데이터 저장소에 저장
- 렌더링 엔진
  - 화면에 위치를 잡고 색칠을 해주는. 픽셀 단위
  - 크롬, 사파리 : Webkit 엔진 사용
  - 파이어폭스 : Gecko 엔진 사용
- 통신
  - http로 서버와 통신
- UI 백엔드
  - UI영역을 처리할 수 있는 백엔드 영역
- 자바스크립트 해석기
- 자료 저장

렌더링 동작 과정
```
DOM 트리 구축 위한 HTML파싱 → 렌더트리구축 → 렌더트리배치 → 렌터트리그리기
```
Simple Main flow
```
( html → DOM Tree + css → Style Rules ) → 렌더트리 → 화면에 표현
```
DOM이란?
- Document Object Model(문서 객체 모델)
- 웹 브라우저가 html페이지를 인식하는 방식
- 트리 구조이다.

# 출처
- [NAVER D2, 브라우저는 어떻게 동작하는가?](https://d2.naver.com/helloworld/59361)
- [원문) How Browsers Work](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)