# 2주차

## Spring Framework
### Spring
- POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?
- spring IoC/DI의 동작원리
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

<br><br>

### POJO란 무엇인가요?
---

****핵심답변****

"Plain Old Java Object" 오래된 방식의 간단한, 지극히 평범한 자바 객체라는 의미입니다.     
특정 규약이나 환경에 종속되어서는 안되고 객체지향 설계를 잘 지켜야 한다는 조건이 있습니다.

<br>

**🤔 Spring Framework에서 POJO는 무엇이 될 수 있을까요?**   
Spring Framework는 기존 프레임워크인 EJB(Enterprise Java Beans)등의 복잡성을 해결하여    
생산성을 향상시켰다는 의의가 있습니다. 따라서 Getter와 Setter를 이용한 가장 기본적인 자바 객체만으로    
구성된 기본 클래스를 Spring Framework에서 POJO라 할 수 있습니다.

---
<br><br>

### Spring DI/IoC는 어떻게 동작하나요?

---
****핵심 답변****

1.DI(Dependency Injection)    
Dependency는 A 객체가 B 객체를 의존한다고 할 때, 의존의 대상이 되는 B 객체가 변하면 A 객체도 영향을 받는 관계를 말합니다.    
그런데, 클래스와 클래스 사이에 직접적인 의존성을 갖게 만들면 결합도(coupling)가 높아집니다.    
결합도가 높아지면 한 클래스의 수정 사항 발생 시 의존성이 있는 다른 클래스의 수정도 불가피하므로 코드의 재활용성과 유연함이 떨어집니다.    
따라서 이를 해결하기 위해 class간의 직접적인 의존관계가 아닌 interface의 활용(생성자 혹은 setter 사용)을 통해    
외부에서 생성된 객체를 주입합니다. 이렇게 하면 결합도는 낮추면서도 런타임시에 의존관계가 결정되기 때문에 유연한 개발이 가능합니다.     
<br>
2.IoC(Inversion of Control)   
IoC는 프로그램의 제어 흐름 구조가 바뀌는 것을 말합니다.   
일반적인 프로그램의 흐름은 main() 메서드가 다음 사용할 객체를 결정하고, 결정된 객체를 생성하고,   
생성된 객체 내의 메서드를 호출하고, 객체 내 호출된 메서드가 다음 사용할 객체를 호출하는 식으로 진행됩니다.   
그러나 DI가 이루어지면 주입된 의존성으로 인해 객체가 자신이 사용할 다른 객체를 선택하거나 생성하지 않습니다.
일반적인 경우와 반대되는, '역전된' 제어가 일어나는 것입니다.   
![](https://images.velog.io/images/apolontes/post/ada9e4f1-fac2-46d5-9cea-b90ec1f45050/2022-02-14_21-49-05.png)


<br><br>

**🤔 IoC 컨테이너의 역할은 무엇이 있을까요?**   
컨테이너는 객체의 생명 사이클을 관리하고, 생성된 인스턴스들에게 추가적인 기능을 제공하도록 하는 것입니다.   
IoC 컨테이너는 스프링 프레임워크에서 이와 같은 역할을 합니다. 또한 POJO의 생성, 초기화, 서비스, 소멸에 관한    
권한을 가지고 있어 개발자들은 IoC 컨테이너에게 이를 맡기고 비즈니스 로직에 집중할 수 있습니다. 

---
<br><br>

### Spring IoC/DI(의존성 주입)의 방법에 대해 아는대로 설명해주세요.
---

****핵심답변****
1.필드 주입(Field Injection)   
가장 흔히 볼 수 있는 주입 방법으로, 사용하기 간편하고 코드를 읽기 쉽습니다.    
```java
@Service
public class BookService {
    @Autowired
    private BookRepository repository;

    public BookService() {
    }
}
```
2.수정자 주입(Setter Injection)   
선택적인 의존성 주입이 필요할 때 유용합니다.   
(필수적인 의존성을 주어야 하는 곳에서 사용하면 NullPointerException이 발생하므로    
null에 대한 검증 로직을 모든 필드에 추가해야 함)   
```java
@Service
public class BookService {
    private BookRepository repository;

    public BookService() {
    }

    @Autowired
    public void setRepository(BookRepository bookRepository) {
        this.repository = bookRepository;
    }
}
```   
3.생성자 주입(Constructor Injection)   
별다른 annotation 없이 매개변수 생성자를 열어두면 사용할 수 있는 방식입니다.    
```java
@Service
public class BookService {
    private final BookRepository repository;

    public BookService(BookRepository repository) {
        this.repository = repository;
    }
}
```   

<br><br>

**🤔 각 DI 주입 방식의 차이점과 이점에 대해서 설명해주세요.**
1.생성자 주입    
-장점: 필수적으로 사용해야 하는 레퍼런스 없이 인스턴스를 만들지 못하게 강제합니다.    
순환 참조 의존성을 체크하기 용이합니다. 테스트 코드 작성시 생성자를 통한 의존성 주입이 용이합니다.    
-단점: 어쩔 수 없는 순환 참조는 생성자 주입으로 해결하기 어렵습니다.    
<br>
2.필드 주입      
-장점: 가장 간단하게 선언하는 방식입니다.   
-단점: 의존 관계가 눈에 잘 보이지 않아 추상적이고, 따라서 의존성이 과도하게 복잡해질 수 있습니다.    
또한 단위 테스트 시 의존성 주입이 용이하지 않습니다.
 <br>
3.수정자 주입    
-장점: 의존성이 선택적으로 필요한 경우에 사용할 수 있어 자칫 과도하게 복잡해질 수 있는 상황을    
해결할 수 있습니다.
-단점: 의존성 주입 대상 필드가 final 선언이 불가합니다.     
<br><br>

**🤔 의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.**

<br><br>

---
