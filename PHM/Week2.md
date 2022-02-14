# [2주차] Spring

## Spring Framework

## 스프링 프레임워크란?
### 핵심답변

#### 🤔 스프링 프레임워크의 종류: Spring, Spring MVC, Spring Boot, Spring Data JPA, Spring AOP

<br><br>
## 스프링 프레임워크의 특징
### 핵심답변

#### 🤔 POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?
    POJO란, Plan Old Java Object의 약자로, 다른 클래스나 인터페이스를 상속받지 않은, 기본적인 기능만 가진 자바객체를 말합니다.
    POJO의 특징으로는, 특정 규약(Contract)에 종속되지 않아야하며(JAVA언어와 꼭 필요한 API외에 종속되지 않아야한다.), 특정환경에 종속되지 않고 객체지향원리에 충실해야한다가 있습니다.
    POJO를 사용하는 이유로는, 종속된 코드를 분리함으로 코드의 간결함과 자동화 테스트의 유리, 객체지향적 설걔의 자유로운 사용이 있습니다.

    Spring은 가장 대표적인 POJO프레임워크이며, POJO란 객체지향적인 원리에 충실한 방식으로 설걔된 오브젝트입니다.
<Br>
참고      
[POJO에 대하여](https://limmmee.tistory.com/8)

<Br><br>
## spring IoC/DI의 동작원리**
### 핵심답변

IOC는 제어의 역전을 의미합니다.제어의 역전이란, 객체가 자신이 사용할 객체를 스스로 선택하지 않으며 생성하지 않으며 모든 제어 권한을 외부에서 결정된다는 것을 의미합니다.   
Spring framwork는 객체에대한 생성 및 생명주기를 관리할 수 있는 IOC 컨테이너를 제공하고있습니다.    
DI란, 스프링 IOC 기능의 대표적인 동작원리이며, 객체간의 의존성을 자신이 아닌 외부에서 주입하는 개념입니다.   

<Br><br>

#### 🤔 Spring DI/IoC는 어떻게 동작하나요?
IOC 컨테이너에서 관리하는 객체를, DI를 통해 내부에 의존성을 주입함으로써, 내부에서 해당 객체의 기능을 사용할 수 있도록 합니다.   

<Br><br>

#### 🤔 IoC 컨테이너의 역할은 무엇이 있을까요?
컨테이너란, 보통 객체의 생명주기를 관리, 생성된 인스턴스들에게 추가적인 기능을 제공하도록 하는 것 입니다.
스프링에서는 IOC 컨테이너가, 객체의 생성과 관리를 책임지고 의존성을 관리해줌으로써 개발자가 로직에 집중할 수 있도록 해줍니다.

Spring IOC 컨테이너의 역할
1. IoC 컨테이너는 객체의 생성을 책임지고, 의존성을 관리한다.
2. POJO의 생성, 초기화, 서비스, 소멸에 대한 권한을 가진다.


<Br><br>

## Spring IoC/DI(의존성 주입)의 방법에 대해 아는대로 설명해주세요.
### 핵심답변
1. 수정자 주입(Setter Injection)
2. 필드 주입(Field Injection)
3. 생성자 주입(Constructor Injection)

<Br><br>

#### 🤔  각 DI 주입 방식의 차이점과 이점에 대해서 설명해주세요.
1. 수정자 주입(Setter Injection)은 선택적인 의존성을 사용할 때 유용합니다. setter 메소드를 사용하기때문에, 런타임시 의존관걔를 주입해 낮은 결합도를 가진다는 장점이 있지만,
setter 메소드를 사용해 의존성을 주입해 주지 않아도, 메인 객체가 생성되어 NullPointException이 발생할 수다는 문제점이 있습니다.
   ```java
   @Component
   public class SampleController {
      private SampleService sampleService;

      @Autowired
      public void setSampleService(SampleService sampleService) {
         this.sampleService = sampleService;
      }
   }
2. 필드 주입(Field Injection)은 변수 선언부에 @Autowired 어노테이션을 이용하여 사용합니다.
   @Autowired를 사용하여 자동으로 의존성이 주입되기 때문에 간편하지만, 참조 관꼐를 눈으로 확인하기 어렵고, 너무 많은 필드 주입을 하게되면 참조관계과 꼬일 수 있다는 단점이 있습니다.
3. 생성자 주입(Contructor Injection)은 선언된 갹채를, 생성자를 이용하여 의존성을 주입하는 방법입니다.
    생성자 주입을 사용할때의 이점으로는 2가지가 있습니다.
   1. Null을 주입하지 않는 이상, NullPointException이 발생하지 않습니다.
   2. 의존관계를 주입하지 않은 경우 해당 객체를 생성할 수 없다. 즉, 의존관계에 대한 내용을 외부로 노출시킴으로써 컴파일 타임에 오류를 잡아낼 수 있습니다.
   3. final을 사용할 수 있어, 선언과 동시에 초기화 되어야 합니다. 
   ```java
    public class Controller {
      private final Service service; // final 추가
    
      public Controller(Service service) {
        this.service = service;
      }
    
      public void callService() {
        service.doSomething();
      }
    }
    ```
   <br><br>

#### 🤔  의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.

생성자 주입을 사용하면, 컨테이너가 빈을 생성하는 시점에서 객체생성에 사이클 관계가 생기기 때문에 객체 간 순환참조를 하고있는 경우   
스프링 어플리케이션이 구동이 되지 않습니다.
하지만 , 필드 주입이나, 수정자 주입은 객체 생성 후 비지니스 로직 상에서 순환참조가 일어나기 때문에 객체 생성시점에는 순환참조가 일어나는지 아닌지 발견할 수 있는 방법이 없습니다.

<br>
    
참고    
[IOC와 DI에 대하여](https://mo-world.tistory.com/entry/IOC%EC%99%80-DI-%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC-%EC%8A%A4%ED%94%84%EB%A7%81-%EA%B0%9C%EB%85%90-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-%EC%89%BD%EA%B2%8C-%EC%84%A4%EB%AA%85)    
[IOC 컨테이너](https://dev-coco.tistory.com/80)   
[생성자 주입을 사용해야하는이유](https://yaboong.github.io/spring/2019/08/29/why-field-injection-is-bad/)

<br><br>

## MVC 패턴이란?
### 핵심답변

Model-View-Controller로 나누어진 디자인 패턴
<Br><br>

#### 🤔 프론트 컨트롤러 패턴이란 무엇인가요?
프론트 컨트롤러란, 뷰에서 들어오는 모든 요청을 담당하여 웹 어플리케이션을 실행하는 모든 요청을 일괄적으로 처리할 수 있도록 해주는 디자인 패턴 입니다.
![image](https://user-images.githubusercontent.com/42319300/153901444-5b4ebf17-4f91-4e5d-8c99-045566f72a91.png)
<Br><br>

#### 🤔 Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.
Dispatcher Servlet이란, Spring MVC에서 프론트 컨트롤러 패턴을 구현한 Servlet입니다.

1. 클라이언트가 url을 요청하면, 웹 브라우저에서 스프링으로 request가 보내집니다.
2. Dispatcher Servlet이 request를 받으면, Handler Mapping을 통해 해당 url을 담당하는 Controller를 탐색 후 찾아냅니다.
3. 찾아낸 Controller로 request를 보내주고, 보내주기 위해 필요한 Model을 구성합니다.
4. Model에서는 페이지 처리에 필요한 정보들을 Database에 접근하여 쿼리문을 통해 가져옵니다.
5. 데이터를 통해 얻은 Model 정보를 Controller에게 response 해주면, Controller는 이를 받아 Model을 완성시켜 Dispatcher Servlet에게 전달해줍니다.
6. Dispatcher Servlet은 View Resolver를 통해 request에 해당하는 view 파일을 탐색 후 받아냅니다.
7. 받아낸 View 페이지 파일에 Model을 보낸 후 클라이언트에게 보낼 페이지를 완성시켜 받아냅니다.
8. 완성된 View 파일을 클라이언트에 response하여 화면에 출력합니다.

![image](https://user-images.githubusercontent.com/42319300/153902623-5aa34db5-749b-4a9f-bade-81eaa2ae5ab3.png)
<Br><br>

#### 🤔  Spring Web MVC에서 요청 마다 Thread가 생성되어 Controller를 통해 요청을 수행할텐데,  어떻게 1개의 Controller만 생성될 수 있을까요?

## AOP
    
#### 🤔 AOP(Aspect Oriented Programming)란 무엇일까요?
AOP란 Aspect Oriented Programming, 관점 지향 프로그래밍을 의미합니다.   
관점지향이란, 어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 각각 모듈화하는 프로그래밍 기법을 의미합니다.   
따라서 AOP는 핵심기능과 부가기능을 나누어서 설계, 구현하는 것을 의미합니다.

![image](https://user-images.githubusercontent.com/42319300/153905949-7ab73ff7-59a3-4445-a994-5cd39f439a61.png)
<br>

참고    
[AOP란](https://thalals.tistory.com/271)

#### 🤔 Autowiring 에 대해서 설명해주세요

## Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.

## Bean에 대해 설명해보세요.
    - **Spring Bean이란 무엇인가요?**
    - **스프링 Bean의 생성 과정을 설명해주세요.**
    - **스프링 Bean의 Scope에 대해서 설명해주세요.**
    - **Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.**
- **Getter와 Setter를 사용해야하는 이유에 대해서 설명해주세요.**
- Spring에서 데이터를 받는 방식(과정)과 종류에 대해서 설명해주세요.
- **Spring에서 예외처리하는 방법에 대해서 설명해주세요.**
    - Spring Boot의 예외처리의 내부 구현은 어떻게 되어 있나요?
- **DTO를 사용하는 이유?**
    - DAO와 DTO의 차이를 설명해주세요
- **Filter와 Interceptor 차이**
    - **Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?**
- Spring Application을 구동할 때 메서드를 실행시키는 방법에 대해 설명해주세요.

## JPA

- JPA란?
- **JPA를 사용할 때의 이점에 대해서 설명해주세요.**
- JPA 영속성 컨텍스트의 이점(5가지)를 설명해주세요.
- **JPA에서 N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.**
- JPA를 사용할 때 쿼리를 사용하는 방법에 대해서 설명해주세요.
