### POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?

---

**핵심답변**

 POJO란 객체지향적인 원리에 충실하면서 환경과 기술에 종속되지 않고 필요에 따라 재활용될 수 있는 방식으로 설계된 오브젝트를 의미한다.

Spring Framework에서 POJO는 일반적으로 인터페이스를 상속 받지 않고 getter, setter와 같이 기본적인 기능만 가진 자바 객체입니다.

---

[POJO란](https://www.notion.so/POJO-afefe872d2a54d9c9e841d6da6d22c4f)

### spring IoC/DI의 동작원리 && Spring DI/IoC는 어떻게 동작하나요?

---

**핵심답변**

IoC 기능의 대표적인 동작 원리는 의존관계 주입으로 설계 시점에서는 알 수 없는 런타임 시점에 객체간의 의존관계를 스프링이 결정하고, 컨테이너가 객체 레퍼런스를 제공해주는 것입니다.

DI는 앞서말한 의존관계를 주입하는 것을 의미하는데, A클래스와 B 클래스가 서로 의존관계를 갖는다고 할 때, A클래스가 C인터페이스를 참조하고, B클래스가 C인터페이스를 구현함으로서 느슨한 의존관계 동작을 갖게 됩니다.

---

[spring IoC/DI의 동작원리](https://www.notion.so/spring-IoC-DI-0af6b0ea9e844381a15ece07361b1900)

### IoC 컨테이너의 역할은 무엇이 있을까요?

---

**핵심답변**

- 객체의 생성을 책임지고 생성주기를 관리하며, 의존성을 관리합니다.
- POJO의 생성, 초기화, 서비스, 소멸에 대한 권한을 갖습니다.

---

[[Spring] IoC 컨테이너 (Inversion of Control) 란](https://dev-coco.tistory.com/80)

### Spring IoC/DI(의존성 주입)의 방법에 대해 아는대로 설명해주세요.

---

**핵심답변**

Spring에서는 @Autowired 어노테이션을 이용해 의존성 주입이 가능한데,

- 생성자에 어노테이션을 붙여 의존성 주입을 받는 생성자 주입
- 변수 선언부에 어노테이션을 붙여 의존성 주입을 받는 필드 주입
- Setter 메서드에 어노테이션을 붙여 의존성 주입을 받는 Setter 주입

가 있습니다.

---

****[[Spring] DI(Dependency Injection) 세 가지 방법](https://velog.io/@gillog/Spring-DIDependency-Injection-%EC%84%B8-%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95)****

### 의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.

---

**핵심답변**

- 생성자를 통한 주입은 스프링 레퍼런스에서 권장하는 방법입니다.
- OCP 원칙을 지키며 객체의 불변성을 확보할 수 있게 됩니다.
- 컴파일 시점에 객체를 주입받아 테스트 코드를 작성할 수 있게 됩니다.
- 순환 참조 문제를 애플리케이션 구동 시점에 확인할 수 있게됩니다.

---

[[Spring] 다양한 의존성 주입 방법과 생성자 주입을 사용해야 하는 이유 - (2/2)](https://mangkyu.tistory.com/125)

### MVC 패턴이란?

---

**핵심답변**

웹을 구현할 때 그 구성 요소를 Model, View, Controller의 세가지 역할로 분리시켜서 개발하는 패턴입니다.

****🤔 각 구성 요소의 동작들에 대해 설명부탁드립니다.****

- Model은 모든 데이터에 대한 정보를 알고있고, 이런 정보를 가공할 수 있어야 합니다.
- View는 User에게 보여주고자 하는 모든 것을 화면에 출력하는 역할을 합니다.
- Controller는 데이터와 UI의 소통을 담당하는 역할을 합니다. Model과 View의 경우 서로의 정보를 모르지만, Controller는 Model과 View에 대한 정보를 알고 있습니다.

****🤔 MVC 패턴의 장,단점을 설명해주세요.****

- 개발자들 맡은 부분의 개발에만 집중할 수 있게 해줘서 개발의 효율성이 높아집니다.
- 개발 후에 유지보수 또는 확장성을 보장합니다.

- 하나의 Controller에 다수의 Model과 View가 연결되어 있는 상황이 생길 수 있어 서로의 의존성문제가 발생할 수 있습니다.

****🤔 MVVM 패턴이 뭔지 설명해주세요.****

MVC 패턴에서 Controller를 빼고 ViewModel을 추가한 패턴입니다. MVC패턴의 의존성 문제를 해결하기 위한 패턴으로 ViewModel이 View와의 Data Binding으로 인해 자동으로 갱신됨으로서 Model과 View 독립성을 유지할 수 있게 됩니다.

---

**[일반적인 MVVM 패턴](https://jhtop0419.tistory.com/m/21)**

**[[디자인패턴] MVC 패턴이란?](https://m.blog.naver.com/tlstjd436/222010976665)**

### 프론트 컨트롤러 패턴이란 무엇인가요?

---

**핵심답변**

공통되는 컨트롤러 코드에 대해 애플리케이션의 일괄적인 처리를 위해 만들어진 패턴으로 뷰에서 들어오는 모든 요청을 담당하여 요청에 맞는 컨트롤러를 찾아서 호출시켜주는 역할을 합니다.  스프링에서는 Dispatcher Servlet이 프론트 컨트롤러에 해당합니다.

---

**[[MVC] 프론트 컨트롤러 패턴](https://yeonyeon.tistory.com/103)**

### Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.

---

**핵심답변**

클라이언트로부터 어떠한 요청이 오면 톰캣과 같은 서블릿 컨테이너가 요청을 받게 됩니다. 그리고 이 모든 요청에 대해 디스패처 서블릿은 공통적인 작업을 먼저 처리하고 이외의 작업은 적절한 세부 컨트롤러로 위임합니다.

****🤔 Dispatcher Servlet이 뭔가요?****

가장 앞단에서 HTTP 프로토콜로 들어오는 모든 요청을 가장 먼저 받아 적합한 컨트롤러에 위임해주는 프론트 컨트롤러입니다.

****🤔 Dispatcher Servlet이 모든 요청을 받아드린다면, Dispatcher Servlet이 애플리케이션에 대한 요청과 정적 자원에 대한 요청을 어떻게 구분하나요?****

애플리케이션에 대한 요청을 탐색하고 없으면 정적 자원에 대한 요청을 처리함과 같이 영역을 분리하여 구분하였습니다.

****🤔 Dispatcher Servlet의 동작 과정을 설명해주세요.****

1. 클라이언트의 요청을 디스패처 서블릿이 받습니다.
2. 요청 정보를 통해 요청을 위임할 컨트롤러를 찾습니다.
3. 요청을 컨트롤러로 위임 처리할 핸들러 어댑터를 찾습니다.
4. 핸들러 어댑터가 컨트롤러로 요청을 위임합니다.
5. 비지니스 로직이 처리됩니다.
6. 컨트롤러가 ResponseEntity를 반환합니다.
7. HandlerAdapter가 반환받은 ResponseEntity를 통해 Response 처리를 진행합니다.
8. 서버의 응답을 클라이언트로 반환합니다.

![[https://mangkyu.tistory.com/18](https://mangkyu.tistory.com/18)](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fb1451e5-2225-4b44-8b55-2227065d0d62/Untitled.png)

[https://mangkyu.tistory.com/18](https://mangkyu.tistory.com/18)

---

[[Spring]Dispatcher-Servlet(디스패처 서블릿)이란? 디스패처 서블릿의 개념과 동작 과정](https://mangkyu.tistory.com/18)

[Spring MVC - DispatcherServlet 동작 원리](https://jess-m.tistory.com/15)

### AOP(Aspect Oriented Programming)란 무엇일까요?

---

**핵심답변**

기능을 핵심 기능과 부가 기능으로 분리시키고 각각을 모듈화 하는 기술을 의미합니다.

****🤔 AOP 기술을 적용하는 이유가 뭔가요?****

필수적이지만, 반복적으로 사용되는 코드들을 한 곳에서 유지하고 관리할 수 있게 만들어 리팩토링과 유지보수에 이점을 주기 때문입니다.

****🤔 AOP의 특징에 대해서 설명부탁드립니다.****

- 프록시 패턴 기반이기 때문에, 접근 제어가 가능합니다.
- 프록시가 호출을 인터셉터해서 핵심 로직 전과 후에 부가기능을 수행할 수 있습니다.
- 핵심 기능의 메소드가 호출되는 런타임 시점에만 부가 기능을 적용할 수 있습니다.

****🤔 프록시 패턴이란?****

어떤 객체에 대한 접근을 제어하거나 부가기능을 추가하는 용도로 실제 객체를 대신하는 객체를 제공하는 패턴입니다.

****🤔 프록시 패턴 동작 원리에 대해서 설명해주세요.****

클라이언트가 인터페이스 타입으로 프록시 객체를 사용하게 되고, 프록시는 핵심 기능을 갖는 실제 객체를 감싸서 클라이언트의 요청을 처리하게 됩니다. 이런 특징 덕분에 프록시 패턴은 접근을 제어할 수 있고 부가 기능을 추가할 수 있게 됩니다.

---

[관점지향 프로그래밍(Aspect - Oriented Programming)이란 무엇인가?](https://dev-coco.tistory.com/81)

****[[Spring] AOP(Aspect Oriented Programming)란 무엇일까?](https://devlog-wjdrbs96.tistory.com/398)****

### Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.

---

**핵심답변**

- CorsFilter로 직접 response에 header를 넣어주기
    - 빈으로 등록된 CorsFilter 클래스를 생성합니다.
    - 해당 클래스에 doFilter를 직접 오버라이드해서 Options 메서드에 response로 Access-Control-Allow-Origin헤더에 허용된 Origin이라는 코드를 작성합니다.
- Controller에서 @CrossOrigin 어노테이션 추가해주기
- WebMvcConfigurer를 이용해서 처리하기
    - @Bean으로 Configurer를 추가합니다.

****🤔 CORS가 발생하는 이유에 대해서 설명해주세요.****

CORS는 SOP(Same Origin Policy) 즉, 동일한 출처의 Origin만 리소스를 공유할 수 있다라는 보안 정책 때문에 발생했습니다.

여기서 동일한 Origin이란, 스키마, Host, Port가 같아야합니다.

****🤔 CORS 해결 방법****

- HTTP 통신 헤더인 Origin 헤더에 요청을 보내는 곳의 정보를 담고 서버로 요청을 보냅니다.
- 이후 서버는 Access-Control-Allow-Origin헤더에 허용된 Origin이라는 정보를 담아 보냅니다.
- 클라이언트는 헤더의 값과 비교해 정상 응답임을 확인하고 지정된 요청을 보냅니다.
- 서버는 요청을 수행하고 200OK 코드를 응답합니다.

****🤔 Preflight 란?****

요청 거부로 인해 불필요한 작업을 줄이고자, 클라이언트가 사전에 서버에서 어떤 메서드와 어떤 header를 허용하는지 확인하는 과정입니다.

기본적으로 브라우저에서 OPTIONS 메서드로 preflight를 전송합니다.

---

**[[Spring Boot] CORS 를 해결하는 3가지 방법 (Filter, @CrossOrigin, WebMvcConfigurer)](https://wonit.tistory.com/572)**

****[[Spring Boot] CORS와 Preflight에 관한 이슈](https://velog.io/@change/Spring-Boot-CORS%EC%99%80-Preflight%EC%97%90-%EA%B4%80%ED%95%9C-%EC%9D%B4%EC%8A%88)****