---
title: 스레드와 락 - (1) 프로세스와 스레드
author: Yujin Ahn
date: 2020-09-02 16:05:00 +0900
categories: [Study, CS]
tags: [os]     # TAG names should always be lowercase
---
# 프로세스와 스레드의 차이

**프로그램은** "디스크에 저장되어 있는 실행가능한 명령어의 집합"

**프로세스**는 "실행중인 프로그램". 디스크로부터 메모리에 적재(load)되어 cpu할당을 받을 수 있는 것. (작업, 또는 Task라고도 한다. 프로그램의 인스턴스)

**스레드**는 "하나의 프로세스 내에서 제어 흐름을 갖는 단위"

## 프로세스

프로세스가 할당받는 시스템 자원

- CPU시간
- 주소 공간
- 독립된 메모리 영역 (Code, Data, Heap, Stack 구조)

특징

- 한 프로세스가 다른 프로세스의 자원에 접근하려면 프로세스 간의 통신(IPC)을 사용해야 한다.
    - Ex. 파이프, 파일, 소켓 등을 이용한 통신 방법

운영체제는 프로세스를 관리하기 위해 프로세스에 관한 모든 정보를 가지고 있는데, 이를 PCB(Process Control Block)라고 한다.

(Code, Data, Heap, Stack) 구조

- Code - 프로그램의 실제 코드 

- Data - 프로세스가 실행 될 때 정의된 전역변수와 Static 변수

- Heap - 프로세스 런타임 중 동적으로 할당되는 변수들을 저장(ex, 함수내에서 할당되는 변수)

- Stack - 함수에서 다른 함수를 실행하는 등의 서브루틴들의 정보를 저장(재귀와 스택이 관련 있는 경우)

## 스레드

스레드는

- thread ID, pc(program counter), registers
- 프로세스로부터 할당받은 Stack

으로 구성되어 있다.

특징

- Code, Data, Heap영역을 공유해 같은 프로세스 내의 스레드들은 프로세스 내의 주소공간과 자원들을 공유한다.
- 한 스레드가 공유자원을 변경하면, 프로세스 내 다른 스레드들에게 즉시 공유된다.

왜 스레드마다 스택을 독립적으로 할당하는지?

- 지역변수와 되돌아갈 주소값을 추적하기 위해!

왜 스레드마다 PC, register를 독립적으로 할당하는지?

- 스레드가 명령어를 어디까지 수행했고, 어떠한 상태로 종료하였는지 알기 위해!

## 멀티 프로세스와 멀티 스레드의 차이

멀티 프로세스 - 하나의 컴퓨터에 여러 CPU를 장착해 하나 이상의 프로세스를 병렬적으로 처리하는것

멀티스레드 - 하나의 프로세스를 다수의 실행 단위로 구분하여 자원을 공유하고 자원의 생성과 관리의 중복성을 최소화하여 수행 능력을 향상시키는 것.

### 멀티스레드의

장점

- 독립적인 프로세스에 비해 공유메모리만큼의 시간, 자원 손실이 감소.
- 컨텍스트 스위치가 프로세스보다 빠르다.  (프로세스는 Context를 PCB에 저장해야함.) → 시스템 처리량 증가
    - 컨텍스트 스위치란? CPU가 현재 작업을 멈추고 다른 작업을 하는것.
- 다른 스레드들과 데이터 공유도 편하다. (프로세스는 IPC)

단점

- 공유 자원을 사용하며 동기화 문제에 신경써야한다.
- 하나의 스레드에 문제가 발생하면 전체 프로세스가 영향을 받는다. (반면 멀티프로세스는 자식프로세스가 죽는다고 영향이 확산되는것은 아님)
- 디버깅이 어렵다.

## Thread-Safe란 무엇인가?

- 멀티 스레드 환경에서 여러 스레드가 하나의 객체 및 변수(공유 자원)에 접근할 때, 의도한대로 동작하는 것을 말한다.

어떻게 하면 Thread-Safe하게 구현할 수 있을까?

- 공유자원에 접근하는 임계영역(critical section)을 동기화하는 기법으로 제어해줘야 한다. = 상호배제
- 동기화방법으로는 Mutex Semaphore
- Reetrant함을 보장.
    - Reetrant는 재진입성이라는 의미로 어떤 함수가 Reetrant하다는 것은 여러 스레드가 동시에 접근해도 언제나 같은 실행 결과를 보장한다는 의미이다.
    - 이를 만족하기 위해서 해당 서브루틴에서 공유자원을 사용하지 않으면 된다.
    - 따라서, Reetrant하다면 Thread-safe하지만 그 역은 성립하지 않는다.

## 자바의 스레드

독립적인 응용 프로그램이 실행될 때, main() 메서드를 실행하기 위해 메인 스레드가 자동으로 만들어진다.

자바의 스레드 구현 방법

- java.lang.Runnable 인터페이스를 구현하기
- java.lang.Thread 클래스를 상속받기

.

//추가하기

.

.


다음시간에는 동기화와 락에 대해서 알아보아요 ;-)

출처
[https://docs.oracle.com/javase/tutorial/essential/concurrency/procthread.html](https://docs.oracle.com/javase/tutorial/essential/concurrency/procthread.html)
[https://shoark7.github.io/programming/knowledge/difference-between-process-and-thread](https://shoark7.github.io/programming/knowledge/difference-between-process-and-thread)