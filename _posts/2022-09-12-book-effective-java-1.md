---
title: Effective Java - 2장. 객체 생성과 파괴
author: Yujin Ahn
date: 2022-09-12 01:39:00 +0900
categories: [Blogging, Book]
tags: [JAVA]
---

# ITEM 1 - 생성자 대신 정적 팩토리 메서드를 고려하라

클래스는 클라이언트에 public 생성자 대신 정적 팩토리 메서드를 제공할 수 있다.

정적 팩토리 메서드 - 객체 생성을 하는 정적(static) 메서드

이런 경우 5가지 장점이 있다.

1. 이름을 가질 수 있다
    1. 하나의 시그니처로는 하나의 생성자만 만들 수 있다. 의미가 명확하게 드러나는 이름으로 반환될 객체의 특성을 제대로 설명할 수 있다.
2. 호출될 때마다 인스턴스를 새로 생성하지 않아도 된다
    1. 불변 클래스는 인스턴스를 미리 만들어 놓거나 새로 생성한 인스턴스를 캐싱하여 재활용할 수 있으므로 불필요한 객체 생성을 막을 수 있다.
    2. 정적 팩토리 방식의, 언제 어떤 인스턴스가 살아있게 할 지 통제하는 클래스를 인스턴스 통제(instance-controlled) 클래스라고 한다. 인스턴스를 통제하면 클래스를 싱글턴으로 만들 수도, 인스턴스화 불가로 만들 수도 있다. 또한 불변 값 클래스에서 동치인 인스턴스가 단 하나뿐임을 보장할 수도 있다.
3. 반환 타입의 하위 타입 객체를 반환할 수 있다
    1. 구현 클래스를 공개하지 않고도 객체를 반환할 수 있어 API를 작게 만들 수 있다는 장점이 있다. ex) java.util.Collections
4. 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다
    1. 클라이언트는 팩토리가 건네주는 객체가 어떤 클래스의 인스턴스인지 알 수도, 알 필요도 없기에 유연하게 구현할 수 있다.
5. 정적 팩토리 메소드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다
    1. 클라이언트가 서비스의 인스턴스를 얻을 때 사용하는 서비스 접근 API 역시 정적 팩토리이다. 서비스 제공자 인터페이스가 없다면 각 구현체를 인스턴스로 만들 때 리플렉션을 사용해야 한다.
    

단점은 다음과 같다.

1. 상속을 하려면 public이나 protected 생성자가 필요하니 정적 팩터리 메서드만 제공하면 하위 클래스를 만들 수 없다.
2. 정적 팩토리 메서드는 프로그래머가 찾기 어렵다.
    1. 이러한 문제를 해결하기 위해 흔히 사용하는 명명 방식들은
    2. from : 하나의 매개변수를 받아 객체를 생성 (형변환)
    3. of : 여러개의 매개변수를 받아 객체를 생성
    4. valueOf : from과 of의 더 자세한 버전
    5. instance | getInstance : 인스턴스를 생성하지만, 같은 인스턴스임은 보장하지 않는다
    6. create | newInstance : 새로운 인스턴스 생성 등이 있다.

# ITEM 2 - 생성자에 매개변수가 많다면 빌더를 고려하라

정적 팩터리와 생성자는 선택적 매개변수가 많을 때 대응하기 어렵다

## 점층적 생성자 패턴(telescoping constructor pattern)

```java
public class NutritionFacts {
	private final int calories;      // 필수
	private final int fat;           // 선택
	private final int sodium;        // 선택
	private final int carbonhydrate; // 선택
	
	public NutritionFacts(int calories) {
		this(calories, 0);
	}

	public NutritionFacts(int calories, int fat) {
		this(calories, fat, 0);
	}
...

	public NutritionFacts(int calories, int fat, int sodium, int carbonhydrate) {
		this.calories = calories;
		this.fat = fat;
		this.sodium = sodium;
		this.carbonhydrate = carbonhydrate;
	}
}
```

필수 매개변수만 받는 생성자, 필수 매개변수 1개와 선택 매개변수 1개를 받는 생성자 … 전부 다 받는 생성자로 늘려나가는 형태. 인스턴스를 만들려면 원하는 매개변수를 포함하는 가장 짧은 생성자를 사용하면 된다.

