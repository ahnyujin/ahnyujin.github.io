---
title: Spring Framework
author: Yujin Ahn
date: 2020-09-29 22:00:00 +0900
categories: [Study, Spring]
tags: [spring]     # TAG names should always be lowercase
---

Spring Framework 예제 : [spring-petclinic](https://projects.spring.io/spring-petclinic/)
[(git)](https://github.com/spring-projects/spring-petclinic)
# Inversion of Control
의존성에 대한 컨트롤이 뒤바뀌었다.

## 원래는 어떻게 되었나?
원래 의존성에 대한 제어권은 자기 자신이 들고있는것.
```java
class OwnerController {
	private OwnerRepository owners = new OwnerRepository();
}
```
OwnerRepository는 OwnerController의 의존성
- 즉, OwnerRepository가 있어야 OwnerController를 제대로 사용할 수 있음.
- OwnerController가 OwnerRepository를 필요로 함

의존성을 누가 관리하냐가 관건.

## Inversion of Control
나(여기서 OwnerRepository) 이외의 누군가가 의존성을 주입해주는것.
```java
class OwnerController {
	private OwnerRepository owners;
    
    public OwnerController(OwnerRepository owners) {
        this.owners = owners;
    }
}

class OwnerControllerTest {
    @Test
    public void create(){
        OwnerRepository owners = new OwnerRepository();
        OwnerController controller = new OwnerController(owners);
    }
}
```

# IOC(Inversion of Control) 컨테이너
- 스프링은 IOC용 컨테이너를 제공해준다. 이 컨테이너의 핵심 인터페이스가 Application Context (Bean Factory)
- 빈(bean)을 생성, 의존성을 관리해준다.
- 위의 OwnerController, OwnerRepository도 빈이다. 따라서 이 빈들의 의존성도 IOC 컨테이너가 관리.

## 빈은 누구인가
@Controller, @Service, @Repository 등 어노테이션이 붙은 애들.
- 빈인 것들은 IntelliJ 좌측에 초록 콩이 붙음ㅎㅎ

## ApplicationContext 확인하는 법
- 보통 IOC컨테이너를 직접 접할 일은 없다.
하지만 ApplicationContext도 하나의 빈으로 만들어졌기 때문에 확인 가능
```java
@RestController
public class SampleController {
    
    @Autowired
    ApplicationContext applicationContext;

    @GetMapping("/context")
    public String context() {
        return applicationContext.getBean(OwnerRepository.class);
    }
}
```

# 출처
[인프런 스프링 프레임워크 입문](https://www.inflearn.com/course/spring#)