---
title: (Spring) WebFlux
author: Yujin Ahn
date: 2020-11-03 17:00:00 +0900
categories: [Languages&Frameworks, Spring]
tags: [spring]     # TAG names should always be lowercase
---

# Spring Framework 5 특징
- JDK8부터 지원
- 코틀린 지원
- Reactive Programming Model
- JUnit 5 Jupiter
- 호환되는 라이브러리 업데이트 ex) JDBC 4.0, Hibernate 5

# 리액티브 프로그래밍
## Reactive Programming이란?
어떤 이벤트에 대해 최대한 빠른 시간 내에 응답하는 것이다.

비동기 프로토콜을 기반으로 적은 수의 쓰레드로 확장성있는 논블로킹, 이벤트 드리븐 개발

특징
- 응답성(responsible) - 시스템에 가능한 한 즉각적으로 응답
- 탄력성(resilient) - 시스템의 장애에 직면해도 응답성을 잃지 않는것 // 장애가 전파되지 않도록 함
- 유연성(Elastic) - 시스템의 작업량이 변화하더라도 응답성을 유지하는 것
- 메시지 기반(Message Driven) - 비동기 프로토콜을 기반으로 작은 수의 쓰레드로 확장성있는 논블로킹 / Event-driven개발

## BackPressure
동기 방식, 명령형 코드, 블로킹 호출은 요청자를 대기 상태로 두어 자연스럽게 BackPressure 형태를 취한다.
논블로킹 코드에서는 빠른 producer 가 destination 를 압도하지 않도록 하기 위해 이벤트의 속도를 제어하는 것이 중요하다.

## 리액티브 스트림
리액티브 스트림은 백프레셔를 통해 비동기 컴포넌트들 사이의 비동기적 상호 작용을 정의한다.
예를 들어, 데이터 저장소(Publisher 역할)는 HTTP 서버(Subscriber 역할)가 응답에 쓰기 위한 위한 데이터를 생성한다.
리액티브 스트림의 목적은 Subscriber가 Publisher의 데이터의 생성 속도를 제어할 수 있게 하는 것이다.

Publisher 를 늦출 수 없다면?
- 버퍼 사용, 드랍 또는 실패 등을 결정해야 한다.

# Spring Webflux
스프링 웹플럭스는 스프링5에서 추가된 리액티브 스택 웹 프레임워크이다.

기존 스프링 프레임워크의 오리지널 웹 프레임워크인 스프링 웹 MVC는 Servlet API와 Servlet Container를 위한 것이었다.

스프링웹플럭스는 완전한 논블로킹으로, Reactive Streams backpressure를 지원하며, Netty, Undertow, and Servlet 3.1+ containers 등의 서버에서 구동된다.

## Why Spring Webflux?
- 사실 Servlet 3.1 에서 이미 non-blocking I/O를 다루기 위한 API를 제공한다.
- 그러나 이 API를 사용하면 다른 나머지 서블릿 API와는 멀어지게 된다(필터, 서블릿과 같은 동기방식 처리나 getParameter, getPart 등 블로킹 API).
- 이런 점이 어떠한 논블로킹 런타임에서든 기반 역할로 지원하는 새로운 공통 API의 탄생 동기가 되었다.
- Netty와 같이 비동기 논블로킹 영역이 잘 구현된 서버로 인해 이 점은 중요하다.

Webflux의 특성
1. 적은 리소스로 많은 트래픽을 감당
2. 함수형 프로그래밍

## 1. 적은 리소스로 많은 트래픽을 감당
기존 스프링 mvc는 스레드 풀 방식을 사용하고 있다.(one request per thread model)
클라이언트의 요청들을 큐를 통해 받게 되고 thread pool size만큼의 요청까지만 동시에 작업할 수 있다. 즉, 하나의 요청이 하나의 스레드를 필요로 한다. 그러므로 대량의 트래픽이 들어올 경우 큐에서 대기해야 하기 때문에 전체 대기 시간이 늘어나는 문제가 발생한다. 이러한 현상을 Thread pool hell이라고 한다.

어떻게 효율을 높일 수 있을까?
- I/O 작업은 CPU가 관여하지 않는다. I/O Controller가 데이터를 읽어오고 이를 전달받을 뿐.
- 따라서 I/O를 처리하는 방식을 **비동기 논블로킹 방식**으로 바꾼다.(Spring의 WebFlux)

스프링 WebFlux는 클라이언트의 요청을 싱글스레드 이벤트루프를 통해서 작업을 처리한다.

이렇듯 Non Blocking 방식을 활용하면 좀 더 효율적으로 I/O를 제어할 수 있고 성능에도 좋은 영향을 미친다. 특히나 서비스간 호출이 많은 마이크로서비스 아키텍처에 적합

### 주의해야할 점
WebFlux로 성능을 최대치로 끌어올리려면 모든 I/O 작업이 논블로킹 기반으로 동작해야 된다.

## 2. 함수형 프로그래밍
순수함수를 조합하여 프로그래밍하는 방식

1. 불변성
2. first-class function
3. 지연연산

(!작성중!)

출처
- [docs.spring.io/spring-framework](https://docs.spring.io/spring-framework/docs/current/reference/html/web-reactive.html)
- [ㄴ 번역 스프링 웹플럭스 레퍼런스 (Web on Reactive Stack)](https://parkcheolu.tistory.com/134)
- [Spring WebFlux는 어떻게 적은 리소스로 많은 트래픽을 감당할까?](https://devahea.github.io/2019/04/21/Spring-WebFlux%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%A0%81%EC%9D%80-%EB%A6%AC%EC%86%8C%EC%8A%A4%EB%A1%9C-%EB%A7%8E%EC%9D%80-%ED%8A%B8%EB%9E%98%ED%94%BD%EC%9D%84-%EA%B0%90%EB%8B%B9%ED%95%A0%EA%B9%8C/)