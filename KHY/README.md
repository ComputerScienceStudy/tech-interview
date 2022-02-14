# Tech Interview
## [Java](https://github.com/ComputerScienceStudy/tech-interview/blob/main/KHY/Content/Java.md)
- JVM 동작 과정/원리
- GC(Garbage Collector)의 종류와 동작 과정/원리
- Java 언어 기초
    - 정적 타입 언어와 동적 타입 언어의 차이
    - Java 코드의 컴파일 과정
    - 각 변수 타입이 몇 byte인지, primitive type과 reference type 인지
    - overriding vs overloading 개념과 활용
    - 접근자 종류와 기능
    - final 키워드
    - Generic의 개념
    - ThreadLocal이 무엇이고 언제 활용되는지
    - static이란 무엇인가요?
      - java의 non-static 멤버와 static 멤버의 차이 
      - java의 main 메서드가 static인 이유
    - Wrapper Class란 무엇인가요?
    - Lombok
- 객체지향
    - 객체지향에 대해서 설명해주세요. 
    - SOLID(객체지향 5대원칙)에 대해서 설명해주세요.
- 오류처리
    - Checked Exception과 Unchecked Exception에 대해 설명해주세요. 스프링 트랜잭션 추상화에서 rollback 대상은 무엇일까요?
    - 자바의 동시성 이슈(공유자원 접근)에 대해 설명해주세요. 
    - 자바에서 null을 안전하게 다루는 방법에 대해 설명해주세요.

## [Spring Framework](https://github.com/ComputerScienceStudy/tech-interview/blob/main/KHY/Content/Spring.md)
### Spring
- POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?
- Spring DI/IoC는 어떻게 동작하나요?
  - IoC 컨테이너의 역할은 무엇이 있을까요?
- Spring IoC/DI(의존성 주입)의 방법에 대해 아는대로 설명해주세요.
  - 각 DI 주입 방식의 차이점과 이점에 대해서 설명해주세요.
  - 의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.
- MVC 패턴이란?
- 프론트 컨트롤러 패턴이란 무엇인가요?
- Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.
- AOP(Aspect Oriented Programming)란 무엇일까요?
- Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.
- Bean에 대해 설명해보세요.
  - Spring Bean이란 무엇인가요?
  - 스프링 Bean의 생성 과정을 설명해주세요.
  - 스프링 Bean의 Scope에 대해서 설명해주세요.
  - Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.
- Getter와 Setter를 사용해야하는 이유에 대해서 설명해주세요.
- Spring에서 예외처리하는 방법에 대해서 설명해주세요.
- Filter와 Interceptor 차이
  - Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?
- DTO를 사용하는 이유
### JPA
- JPA를 사용할 때의 이점에 대해서 설명해주세요.
- JPA에서 N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.