선택 매개변수의 수가 많아지면 읽기도 어렵고, 코드를 작성하기도 어렵다.

## 자바빈즈 패턴(JavaBeans pattern)

매개변수가 없는 생성자로 객체를 만들고, setter 메서드를 통해 매개변수의 값을 설정한다

```java
public class NutritionFacts {
	private final int calories      = 0 // 필수
	private final int fat           = 0 // 선택
	private final int sodium        = 0 // 선택
	private final int carbonhydrate = 0 // 선택
	
	public NutritionFacts() { }

	public void setCalories(int val)      { calories = val; }
	public void setFat(int val)           { fat = val; }
	public void setSodium(int val)        { sodium = val; }
	public void setCarbonhydrate(int val) { carbonhydrate = val; }
}
```

코드가 길지만 점층적 생성자 패턴에 비해 더 읽기 쉽고 인스턴스를 만들기도 쉽다.

그러나 심각한 단점을 가지고 있다. 객체를 하나 만드려면 여러 setter를 호출해야 하고, 객체가 완전히 생성되기 이전에는 일관성(consistency)이 무너진 상태에 놓이게 된다(오히려 일관성 면에서는 점층적 생성자 패턴이 유리하다). 일관성이 깨진 객체는 버그를 심은 코드와 그 버그 때문에 런타임에 문제를 겪는 코드가 물리적으로 멀 것이므로 디버깅이 어렵다. 클래스를 불변으로 만들 수도 없으므로 스레드 안전성을 위해 프로그래머의 추가 작업이 필요하다.

## 빌더 패턴(Builder pattern)

스레드 안전성과 가독성을 지키는 방법이다.

```java
public class NutritionFacts {
	private final int calories;      // 필수
	private final int fat;           // 선택
	private final int sodium;        // 선택
	private final int carbonhydrate; // 선택

	public static class Builder {
	  // 필수 매개변수
	  private final int calories;
	 
	  // 선택 매개변수 - 기본값으로 초기화
	  private final int fat           = 0;
		private final int sodium        = 0;
		private final int carbonhydrate = 0;
	
	  public Builder(int calories) {
	    this.calories = calories;
	  }
		
	  public Builder fat(int val) {
	   fat = val;
	   return this;
	  }
	
	  public Builder sodium(int val) {
	   sodium = val;
	   return this;
	  }
	
	  public Builder carbonhydrate(int val) {
	   carbonhydrate = val;
	   return this;
	  }
	
		public NutritionFacts build() {
	    return new NutritionFacts(this);
	  }
  }

	private NutritionFacts(Builder builder) {
	  calories = builder.calories;
		fat = builder.fat;
		sodium = builder.sodium;
		carbonhydrate = builder.carbonhydrate;
	}
}
```

1. 클라이언트는 필요한 객체를 직접 만드는 대신 필수 매개변수만으로 생성자를 호출해 빌더 객체를 얻는다
2. 빌더 객체가 제공하는 세터 메소드들로 원하는 선택 매개변수들을 설정한다
3. 마지막으로 매개변수가 없는 build 메서드를 호출해 객체(일반적으로 불변)를 얻는다.

**빌더의 세터 메서드들은 빌더 자신을 반환해 연쇄적으로 호출할 수 있다. 이러한 방식을 fluent API 혹은 method chaining이라고 한다**

단점은 빌더 생성 코드가 장황해서 매개변수 4개 이상은 되어야 값어치를 한다는 것이다. 그러나 시간이 지날수록 매개변수는 많아질 것이므로 처리해야 할 매개변수가 많다면 빌더 패턴을 사용하는것이 좋다.

# ITEM 3 - private 생성자나 열거 타입으로 싱글턴임을 보증하라

싱글턴(singleton)이란? 인스턴스를 하나만 생성할 수 있는 클래스

싱글턴을 만드는 방법 두가지를 소개한다. 두 방식 모두 생성자는 private으로 감춘다.

## public static final 필드 방식의 싱글턴

```java
public class Elvis {
	**public static final Elvis INSTANCE = new Elvis();**
	private Elvis() {...}
	
	public void leaveTheBuilding() {...}
}
```

장점은 public static 필드가 final이니 클래스가 싱글턴임이 명확하다.

