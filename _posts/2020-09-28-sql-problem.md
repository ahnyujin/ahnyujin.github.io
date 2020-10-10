---
title: SQL 문제풀이
author: Yujin Ahn
date: 2020-09-28 20:40:00 +0900
categories: [CS, Database]
tags: [db]     # TAG names should always be lowercase
---
MYSQL 사용

---

# [ SELECT ]
## 59034. 모든 레코드 조회하기
```sql
SELECT * FROM ANIMAL_INS ORDER BY ANIMAL_INS.ANIMAL_ID
```
## 59035. 역순 정렬하기
```sql
SELECT NAME, DATETIME FROM ANIMAL_INS ORDER BY ANIMAL_INS.ANIMAL_ID DESC
```
## 59036. 아픈 동물 찾기
```sql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS WHERE INTAKE_CONDITION = 'Sick' ORDER BY ANIMAL_ID
```
__" " 가 아닌 ' ' 사용에 주의하자.__
## 59037. 어린 동물 찾기
```sql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS WHERE INTAKE_CONDITION != 'Aged' ORDER BY ANIMAL_ID
```
## 59403. 동물의 아이디와 이름
```sql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS ORDER BY ANIMAL_ID
```
## 59404. 여러 기준으로 정렬하기
```sql
SELECT ANIMAL_ID, NAME, DATETIME FROM ANIMAL_INS ORDER BY NAME, DATETIME DESC
```
## 59405. 상위 n개 레코드
MYSQL
```sql
SELECT NAME FROM ANIMAL_INS ORDER BY DATETIME LIMIT 1
```
Oracle의 경우
```sql
SELECT NAME FROM ANIMAL_INS ORDER BY DATETIME ROWNUM <= 1
```

---

# [ SUM, MAX, MIN ]
## 59415. 최댓값 구하기
```sql
SELECT MAX(DATETIME) FROM ANIMAL_INS
```
## 59038. 최솟값 구하기
```sql
SELECT MIN(DATETIME) FROM ANIMAL_INS
```
## 59406. 동물 수 구하기
```sql
SELECT COUNT(*) AS COUNT FROM ANIMAL_INS
```
AS
- ALIAS의 예약어. 필드명이나 테이블 명 다시 지을때 사용
- **생략 가능하다**

## 59408. 중복 제거하기
```sql
SELECT COUNT(DISTINCT NAME) FROM ANIMAL_INS
```

---

# [ GROUP BY ]
## 59040. 고양이와 개는 몇 마리 있을까
```sql
SELECT ANIMAL_TYPE, COUNT (ANIMAL_TYPE) FROM ANIMAL_INS GROUP BY ANIMAL_TYPE ORDER BY ANIMAL_TYPE
```
## 59041. 동명 동물 수 찾기
```sql
SELECT NAME, COUNT(*) COUNT FROM ANIMAL_INS GROUP BY NAME
HAVING COUNT(NAME) >= 2 ORDER BY NAME
```
---

# [ IS NULL ]
## 59039. 이름이 없는 동물의 아이디
- NULL을 체크할때는 = 가 아닌 IS를 사용한다.
```sql
SELECT ANIMAL_ID FROM ANIMAL_INS WHERE NAME IS NULL ORDER BY ANIMAL_ID
```
## 59407. 이름이 있는 동물의 아이디
- 위 문제에서 IS 를 IS NOT으로 바꾸기
## 59410. NULL 처리하기
- IFNULL(컬럼명, 변환값) : 컬럼 내용이 NULL일때 값을 변환
```sql
SELECT ANIMAL_TYPE, IFNULL(NAME, 'No name') NAME, SEX_UPON_INTAKE FROM ANIMAL_INS ORDER BY ANIMAL_ID
```
---

# [ JOIN ]
## 59042. 없어진 기록 찾기
- OUTS에는 있고 INS에는 없는 기록 찾기
- RIGHT OUTER JOIN ( = RIGHT JOIN ) 사용
```sql
SELECT OUTS.ANIMAL_ID, OUTS.NAME
FROM ANIMAL_INS AS INS RIGHT JOIN ANIMAL_OUTS AS OUTS ON INS.ANIMAL_ID = OUTS.ANIMAL_ID
WHERE INS.ANIMAL_ID IS NULL
ORDER BY OUTS.ANIMAL_ID
```
## 59043. 있었는데요 없었습니다
```sql
SELECT INS.ANIMAL_ID, INS.NAME
FROM ANIMAL_INS AS INS JOIN ANIMAL_OUTS AS OUTS ON INS.ANIMAL_ID = OUTS.ANIMAL_ID
WHERE INS.DATETIME > OUTS.DATETIME
ORDER BY INS.DATETIME
```
## 59044. 오랜 기간 보호한 동물(1)
```sql
SELECT INS.NAME, INS.DATETIME
FROM ANIMAL_INS INS LEFT JOIN ANIMAL_OUTS OUTS ON INS.ANIMAL_ID = OUTS.ANIMAL_ID
WHERE OUTS.ANIMAL_ID IS NULL
ORDER BY INS.DATETIME LIMIT 3
```
## 59045. 보호소에서 중성화한 동물
```sql
SELECT INS.ANIMAL_ID, INS.ANIMAL_TYPE, INS.NAME  FROM ANIMAL_INS INS JOIN ANIMAL_OUTS OUTS ON INS.ANIMAL_ID = OUTS.ANIMAL_ID
WHERE INS.SEX_UPON_INTAKE LIKE 'Intact%' AND (OUTS.SEX_UPON_OUTCOME LIKE 'Spayed%' OR OUTS.SEX_UPON_OUTCOME LIKE 'Neutered%')
```
위
```sql
OUTS.SEX_UPON_OUTCOME LIKE 'Spayed%' OR OUTS.SEX_UPON_OUTCOME LIKE 'Neutered%'
```
식을
```sql
OUTS.SEX_UPON_OUTCOME REGEXP '^Spayed|^Neutered'
```
이렇게도 바꿀 수 있다.
### MYSQL 패턴 매칭(pattern matching)
1. LIKE
   - LIKE 연산자는 특정 패턴을 포함하는 데이터만을 검색하기 위해 사용
   - 특정 패턴을 포함하지 않는 데이터를 검색하고 싶을 때는 **NOT LIKE** 연산자를 사용
   - 와일드카드(wildcard) 문자
     - '%'는 0개 이상의 문자
     - '_'는 1개의 문자를 대체함.
2. REGEXP
  - LIKE 연산자보다 더욱 복잡한 패턴을 검색하고 싶을 때 사용
  - REGEXP 연산자는 정규 표현식을 토대로 하는 패턴 매칭 연산을 제공. [참고](http://tcpschool.com/mysql/mysql_operator_patternMatching)
  - NOT REGEXP 제공

# 출처
- 문제 출처 - [프로그래머스 > SQL 고득점 Kit](https://programmers.co.kr/learn/challenges?selected_part_id=17043)
- [tcpschool > MYSQL > 패턴 매칭](http://tcpschool.com/mysql/mysql_operator_patternMatching)