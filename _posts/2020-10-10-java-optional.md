---
title: (Java) Optional
author: Yujin Ahn
date: 2020-10-10 17:00:00 +0900
categories: [Languages&Frameworks, Java]
tags: [java]     # TAG names should always be lowercase
---
Optional<T>은 지네릭 클래스로 'T타입의 객체'를 감싸는 [래퍼클래스](https://ahnyujin.github.io/posts/java-wrapper-class) 다.
따라서 모든 타입의 참조변수를 담을 수 있다.

정의된 메소드를 통해 반환된 결과가 null인지 간단하게 처리할 수 있다.

```java
Optional<String> optVal = Optional.of(null); //NullPointerException발생
Optional<String> optVal = Optional.ofNullable(null); //OK
```
