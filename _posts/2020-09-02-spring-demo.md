---
title: Spring Demo
author: Yujin Ahn
date: 2020-09-02 00:00:00 +0900
categories: [Study, Spring]
tags: [spring]     # TAG names should always be lowercase
---

## Basic of Spring
스프링이란? 자바 엔터프라이즈 개발을 위한 오픈소스 애플리케이션 프레임워크
애플리케이션 프레임워크란? 애플리케이션의 바탕이 되는 틀과 공통 프로그래밍 모델, 기술 API 등을 제공해준다.

- 스프링 컨테이너(애플리케이션 컨텍스트)라 불리는 스프링 런타임 엔진을 제공한다.
    - 역할 : 애플리케이션 오브젝트의 생성과 관리
- 핵심 프로그래밍 모델
    1. IoC/DI  //오브젝트의 생명주기, 의존관계에 대한 프로그래밍 모델
    2. 서비스 추상화 //특정 기술에 종속되지 않고 이식성이 뛰어난 애플리케이션 만들자
    3. AOP // 부가적인 기능을 독립적으로 모듈화하는 프로그래밍 모델
- 방대한 기술 API 제공

스프링은 자바의 기본인 객체지향에 충실하자는 모토
스프링에서 애플리케이션에서 오브젝트가 생성되고 오브젝트간 관계를 맺고, 사용되고, 소멸되기까지의 전 과정을 살펴보자.
DAO(Data Access Obejct) DB의 데이터를 조작하는 기능을 담당하는 오브젝트

자바빈이란?
# 제어의 역전 (IoC)
# 의존관계 주입 (DI)
스프링 IoC의 대표적인 동작 원
bean scope

singleton

request

session

# AOP
# Transaction