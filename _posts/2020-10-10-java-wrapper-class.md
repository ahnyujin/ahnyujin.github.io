---
title: (Java) Wrapper Class
author: Yujin Ahn
date: 2020-10-10 17:00:00 +0900
categories: [Languages&Frameworks, Java]
tags: [java]     # TAG names should always be lowercase
---
# 래퍼(wrapper) 클래스
**기본형 객체도 어쩔 수 없이 객체로 다루어야 하는 때**도 있다.
- 매개변수로 객체를 요구할 떄,
- 기본형 값이 아닌 객체로 저장해야 할 때,
- 객체간의 비교가 필요할 때

이때 사용되는 것이 래퍼 클래스.

래퍼 클래스는 객체 생성시에 생성자의 인자로 주어진 각 자료형에 알맞은 값을 내부적으로 저장하고 있으며, 이에 관련된 여러 메서드들이 정의되어 있다.

래퍼클래스는 모두 equals()가 오버라이딩되어 있어서 값을 비교할 수 있다.

### 래퍼클래스의 상속도
```
Object-+-Boolean
       |
       +-Character
       |
       +-Number----+-Byte, Short, Integer, Long, Float, Double, BigInteger, BigDecimal
```

### 문자열을 숫자로 반환하기
- 기본형으로 변환
    - 타입.parse타입(String s) //ex) int i = Integer.parseInt("100");
    - 대체로 많이 사용하며 비교적 빠르다.
- 래퍼클래스로 변환
    - 타입.valueOf() // ex) Integer i = Integer.valueOf("100");
    
## 오토박싱 & 언박싱
컴파일러가 자동으로 형변환 코드를 추가해주어 기본형과 참조형 간의 연산을 가능하게 함

오토박싱(autobosing)
- 기본형 값을 래퍼클래스 객체로 자동 변환해주는 것

언박싱(unboxing)
- 래퍼클래스 기본형로 자동 변환해주는 것

```java
ArrayList<Integer> list = new ArrayList<Integer>();
list.add(10);   //오토박싱
int value = list.get(0); //언박싱
```