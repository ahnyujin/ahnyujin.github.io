---
title: [C++] 동적 할당과 객체 복사
author: Yujin Ahn
date: 2020-10-06 17:00:00 +0900
categories: [Languages&Frameworks, Cpp]
tags: [cpp]     # TAG names should always be lowercase
---

# 동적 할당
C++는 자바처럼 가비지 컬렉션을 알아서 해주지 않기 때문에 개발자가 메모리 신경 써야한다.
new
delete : 메모리 해제
배열일 경우 delete[]

delete를 해주지 않으면 객체는 남아있지만 그 주소값을 가지고 있는 포인터는 메모리상에 존재하지 않게 된다.

# 깊은 복사와 얕은 복사
```cpp
#include <stdio.h>
int main(){
    int *a = new int(5);
    int *b = new int(5);
    
    *a = *b; // 깊은 복사(값을 복사)
    a = b;// 얕은 복사 (참조만 복사) b와 같은것을 가리키게 됨.

    delete a;
    delete b;
}
```

얕은 복사는 delete를 할 경우 문제가 일어날 수 있다.
얕은 복사를 방지하는 방법
1. 문자열 복사하고 싶은 경우 strcpy(깊은 복사) 사용
2. 대입연산자를 오버로딩 해주기
3. 이동 시맨틱
인스턴스화된 객체의 메모리 소유권을 이전하는 기능.
임시 객체가 생성되었을 때 부하를 최소화 하기 위하여 원본 객체의 멤버를 null로 초기화 시켜 소유권을 이전시킨다.
임시객체는 rvalue이다. c++는 
&& rvalue참조자