## 정적 팩토리 방식의 싱글턴

```java
public class Elvis {
	**private** static final Elvis INSTANCE = new Elvis();
	private Elvis() {...}
	**public static Elvis getInstance**() { return INSTANCE; }
	
	public void leaveTheBuilding() {...}
}
```

getInstance는 항상 같은 객체의 참조를 반환하므로 싱글턴을 유지할 수 있다.

장점은 API를 바꾸지 않고도 싱글턴이 아니게 변경 가능하다는 점이다.

그러나 위의 두 방식으로 만든 싱글턴 클래스를 역직렬화 할 때마다 새로운 인스턴스가 생성되는 의도치 않은 문제가 생기기 때문에 아래와 같이 readResolve 메서드를 추가해 주어야 한다.

```java
// 싱글턴임을 보장해주는 readResolve 메서드
private Object readResolve() {
 // 진짜 Elvis를 반환하고, 가짜 Elvis는 가비지 컬렉터에 맡긴다.
 return INSTANCE;
}
```

또한 예외적으로 리플렉션 API인 AccessibleObject.setAccessible을 사용해 private 생성자를 호출할 수 있다. 이러한 경우는 생성자에서 두 번 이상 객체가 생성되려 할 때 예외를 던지게 하면 된다.

## Enum 타입 방식의 싱글턴

```java
public enum Elvis {
  INSTANCE;
  
  public void leaveTheBuilding() {...}
}
```

원소가 하나뿐인 Enum으로 싱글턴을 만드는 것.

추가 작업 없이 직렬화에 유리하다. 위의 두 방법보다 추천. 그러나 만드려는 싱글턴이 Enum 외의 클래스를 상속해야 한다면 사용할 수 없다.

# ITEM 4 - 인스턴스화를 막으려거든 private 생성자를 사용하라

정적 멤버만 담은 유틸리티 클래스와 같이, 클래스의 의도를 명확히 하기 위해 인스턴스화를 막아야 하는 경우가 있다.

인스턴스화를 막으려면 private 생성자를 추가하자.

명시된 생성자가 없으면 컴파일러가 기본 생성자를 자동 생성하고, 사용자는 이 생성자가 자동생성 된 것인지 구분할 수 없기 때문이다.

```java
public class UtilityClass {
  // 기본 생성자가 만들어지는 것을 막는다(인스턴스화 방지용)
	**private UtilityClass**() {
		throw new AssertionError();
  }
}
```

위의 private 생성자를 사용한 코드는 두가지 장점이 있다

1. 클래스 인스턴스화를 막아준다
    1. 그러나 직관적이지 않은 코드이니, ‘인스턴스화 방지용’과 같은 주석을 달아주자
2. 상속을 불가능하게 한다
    1. 하위클래스가 상위클래스의 생성자에 접근할 수 없어 생성자를 호출할 수 없다

# ITEM 5 - 자원을 직접 명시하지 말고 의존 객체 주입을 사용하라

클래스가 내부적으로 하나 이상의 자원에 의존하고, 그 자원이 클래스의 동작에 영향을 주는 경우 정적 유틸리티 클래스나 싱글턴 방식이 적합하지 않다. ex) 맞춤법 검사기와 같이 사용하는 자원(언어, 특수 어휘 등…)에 따라 동작이 달라지는 클래스. 또한 이러한 경우에는 클래스가 직접 자원들을 만들게 해서도 안된다. 대신 필요한 자원을 (혹은 자원을 만드는 팩터리를) 생성자에 (혹은 정적 팩터리나 빌더에) 넘겨준다. 이 기법을 의존 객체 주입이라고 한다. 클래스의 유연성, 재사용성, 테스트 용이성을 개선해준다.

# ITEM 6 - 불필요한 객체 생성을 피하라

필요없는 객체의 반복 생성을 막고 기존 객체를 재사용할 수 있는 방법들이다.

## 문자열 리터럴을 사용하는 모든 코드가 같은 객체를 재사용함을 보장하라

```java
String s = new String("utility");
// 위의 코드 대신
String s = "utility"
```

같은 가상 머신 안에서 사용하는 동일한 문자열 리터럴을 사용하는 모든 코드가 같은 객체를 재사용함이 보장된다.

