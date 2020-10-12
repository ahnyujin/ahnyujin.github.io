---
title: (C++) 정적/동적 바인딩
author: Yujin Ahn
date: 2020-10-06 17:00:00 +0900
categories: [Languages&Frameworks, Cpp]
tags: [cpp]     # TAG names should always be lowercase
---
# 바인딩(Binding)
프로그램 소스에 쓰인 변수, 이름 식별자들에 대한 값 또는 속성을 확정하는 과정

이 과정이 이루어지는 시점에 따라
- 컴파일 시점에서 이루어지면 __정적 바인딩__
- 실행 도중(runtime)에 이루어지면 __동적 바인딩__

정적 바인딩은 타입을 사용하고 동적바인딩은 객체를 사용한다.
c++ default 정적 바인딩
```cpp
class Base {
public:
    void Print() {
        cout << "this is Base" << endl;
    }
}
class Derived : public Base {
public:
    void Print() {
        cout << "this is Derived" << endl;
    }
}

int main() {
    Base *b = new Derived(); 부모 클래스 타입 포인터가 자식 객체를 받을 수 있다. 
    b->Print(); // 여기서 Base(부모)의 Print가 실행될까? Derived(자식)의 Print가 실행될까??
}
```
정답: Base의 Print. 정적 바인딩이기 때문에 Base, 즉 부모 클래스의 메소드가 그대로 

부모클래스의 함수를 **virtual**(가상함수)로 만들면 동적 바인딩이 일어나 실행시점에 객체의 메소드를 실행시킴.