---
title: 자바 버전별 특징
author: Yujin Ahn
date: 2020-09-15 21:00:00 +0900
categories: [Study, Java]
tags: [java]     # TAG names should always be lowercase
---
# JAVA 7
1. Type Interface (타입 추론)
    - 제너릭에서 사용되는 <>오퍼레이터 지원
2. Switch문 문자열 case 사용가능
3. Automatic Resource Management
4. Catching Multiple Exception Type in Single Catch Block
    - 멀티 캐치 가능
# JAVA 8
1. Lambda
2. interface 클래스에 구현체 작성 가능
3. Optional
    - null이 될 수도 있는 객체를 감싸는 일종의 래퍼 클래스
4. 다양한 DateTime 추가
5. GC 성능 대폭 개선
# JAVA 9
1. 인터페이스 내에 private 구현체 가능
2. 모듈 시스템 등장(jigsaw)
# JAVA 10
Local Variable Type Interface -> var사용
JVM heap 영역을 NVDIMM 혹은 사용자 지정과 같은 대체 메모리 장치에 할당 가능

# 출처
- [Java 버전별 특징](https://ggomi.github.io/jdk-version/)