## 불변 클래스에서 생성자 대신 정적 팩토리 메서드를 사용한다

Boolean(String) 생성자 대신 Boolean.valueOf(String) 을 사용하는 것이 좋다.

## 생성비용이 비싼 객체를 반복해 사용한다면 캐싱을 사용하자

```java
static boolean isRomanNumeral(String s) {
  return s.matches("^(?=.)M*(C[MD]|D?C{0,3})"
          + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");
}
```

위 코드의 단점은 String.matches 메서드가 Pattern 인스턴스를 한번 생성하고, 쓰고 버린다는 것이다. 성능이 중요한 경우 이 메서드를 반복해서 사용하는 것은 적합하지 않다.

성능을 개선하기 위해 정규표현식을 표현하는 (불변)Pattern 인스턴스를 클래스 초기화(정적 초기화)과정에서 직접 생성해 캐싱해두고, 메서드가 호출될 때마다 이 인스턴스를 재사용한다.

```java
public class RomanNumerals {
  private static final Pattern ROMAN = Pattern.compile(
    "^(?=.)M*(C[MD]|D?C{0,3})"
    + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");

  static boolean isRomanNumeral(String s) {
    return ROMAN.matcher(s).matches();
  }
}
```

## 박싱된 기본타입보다 기본타입을 사용하고 의도치 않은 오토박싱이 숨어들지 않도록 하자

```java
private static long sum() {
  Long sum = 0L;
  for(long i = 0; i <= Integer.MAX_VALUE; i++)
    sum += i;
  
  return sum;
}
```

위 코드의 sum 변수의 타입을 long으로 변경하면 불필요한 Long 인스턴스를 231개나 아낄 수 있고, 속도도 6.3초에서 0.59초로 빨라진다.

# ITEM 7 - 다 쓴 객체 참조를 해제하라

자바와 같은 가비지 컬렉션 언어에서 또한 메모리 누수에 주의하자. 객체 참조 하나를 회수하지 않으면 가비지 컬렉터는 그 객체가 참조하는 모든 객체를 회수하지 못한다. 따라서 성능에 악영향을 줄 수 있다.

참조를 담은 변수의 scope를 최소가 되도록 적절히 정의했다면 변수가 유효 범위(scope)밖으로 벗어나는 때에 참조 해제는 자연스럽게 일어난다. 다만 아래와 같은 경우들은 객체 참조 해제에 유의하는 것이 좋다.

## 자기 메모리를 직접 관리하는 클래스

자기 메모리를 직접 관리하는 클래스의 경우 메모리 누수에 주의해야 한다.

객체 참조를 담는 스택을 예시로 들면 비활성 영역은 더이상 사용되지 않는다. 가비지 컬렉터는 이러한 사실을 알 길이 없다. 그러므로 프로그래머는 비활성 영역이 되는 순간에 객체를 더이상 사용하지 않을것을 알리기 위해 null 처리 해야한다.

```java
public Object pop() {
  if (size == 0)
    throw new EmptyStackException();
  Object result = elements[--size];
  **elements[size] = null; // 참조 해제**
  return result;
}
```

위 코드의 또다른 장점은 해제한 참조를 이후에 사용했을 때 프로그램이 NullPointerException을 던지며 종료된다는 것이다. 프로그램의 오류는 가능한 조기에 발견되는 것이 좋다.

## 캐시

객체 참조를 캐시에 넣고 더이상 사용하지 않을 경우

만약 캐시 외부에서 **키**를 참조하는 동안만 엔트리가 살아있는 캐시가 필요하다면 WeakHashMap을 사용한다. 이렇게 하면 다 쓴 엔트리는 즉시 자동으로 제거된다.

이외에 엔트리 유효기간을 정확히 정의하기 어려울 경우, ScheduledThreadPoolExecutor와 같은 백그라운드 스레드를 사용하는 방법, 캐시에 새 엔트리를 추가할 때 추가 작업을 수행해주는 방법이 있다.

## listener 혹은 callback

클라이언트가 콜백을 등록만 하고 해지하지 않는다면 콜백은 계속해서 쌓이기만 한다. 이러한 경우 콜백을 약한 참조(weak reference)로 저장하여 가비지 컬렉터가 즉시 수거해 가게끔 한다. ex) WeakHashMap에 키로 저장