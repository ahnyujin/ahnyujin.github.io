---
title: 자바 버전별 특징
author: Yujin Ahn
date: 2020-09-15 21:00:00 +0900
categories: [Study, Java]
tags: [java]     # TAG names should always be lowercase
---
# JAVA 7
1. **Type Interface (타입 추론)**
    - 제너릭에서 사용되는 <>오퍼레이터 지원 // 컴파일러가 타입을 추출한다
    ```java
   ArrayList<Integer> arr = new ArrayList<>();
    ```
2. **Switch문 문자열 case 사용가능**
3. Automatic Resource Management
4. Catching Multiple Exception Type in Single Catch Block
    - 멀티 캐치 가능
    
# JAVA 8
1. **Lambda**
2. **interface 클래스에 구현체 작성 가능**
3. **Optional**
    - null이 될수도 있는 객체를 감싸는 일종의 래퍼 클래스
4. **다양한 DateTime 추가**
5. **GC 성능 대폭 개선**
    - 메모리 누수를 일으켰던 Permanent Generation 영역을 제거하여 static인스턴스와 리터럴 문자열도 GC대상이 되도록 하였다.
    - Metaspace로 변경되었다.

# JAVA 9
1. **인터페이스 내에 private 메소드 가능**
2. **모듈 시스템 등장(jigsaw)**

# JAVA 10
Local Variable Type Interface -> var사용
var 키워드를 이용한 지역변수 선언 및 타입추론 가능
JVM heap 영역을 NVDIMM(비휘발성 NAND 플래시 메모리) 혹은 사용자 지정과 같은 대체 메모리 장치에 할당 가능

# JAVA 11
1. lambda 파라미터에 대한 지역변수 문법
2. 앱실론 가비지 컬렉터 추가
    - 할당을 처리하지만 메모리를 회수하지 않는다. 힙이 소진되면 JVM이 종료된다.
    - 수명이 짧은 서비스와 가비지를 사용하지 않는 애플리케이션에 유용
3. HTTP 클라이언트 표준화
    - 자바9에 도입되었던 HTTP Client API를 표준화
    - HTTP Client API는 비동기 방식으로 작동하고, http2 프로토콜을 지원한다


# 출처
- [Java 버전별 특징](https://ggomi.github.io/jdk-version/)
- [Java 11로 전환해야 하는 이유](https://docs.microsoft.com/ko-kr/azure/developer/java/fundamentals/reasons-to-move-to-java-11)