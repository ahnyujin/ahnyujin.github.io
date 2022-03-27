---
title: Spring IoC, AOP, PSA
author: Yujin Ahn
date: 2022-03-25 01:21:00 +0900
categories: [Blogging, Demo]
tags: [spring]
---

# Spring

자바 엔터프라이즈 개발을 위한 오픈소스 애플리케이션 프레임워크

목적 : POJO를 이용한 애플리케이션 개발로 엔터프라이즈 시스템을 쉽고 효과적으로 개발하자

## POJO(Plain Old Java Object)

순수한 자바 오브젝트

과거 EJB가 인기일때 단순한 자바 오브젝트를 사용하지 않고 EJB에 종속적인 개발을 해왔다. 그러다 보니 모듈을 교체하거나, 시스템을 업그레이드할 때 종속성으로 인한 문제들이 생겨났다. 이러한 문제를 해결하기 위해 단순한 오브젝트를 이용해 애플리케이션의 비즈니스 로직을 구현하는 것이 POJO 프로그래밍이다.

특징
1. 특정 규약에 종속되지 않는다.
   - 특정 라이브러리, 모듈에서 정의된 클래스를 상속받아 구현하지 않는다

2. 특정 환경에 종속되지 않는다.
   - 외부 종속적인 http request, session등을 사용하지 않는다

스프링은 주요 기술인 IoC/DI, AOP, PSA을 통해 POJO방식으로의 프로그래밍을 지원한다. IoC/DI, AOP, PSA를 POJO로 개발할 수 있게 해주는 가능기술이라고 부르기도 한다.

# IoC/DI Container

## IoC Container

1. 객체가 자신의 dependency를 정의
    1. constructor
    2. setter
    3. field
2. 이후 IoC 컨테이너는 빈을 생성할때 dependency를 주입한다. (Object Reference를 주입)

객체가 타 객체와 관계를 맺는 작업의 제어권을 IoC 컨테이너에 넘겼으므로 제어의 역전이라고 부른다.

이제 객체는 자신이 사용할 대상의 생성이나 선택에 관한 책임을 벗어나 구현에만 집중할 수 있게 되었다.

## ApplicationContext

BeanFactory는 빈을 관리하는 기능을 담당한다.

ApplicationContext는 BeanFactory를 확장해 더 많은 엔터프라이즈 기능을 추가로 제공한다. 

org.springframework.context.ApplicationContext 인터페이스는 Spring IoC container를 나타내고 빈을 인스턴스화(instantiate)하고, 설정(configure)하고 구성(assemble)하는 역할을 한다.

![Untitled](https://docs.spring.io/spring-framework/docs/current/reference/html/images/container-magic.png)

애플리케이션 class들은 ApplicationContext가 configuration metadata를 이용해 IoC를 적용한 후 실행 가능한 시스템이 된다.

# AOP(Aspect Oriented Programming)

교차 관심사의 분리로 모듈성을 높이는 것을 목표로 하는 프로그래밍 패러다임

대부분의 프로젝트에서는 로깅, 인증, 인가 등 도메인 로직과 관계없는 기능들이 중복된다.

이러한 공통 기능들을 매번 똑같이 개발하고 유지보수 하지 않게(DRY : Don’t repeat yourself) 분리하여 개발하고 실행시에 스프링이 대신 조합할 수 있다. 

# PSA(Portable Service Abstraction)

POJO로 개발한 코드가 특정 환경과 기술에 종속되지 않고 일관된 방식으로 기술에 접근할 수 있게 해주는 서비스 추상화 기술