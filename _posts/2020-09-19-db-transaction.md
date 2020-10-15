---
title: DB Transaction
author: Yujin Ahn
date: 2020-09-19 22:56:00 +0900
categories: [CS, Database]
tags: [db]     # TAG names should always be lowercase
---
# DB Transaction
트랜잭션이란? 
- 데이터베이스의 상태를 변화시키기위해 수행하는 **논리적인 작업 단위**

왜 필요한가?
- 시스템 상 혹은 사용자의 실수가 있더라도 DB 데이터를 안정적으로 보장하기 위함

## 하나의 트랜잭션은 Commit 되거나 Rollback 된다.
Commit
- 트랜잭션이 성공적으로 끝났고, DB가 다시 일관성있는 상태일 때 이 트랜잭션이 행한 갱신 연산이 완료되었음을 알려주기 위해 사용하는 연산
Rollback
- 트랜잭션 처리가 비정상적으로 종료되어 트랜잭션 원자성이 깨진 경우 이 트랜잭션이 행한 모든 연산을 취소(Undo)시키는 연산
- last consistent state로 rollback 할 수 있음

## 트랜잭션이 안전하게 수행된다는 것을 보장하기 위한 특징 __A.C.I.D__
- 원자성(Atomicity) - All or Nothing
  - 트랜잭션이 DB에 모두 반영되거나, 전혀 반영되지 않아야 한다.
- 일관성(Consistency)
  - 트랜잭션의 작업결과는 항상 일관성 있어야 한다.
  - 즉, 미리 정의된 무결성 제약조건을 위반하면 트랜잭션은 중단된다.
- 독립성(Isolation)
  - 둘 이상의 트랜잭션이 동시에 수행되고있을때, 어떤 트랜잭션도 다른 트랜잭션 연산에 끼어들 수 없다.
  - 원칙상으로는 독립적이어야 하나, 유연하게 수정 가능하다. //isolation level!!
- 지속성(Durability)
  - 트랜잭션이 성공적으로 완료되었으면, 결과는 영구적으로 반영되어야한다.
  
## 트랜잭션 격리수준 
 Isolation Level
- 트랜잭션에서 일관성 없는 데이터를 허용하는 수준
- 트랜잭션간의 침범을 막기 위해, 즉 트랜잭션의 **독립성**을 위해 Locking을 한다.
- 무조건 Locking으로 동시에 수행되는 수많은 트랜잭션들을 순서대로 처리하는 방식으로 구현하게 되면 데이터베이스의 성능은 떨어짐 (무결성 up, 동시성 down)
- 그렇다고 해서, 성능을 높이기 위해 Locking의 범위를 줄인다면, 잘못된 값이 처리될 문제가 발생 (동시성 up, 무결성 down)
- 따라서 효율적인 Locking이 필요하다,

### Isolation level 종류
ANSI/ISO SQL Standard에서 정의함

레벨 낮을수록, 동시성 up & 데이터 무결성 문제 많아진다.
1. Read Uncommitted (레벨 0)
2. Read Committed (레벨 1)
3. Repeatable Read (레벨 2)
4. Serializable (레벨 3)
레벨 높을수록, 데이터 무결성 up & 동시성 처리 안되어서 비용 up!

#### LV_0 : READ UNCOMMITTED
COMMIT전의 트랜잭션의 데이터 변경 내용을 다른 트랜잭션이 읽는 것을 허용

#### LV_1 : READ COMMITTED
COMMIT이 완료된 데이터만 다른 트랜잭션에서 조회 가능
- how? 트랜잭션이 시작되기 전에 커밋된 내용(SNAP SHOT)을 조회함
- 특정 시점을 기준으로 snapshot을 읽어오는 것을 Consistent Read라고 함

#### LV_2 : REPEATABLE READ
트랜잭션 범위 내에서 조회한 내용이 항상 동일함을 보장
- how? 처음으로 read(SELECT)operation을 수행한 시간을 기록하여 이후 read operation마다 해당 시점을 기준으로 consisten read를 수행한다.

#### LV_3 : SERIALIZABLE
한 트랜잭션에서 사용하는 데이터를 다른 트랜잭션에서 접근 불가
모든 작업을 하나의 트랜젝션에서 처리하는것과 같은 가장 높은 고립수준을 제공한다.

  |  | Dirty Read | Non-Repeatable Read | Phantom Read |
  |---|:---:|---:|---:|
  | READ_UNCOMMITTED | O | O | O |
  | READ_COMMITTED | X | O | O |
  | REPEATABLE_READ | X | X | O |
  | SERIALIZABLE | X | X | X |
  
# Dirty Read
커밋되지 않은 데이터를 읽는 현상
# Non-Repeatable Read
한 트랜잭션 내에서 같은 쿼리를 두 번 수행했는데, 그 사이에 다른 트랜잭션이 값을 수정 또는 삭제하는 바람에 두 쿼리 결과가 다르게 나타나는 현상
# Phantom Read
한 트랜잭션 내에서 같은 쿼리를 두 번 수행했는데, 첫 번째 쿼리에서 없던 유령(Phantom) 레코드가 두 번째 쿼리에서 나타나는 현상

# 트랜잭션 전파타입
트랜잭션이 시작하거나 참여하는 방법에 대한 설정
Spring에서의 7가지 전파타입

  | 진행중인 트랜잭션 | 있을 때 | 없을 때 |
  |---|:---:|---:|
  | REQUIRED | 해당 트랜잭션 사용 | 새로운 트랜잭션 생성 |
  | MANDATORY | 해당 트랜잭션 사용 | 예외 발생 |
  | REQUIRES_NEW | 해당 트랜잭션 보류, 새로운 트랜잭션 생성 | 새로운 트랜잭션 생성 |
  | SUPPORTS | 해당 트랜잭션 사용 | 트랜잭션 없이 진행 |
  | NON_SUPPORTS | 해당 트랜잭션 보류 | 트랜잭션 없이 진행 |
  | NEVER | 예외 발생 | 트랜잭션 없이 진행 |
  | NESTED | 중첩 트랜잭션 생성 | 새로운 트랜잭션 생성 |
  
# 출처
- [DBMS는 어떻게 트랜잭션을 관리할까?](https://d2.naver.com/helloworld/407507)
- [Lock으로 이해하는 Transaction의 Isolation Level](https://suhwan.dev/2019/06/09/transaction-isolation-level-and-lock/)
- [트랜잭션 격리 수준(isolation level)](https://joont92.github.io/db/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B2%A9%EB%A6%AC-%EC%88%98%EC%A4%80-isolation-level/)
- [Transaction Isolation Level](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction%20Isolation%20Level.md)