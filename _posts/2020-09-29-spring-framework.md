---
title: Spring Framework
author: Yujin Ahn
date: 2020-09-29 22:00:00 +0900
categories: [Study, Spring]
tags: [spring]     # TAG names should always be lowercase
---

---

Spring Framework 예제 : [spring-petclinic](https://projects.spring.io/spring-petclinic/)
[(git)](https://github.com/spring-projects/spring-petclinic)

---

# [ Inversion of Control ]
의존성에 대한 컨트롤이 뒤바뀌었다.

#### 원래는 어떻게 되었나?
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

### Inversion of Control
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

### IoC(Inversion of Control) 컨테이너
- 스프링은 IoC용 컨테이너를 제공해준다. 이 컨테이너의 핵심 인터페이스가 Application Context (Bean Factory)
- 빈(bean)을 생성, 의존성을 관리해준다.
- 위의 OwnerController, OwnerRepository도 빈이다. 따라서 이 빈들의 의존성도 IOC 컨테이너가 관리.

#### 빈은 누구인가
@Controller, @Service, @Repository 등 어노테이션이 붙은 애들.
- 빈인 것들은 IntelliJ 좌측에 초록 콩이 붙음ㅎㅎ

#### ApplicationContext 확인하는 법
- 보통 IoC컨테이너를 직접 접할 일은 없다.
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

### 빈 (Bean)
**스프링 IoC 컨테이너가 관리하는 객체**
#### 빈이 되려면 어떻게 해야하나요?
IoC 컨테이너에 등록해야 한다
1. Component Scanning
    - @Component
        - @Controller
        - @Service
        - @Repository
2. 직접 등록하는 방법
    - @Bean으로 등록. 이때 @Configuration 을 가지고 있는 클래스 안에서만 가. // @SpringBootApplication은 @Configuration가지고 있음.

#### 빈 꺼내 쓰는법
- @Autowired 또는 @Inject
- (선호하지 않음) ApplicationContext에서 getBean()으로 직접 꺼내쓰는 방법.

빈만이 빈을 쓸 수 있다. 빈을 사용하고 싶으면 클래스도 빈이어야 함.

### 의존성 주입 (Dependency Injection)
의존성을 주입할 때 @Autowired 또는 @Inject를 사용한다.

#### @Autowired / @Inject를 어디에 붙일까?
- 생성자
- Setter
- 필드
☆☆☆☆☆

빈이 되는 클래스에 생성자가 하나만 있고 그 생성자의 매개변수 타입이 빈으로 등록이 되어있다면,

**@Autowired가 없더라도 빈을 주입해준다.**

[ spring-petclinic의 owner/OwnerController 참고 ]
```java
@Controller
class OwnerController {

	private static final String VIEWS_OWNER_CREATE_OR_UPDATE_FORM = "owners/createOrUpdateOwnerForm";

	private final OwnerRepository owners;

	private VisitRepository visits;

	public OwnerController(OwnerRepository clinicService, VisitRepository visits) {
		this.owners = clinicService;
		this.visits = visits;
	}
    //...
}
```

## Repository는 아무런 어노테이션이 안되어있는것 같은데 왜 빈일까?
애플리케이션 컨텍스트에는 수많은 라이프사이클 인터페이스가 있다.

그 라이프사이클 인터페이스를 구현하면 특정한 애플리케이션 큰택스트를 빈를 등록해서 만들고, 초기화하고 빈들을 읽어들이고 하는 수많은 관계들에 끼어들어가는 일들을 할 수 있다.
Spring Data JPA 프로젝트의 Repository<> 인터페이스를 구현한 인터페이스 타입의 객체를 만들어준다. Spring Data JPA는 인터페이스 타입의 객체를 만들어주는 빈을 만들어서 애플리케이션 컨텍스트에 등록해주는 라이프사이클 콜백을 만들어 놨다.

☆☆☆☆☆

---

# [ AOP ( Aspect Oriented Programming ) ]
흩어진 코드를 하나로 모으자

single responsibility principle

1. 바이트 코드
2. 프록시 패턴을 사용

---

# [ PSA (Portable Service Abstraction) ]
이식 가능한 서비스 추상화, 잘 만든 인터페이스
코드를 직접쓰면
- 확장성이 좋지 못하다
- 특정 기술에 특화되어있기 때문에, 기술을 바뀔때마다 코드를 바꾸어야 한다.

잘 만든 인터페이스가 있다면 그 코드들을 이용하자
- 테스트하기가 좋음
- 이식성이 좋음. 바꿔끼기가 좋음

#### 예제 1. 트랜잭션
@Transactional이라는 어노테이션이 있고, 이를 처리할 Aspect가 어딘가에 있다. Aspect는 기술에 독립적인 Platform Transaction Manager라는 인터페이스를 이용해 코딩해 놓았다. 그렇기 때문에 Platform Transaction Manager의 구현체가 바뀌더라도 Transaction aspect의 코드는 바뀌지 않는다. 구현체는 Bean으로 등록된다.
#### 예제 2. 캐싱
@EnableCaching
CacheManager의 구현체가 바뀌더라도 Aspect 코드가 바뀔 일은 없다.
```java
@Configuration(proxyBeanMethods = false)
@EnableCaching
class CacheConfiguration {

	@Bean
	public JCacheManagerCustomizer petclinicCacheConfigurationCustomizer() {
		return cm -> {
			cm.createCache("vets", cacheConfiguration());
		};
	}
    //...
 }
```
#### 예제 3. Spring Web MVC
코드에서 @Controller와 @GetMapping을 사용하는데 이것만 가지고는 서블릿을 사용하는지, 리액티브를 사용하는지 알 수 없다.
- 기술에 독립적이다 = 추상화
- 추상화되어있는 코드는 전환이 쉽다.
#### +) Spring data JPA도
Hibernate를 사용하던지 EclipseLink를 사용하던지
# 출처
[인프런 스프링 프레임워크 입문](https://www.inflearn.com/course/spring#)