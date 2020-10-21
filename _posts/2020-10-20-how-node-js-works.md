---
title: (Node.js) Node.js 동작 원리
author: Yujin Ahn
date: 2020-10-20 17:00:00 +0900
categories: [Languages&Frameworks, Node.js]
tags: [nodejs]     # TAG names should always be lowercase
---

# Node.js란 무엇인가요?

![upload-image](/assets/img/node-js.png)

JavaScript를 브라우저 밖에서도 실행할 수 있도록 하는 **JavaScript의 런타임**
> 비동기 Event-Driven JavaScript 런타임

Node.js는 구글 V8엔진 + 이벤트 루프 의 결과물.

구글 V8엔진
구글이 크롬의 성능을 극대화하기 위해 직접 구현한 자바스크립트의 엔진.(빠르다)

libuv가 이벤트 루프를 제공한다.

동작방식

Node.js는 이벤트 루프 (메인 스레드)와 k개의 worker 스레드(스레드 풀이라고 한다)가 있다. (worker스레드 default 4개)

이벤트루프는 메인스레드로서 비즈니스 로직을 수행한다. 수행도중 blocking IO가 있으면, 기다리지 않고 작업을 worker 스레드에 던져 준 뒤, 다른 이벤트를 실행한다.

IO operation이 끝나면, 콜백을 이벤트루프에게 콜백으로서 등록된다

이벤트 루프는 여러개의 큐를 사용하는 복잡한 과정!

# 자바스크립트는 어떻게 동작하는가??

![upload-image](/assets/img/js-works.png)

자바스크립트 런타임인 브라우저 동작원리

JS 엔진은 메모리힙과 콜스택으로 구성되어 있다.
```
메모리 힙: 메모리 할당을 담당하는 곳
콜스택: 코드가 호출되면서, 스택으로 쌓이는 곳
```

자바스크립트가 싱글스레드 기반 언어라는 말은 하나의 메인스레드와 하나의 콜스택을 갖고 있기 때문이다.

동시성을 보장하는 비동기, 논블로킹 작업들은 런타임 환경에서 담당한다.
JS의 런타임은 브라우저 혹은 Node.js이 될 수 있다.

1. 먼저 실행 코드들이 호출스택에 쌓인다.

2. 실행 코드중 백그라운드가 필요한 작업은 백그라운드공간으로 이동하고, 순차적으로 호출스택이 진행된다.

3. 백그라운드에서 자체적으로 작업완료된 콜백함수는 태스크큐로 이동하여 대기한다.

4. 호출 스택들이 완료되면 이벤트 루프가 태스크 큐에 있는 콜백을 순서대로 호출스택에 올린다.

5. 호출스택이 완료되면 이벤트루프가 돌면서 태스크 큐에 있는 콜백을 실행시키고,

6. 태스크 큐에 아무것도 없다면, 이벤트가 올때까지 대기한다.

용어정리
- 런타임(runtime) 컴퓨터가 실행되는 동안 프로세스나 프로그램을 위한 소프트웨어 서비스를 제공하는 가상 머신 상태

# 출처
- node.js - [node.js)Don't Block the Event Loop (or the Worker Pool)](https://nodejs.org/ko/docs/guides/dont-block-the-event-loop/)
- [nodejs의 내부 동작 원리 (libuv, 이벤트루프, 워커쓰레드, 비동기)](https://sjh836.tistory.com/149#recentEntries)
- js - [어쨌든 이벤트 루프는 무엇입니까? Philip Roberts  JSConf EU](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
- js - [1. Nodejs 동작원리 및 이벤트 루프, 논블로킹I/O (Event Loop , Non-Blocking)](https://namjackson.tistory.com/30)