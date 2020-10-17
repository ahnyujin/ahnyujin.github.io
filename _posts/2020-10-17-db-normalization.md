---
title: (DB) DB 정규화
author: Yujin Ahn
date: 2020-10-17 17:00:00 +0900
categories: [CS, Database]
tags: [db]     # TAG names should always be lowercase
---
# DB 정규화란?

관계형 데이터베이스의 설계에서 중복을 최소화하게 데이터를 구조화하는 프로세스를 정규화라고 한다.

목표
1. 불필요한 데이터(data redundancy)를 제거한다.
2. 데이터 저장을 "논리적으로"한다

정규화 된 정도를 정규형(Normal Form)이라고 한다. 높은 차수의 정규형으로 갈수록 까다롭다.

정규형은 1NF~6NF까지 있지만 비공식적으로 3NF가 되었으면 정규화 되었다고 말하므로, BCNF까지만은 알아두도록 하자.

# 제1정규형 : 1NF (First Normal Form)
릴레이션에 속한 모든 속성의 도메인이 원자값으로만 구성되어 있으면 제1정규형

# 제2정규형 : 2NF
제1정규형에 속하면서, 기본키가 아닌 모든 속성이 **기본키에 완전 함수적 종속**되면 제2정규형

# 제3정규형 : 3NF
제2정규형에 속하면서, 기본키가 아닌 모든 속성이 기본키에 이행적 함수적 종속 되지 않으면 제3정규형

# BCNF (Boyce-Codd Normal Form)
제3정규형에 속하면서, 모든 결정자가 후보키 집합에 속한 정규형 //따라서 일반 컬럼이 후보키를 결정하는 경우 위배

# 역정규화
정규화를 통해 분리되었던 릴레이션에서 중복을 허용하고 다시 통합하거나 분할하여 구조를 재조정하는 과정
데이터베이스에 저장된 자료를 검색하는 시간을 증가시키며 성능을 저하시킬 수 있다. 따라서 데이터베이스의 물리적 설계 과정에서 성능을 향상시키기 위해 역정규화를 실행한다.

# 용어 정리

## 함수적 종속성 (Functional Dependency)
X(결정자) -> Y(종속자)
Y가 X에 함수적으로 종속되어 있다.

## 이행적 함수 종속 (Transitive Functional Dependency)
X,Y,Z에 대해 X->Y, Y->Z이고 X->Z일때 Z가 X에 이행적으로 함수 종속되었다고 한다.

## 삽입이상 (Insertion Anomaly)
새 데이터를 삽입하기 위해 불필요한 데이터도 함께 삽입해야 하는 문제
## 갱신이상 (Update Anomaly)
중복 튜플 중 일부만 변경하여 데이터가 불일치하게 되는 모순의 문제
## 삭제이상 (Deletion Anomaly)
튜플을 삭제하면 꼭 필요한 데이터까지 함께 삭제되는 데이터 손실 문제

STUDENT_ID STUDENT_NUM DEPARTMENT COURSE_ID를 갖고있는 DB를 예시로 들면
- 삽입이상
    - 테이블에 아직 수강신청 하지 않은 학생을 추가하려면 '미수강'같은 과목코드를 추가해야함
- 갱신이상
    - 학생이 전과하는 경우, 학생이 수강신청한 row 일부만 과를 수정하면 학생의 소속이 모호해짐
- 삭제이상
    - 1과목 듣고있는 학생이 수업을 드랍할 경우, row를 삭제해버리면 학생정보도 사라진다

# 참고
- [데이터베이스 정규화 1NF, 2NF, 3NF](https://yaboong.github.io/database/2018/03/09/database-normalization-1/)
- [데이터베이스 정규화 - 이상현상 & 함수적 종속성](https://yaboong.github.io/database/2018/03/09/database-anomaly-and-functional-dependency/)
- [데이터베이스 정규화 1NF, 2NF, 3NF, BCNF](https://3months.tistory.com/193)
- [데이터베이스 정규화, 역정규화](https://dodo000.tistory.com/21)