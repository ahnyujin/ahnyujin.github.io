---
title: DB Transaction
author: Yujin Ahn
date: 2020-09-19 22:56:00 +0900
categories: [CS, Database]
tags: [db]     # TAG names should always be lowercase
---
# DB Transaction
트랜잭션이란? 
데이터베이스의 상태를 변화시키기위해 수행하는 작업단위

트랜잭션 특징
- 원자성(Atomicity)
  - 트랜잭션이 모두 반영되거나, 전혀 반영되지 않아야 한다.
- 일관성(Consistency)
  - 트랜잭션의 작업결과는 항상 일관성 있어야 한다.
- 독립성(Isolation)
  - 둘 이상의 트랜잭션이 동시에 수행되고있을때, 어떤 트랜잭션도 다른 트랜잭션 연산에 끼어들 수 없다.
- 지속성(Durability)
  - 트랜잭션이 성공적으로 완료되었으면, 결과는 영구적으로 반영되어야한다.
  
Commit
- 트랜잭션이 성공적으로 끝났고, DB가 일관성있는 상태일 때 이를 알려주기 위해 사용하는 연산
Rollback
- 트랜잭션 처리가 비정상적으로 종료되어 트랜잭션 원자성이 깨진 경우.
- last consistent state로 rollback 할 수 있음

# 트랜잭션 격리수준 
Isolation Level
- 트랜잭션에서 일관성 없는 데이터를 허용하는 수준
- 트랜잭션간의 침범을 막기 위해, 즉 트랜잭션의 독립성을 위해 Locking을 한다.
- 무조건 Locking으로 동시에 수행되는 수많은 트랜잭션들을 순서대로 처리하는 방식으로 구현하게 되면 데이터베이스의 성능은 떨어짐 (무결성 up, 동시성 down)
- 그렇다고 해서, 성능을 높이기 위해 Locking의 범위를 줄인다면, 잘못된 값이 처리될 문제가 발생 (동시성 up, 무결성 down)
- 효율적인 Locking이 필요하다,

# Isolation level 종류
1. Read Uncommitted (레벨 0)
2. Read Uncommitted (레벨 1)
3. Repeatable Read (레벨 2)
4. Serializable (레벨 3)

## level 높을 경우
비용이 많이 듦
## level 낮을 경우
- Dirty Read
- Non-Repeatable Read
- Phantom Read
# 출처
- [DBMS는 어떻게 트랜잭션을 관리할까?](https://d2.naver.com/helloworld/407507)
- [Transaction Isolation Level](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction%20Isolation%20Level.md)