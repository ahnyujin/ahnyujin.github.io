---
title: (Java) Collection
author: Yujin Ahn
date: 2020-10-07 17:00:00 +0900
categories: [Languages&Frameworks, Java]
tags: [java]     # TAG names should always be lowercase
---

# 자바 컬렉션 프레임워크(Collection Framework)
컬렉션 객체는 여러 원소들을 담울 수 있는 자료구조
자바 컬렉션 프레임워크는 이러한 데이터, 자료구조인 컬렉션과 이를 구현하는 클래스를 정의하는 인터페이스를 제공한다.

컬렉션 인터페이스는 List, Set, Queue로 크게 3가지 상위 인터페이스로 분류하고 있다.
Map의 경우 Collection 인터페이스를 상속받고 있지 않지만 Collection으로 분류된다.

# Collection 인터페이스의 특징
  | 인터페이스 | 구현클래스 | 특징 |
  |---|:---:|---:|
  | Set | HashSet, TreeSet | 순서를 유지하지 않는 데이터의 집합으로, 데이터의 중복 허용x |
  | List | Vector, ArrayList, LinkedList | 순서가 있는 데이터의 집합으로, 데이터의 중복 허용o |
  | Queue | LinkedList, PriorityQueue | List와 유사 |
  | Map | Hashtable, HashMap, TreeMap | 키,값 쌍으로 이루어진 데이터 집합으로, 순서는 유지되지 않으며 key중복 허용x, (값 중복은 허용o) |

배열과의 차이점은 정적 메모리 할당이 아닌 동적 메모리 할당을 하게된다.
# List인터페이스
> 중복을 허용하면서 저장순서가 유지되는 컬렉션을 구현하는데 사용된다.

Vector
- 과거에 대용량처리를 위해 사용했으며, 내부에서 자동으로 동기화처리가 일어나 성능이 좋지않아 잘 사용하지 않음.
ArrayList
- 기존의 Vector를 개선한 것으로 Vector와 구현원리와 기능적 측면에서 동일하다.
LinkedList
- 양방향 포인터 구조로 데이터의 삽입, 삭제가 빈번할 경우 데이터의 위치정보만 수정하면 되기에 유용하다.
- 스택, 큐, 양방향 큐 등을 만들기 위한 용도로 쓰인다.

## +) 배열과 연결리스트
배열
- 장점: 구조가 간단하며 데이터를 읽어오는데 걸리는 시간이 빠르다.
- 단점: 크기를 변경할 수 없고, 비순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸린다는 것.
연결리스트(linked list)
- 불연속적인 데이터를 서로 연결한 형태로 구성한다.
- 장점: 중간 데이터를 추가, 삭제하는것이 배열보다 빠르다. 재배치에 시간이 적게 든다.
- 단점: 인덱스를 가지고 있는 배열과 달리 한번에 데이터 접근이 가능하지 않다.

## +) ArrayList는 thread safe하지 않고, Vector는 Thread safe하다.
# Map 인터페이스
> 키, 값의 쌍으로 이루어진 데이터 집합으로, 순서는 유지되지 않으며 키의 중복은 허용하나 값의 중복은 허용하지않는다.

Hashtable
- HashMap보다 느리지만 동기화 지원
- null불가
HashMap
- 중복과 순서가 허용되지 않으며 null값이 올 수 있다.
TreeMap
- 정렬된 순서대로 키와 값을 저장하여 검색이 빠름

# Set인터페이스
> 순서를 유지하지 않는 데이터의 집합으로 데이터의 중복을 허용하지 않는다.

HashSet
- 가장 빠른 임의 접근 속도
- 순서를 예측할 수 없음
TreeSet
- 정렬방법을 지정할 수 있음

# 출처
- [Java 컬렉션](https://gangnam-americano.tistory.com/41)
- [Java에서 Collection 이란?](https://www.crocus.co.kr/1553)
- 자바의 정석