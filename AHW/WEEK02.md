# 2주차

### Spring

- **MVC 패턴이란?**
  - 구성요소:
    1. Model - 핵심적인 비즈니스 로직을 담당하여 데이터베이스를 관리 or Java의 POJO
    2. View - 사용자에게 보여주는 화면 (Model에 포함된 데이터의 시각화)
    3. Controller - 모델과 뷰 사이에서 정보 교환을 할 수 있도록 연결시켜주는 역할
  - 장점
    1. 코드의 재사용에 유용, 사용자 interface와 응용 프로그램 개발에 소요되는 시간 단축
[](https://kim6394.tistory.com/161)
  
  **💡 스프링 MVC 구조 흐름에 대해서 과정대로 설명해보세요**
  
    ![image](https://user-images.githubusercontent.com/90819869/153923252-67a1e44f-f7e0-4069-9ec0-aef485845fe3.png)
    
    1. `Dispatcher Servlet(DS)`이 클라이언트로부터 요청을 받는다
    2. DS가 `Handler Mapping`에게 처리를 요청할 핸들러(`Controller`) 이름을 묻는다
    3. 핸들러 맵핑은 요청 URL을 보고 핸들러 이름을 DS에게 알려준다 (이 때, 핸들러를 실행하기 전/후에 처리할 것들을 인터셉터로 만들어 줌)
    4. DS가 해당 핸들러에게 제어권을 넘겨준다
    5. 해당 핸들러가 응답에 필요한 서비스 호출 및 렌더링해야 하는 `View` 이름 판단 후 DS에게 전송한다
    6. DS가 받은 뷰 이름을 `View Resolver`에게 전달해 응답에 필요한 뷰를 만들라고 명령한다
    7. 뷰 리졸버에게 응답에 필요한 뷰를 받는다
    8. DS는 해당 뷰에 모델과 컨트롤러를 보낸다
    9. 뷰는 DS에게 받은 모델과 컨트롤러를 활용해 원하는 응답 생성 후 다시 보내준다
    10. DS는 뷰로부터 받은 것을 클라이언트에게 응답한다
[](https://hongjuzzang.github.io/web/web_spring/)

---
- **프론트 컨트롤러 패턴이란 무엇인가요?**
  - 프론트 컨트롤러란? 주로 서블릿 컨테이너의 제일 앞에서 서버로 들어오는 클라이언트의 모든 요청을 받아 처리해주는 컨트롤러
  - 구조
    - 기존 패턴
    - ![image](https://user-images.githubusercontent.com/90819869/153976572-3eb68212-1225-4e1b-b430-ab4b2e1e03b5.png)
      - 각 클라이언트들은 Controller A, B, C에 대해 각각 호출한다.
      - 공통 코드들은 별도로 처리되어 있지 않고 각 Controller에 포함되어 있다.
    - 프론트 컨트롤러 패턴
    -  ![image](https://user-images.githubusercontent.com/90819869/153976771-7c6dad1f-480b-4883-82a0-d411f654f785.png)
      - Front Controller은 각 요청에 맞는 컨트롤러를 찾아서 호출
      - 공통 코드에 대해서는 Front Controller에서 처리하고, 서로 다른 코드들만 각 Controller에서 처리할 수 있도록 한다.
  - 장점
    1. 공통된 부분을 처리해주는 FrontController로 중복을 줄일 수 있음
    2. Front Controller 외 다른 Controller에서 Servlet 사용하지 않아도 됨
[](https://yeonyeon.tistory.com/103)

---
- **Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.**
  - DS란? Spring MVC 패턴에서 기본적으로 사용하는 Servlet으로, 클라이언트의 요청이 있을 시 가장 앞단에서 요청을 가로채어(Front Controller) 요청에 매핑되는 Controller에 작업을 전달하고 비지니스 로직 처리 후 해당 결과 View를 클라이언트에 전달하는 역할
  - ![image](https://user-images.githubusercontent.com/90819869/153977295-1d36b55b-2045-44cb-a0ef-d9d9b64f8e66.png)
  - (상기 내용 참고)

---
- **POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?**
  - Plain Old Java Object(오래된 방식의 자바 오브젝트)의 약자
  - 다른 클래스나 인터페이스를 상속/implements 받아 메서드가 추가된 클래스가 아닌 일반적으로 우리가 알고 있는 getter, setter 같이 기본적인 기능만 가진 자바 객체이다
  - 자바의 기본 객체 예시:
  - ```public class User {
    private int id;
    private String name;
    private String email;
    
    public int getId() {
    	return id;
    }
    public String getName() {
    	return name;
    }
    public String getEmail() {
    	return email;
    }
    
    public void setId(int id) {
    	this.id = id;
    }
    public void setName(String name) {
    	this.name = name;
    }
    public void setEmail(String email) {
    	this.email = email;
    }
  - 장점:
    1. 코드의 간결함 (비즈니스 로직과 특정 환경/low 레벨 종속적인 코드를 분리하므로 단순하다.)
    2. 자동화 테스트에 유리 (환경 종속적인 코드는 자동화 테스트가 어렵지만, POJO는 테스트가 매우 유연하다.
    3. 객체지향적 설계의 자유로운 사용

[](https://limmmee.tistory.com/8)

---
- **Spring IoC/DI의 동작원리**
  - Spring DI/IoC는 어떻게 동작하나요?
    - `DI(Dependency Injection)`란 스프링이 다른 프레임워크와 차별화되어 제공하는 의존 관계 주입 기능
      - 객체를 직접 생성하는 게 아니라 외부에서 생성한 후 주입 시켜주는 방식
      - DI(의존성 주입)를 통해서 모듈 간의 결합도가 낮아지고 유연성이 높아진다
      - ![image](https://user-images.githubusercontent.com/90819869/153978454-2fc1cdde-ba58-4b85-968a-f33d5f7da2b6.png)
      - A 객체에서 B, C객체를 사용(의존)할 때 A 객체에서 직접 생성 하는 것이 아니라 외부(IOC컨테이너)에서 생성된 B, C객체를 조립(주입)시켜 setter 혹은 생성자를 통해 사용하는 방식이다
      - 장점:
        1. 클래스들 간 의존 관계를 최소화 할 수 있다.
        2. 프로젝트 유지보수가 용이하다.
        3. 기존에는 개발자가 직접 객체의 생성과 소멸을 제어했는데 DI로 인해 객체의 생성과 소멸 등 클래스간 의존관계를 스프링 컨테이너가 제어해준다.
  - IoC 컨테이너의 역할은 무엇이 있을까요?
    - 객체의 생성을 책임지고, 의존성 관리
    - POJO의 생성, 초기화, 서비스, 소멸에 대한 권한 有
    - (개발자들이 직접 할 수 있지만) POJO의 생성을 컨테이너에게 맡길 수 있다
    - ![image](https://user-images.githubusercontent.com/90819869/153978905-648cae1e-27c3-4ca3-ac17-e048adf572f3.png)
[](https://velog.io/@gillog/Spring-DIDependency-Injection)

---
- **Spring IoC/DI(의존성 주입)의 방법에 대해 아는대로 설명해주세요.**
  - 각 DI 주입 방식의 차이점과 이점에 대해서 설명해주세요.
    1. Field Injection(필드 주입)
      - 변수 선언부에 @Autowired Annotation
    3. Setter Injection(수정자 주입)
      - set Method를 정의해서 사용
    5. Constructor Injection(생성자 주입)
      - Constructor에 @Autowired Annotation을 붙여 의존성을 주입받을 수 있다
  - 의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.
    1. 생성자 호출시점에 딱 1번만 호출되는 것이 보장됨
    2. 생성자 주입은 객체를 생성할 때 딱 1번만 호출되므로 이후에 호출되는 일이 없음. 따라서 불변하게 설계할 수 있다
      - [](https://woodcock.tistory.com/8)
      - [](https://yaboong.github.io/spring/2019/08/29/why-field-injection-is-bad/)
---
- **AOP(Aspect Oriented Programming)란 무엇일까요?**

---
- **Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.**

---
- Bean에 대해 설명해보세요.
  - Spring Bean이란 무엇인가요?
    - 스프링에서는 객체를 Bean이라고 부르며, 프로젝트가 실행될때 사용자가 Bean으로 관리하는 객체들의 생성과 소멸에 관련된 작업을 자동적으로 수행해주는데 객체가 생성되는 곳을 스프링에서는 Bean 컨테이너라고 부른다
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
