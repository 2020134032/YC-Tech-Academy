목차
1. Bean 주입
2. Bean Component 차이
3. Field Injection, Constructor Injection 차이
4. @Primary, @Qualifier annotation

## Bean 
object controlled by the spring ioc

스프링이 의존관계 주입을 위해서 생성하고 관리하는 객체.

bean is an object instantiated and manged by spring ioc contatiner

*일반적인 DI와 bean을 통한 DI의 차이*
- 스프링은 bean을 싱글톤으로 관리 (just one instance)

1) bean 적용 안할 시
```java
public class RaceTrack {
  private String location;
  private int miles;
  private String trackType;
}

public class Driver {
  private String name;
  private String team;
  private int yearsExperience;
}
public class RaceRound {
  private String startTime;
  private RaceTrack currentRaceTrack = new RaceTrack(); // new()
  private Driver currentDriver = new Driver(); // new()
}
```

와 같이 new 키워드 사용

2) bean 적용시

```java
@Component
public class RaceTrack {
  private String location;
  private int miles;
  private String trackType;
}

@Component
public class Driver {
  private String name;
  private String team;
  private int yearsExperience;
}

public class RaceRound {
  private String startTime;
  @Autowired
  private RaceTrack currentRaceTrack;
  @Autowired
  private Driver currentDriver;
} // using @Autowired keyword!
```

유저가 직접 new 키워드 등을 통해 객체를 생성하지 않음.


## Bean Component 차이
## Field Injection, Constructor Injection

// https://eng.zemosolabs.com/when-not-to-autowire-in-spring-spring-boot-93e6a01cb793

```
Senior Dev : Why are you using field injection instead of constructor injection?
Junior Dev : What is field injection? I am using @Autowired
```
Types on Dependency Injection
- Field Injection: 위와 같은 @Autowired 사용
- Constructor Injection
- Setter Injection

// constructor Injection
```java
public class CoffeeController {

  private final CoffeeRepository coffeeRepository;

  public CoffeeController(CoffeeRepository coffeeRepo) {
    this.coffeeRepository = coffeeRepo;
  }
}
// no use of annotations. 생성자 부를때 ioc 컨테이너가 주입
```

아직은 이유를 정확하게 모르지만 constructor injection을 추천한다고 함.

(reliable, strict해서)
## @Primary, @Qualifier annotation

<hr>
출처:https://www.baeldung.com/spring-tutorial

https://docs.spring.io/spring-framework/reference/core/beans/definition.html
