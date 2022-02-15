# Spring Framework

## Spring

### POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?

---

**핵심답변**

 POJO란 객체지향적인 원리에 충실하면서 환경과 기술에 종속되지 않고 필요에 따라 재활용될 수 있는 방식으로 설계된 오브젝트를 의미한다.

Spring Framework에서 POJO는 일반적으로 인터페이스를 상속 받지 않고 getter, setter와 같이 기본적인 기능만 가진 자바 객체입니다.

---

>[POJO란](https://www.notion.so/POJO-afefe872d2a54d9c9e841d6da6d22c4f)

<br>
<br>

### spring IoC/DI의 동작원리 && Spring DI/IoC는 어떻게 동작하나요?

---

**핵심답변**

IoC 기능의 대표적인 동작 원리는 의존관계 주입으로 설계 시점에서는 알 수 없는 런타임 시점에 객체간의 의존관계를 스프링이 결정하고, 컨테이너가 객체 레퍼런스를 제공해주는 것입니다.

DI는 앞서말한 의존관계를 주입하는 것을 의미하는데, A클래스와 B 클래스가 서로 의존관계를 갖는다고 할 때, A클래스가 C인터페이스를 참조하고, B클래스가 C인터페이스를 구현함으로서 느슨한 의존관계 동작을 갖게 됩니다.

---

>[spring IoC/DI의 동작원리](https://www.notion.so/spring-IoC-DI-0af6b0ea9e844381a15ece07361b1900)

<br>
<br>

### IoC 컨테이너의 역할은 무엇이 있을까요?

---

**핵심답변**

- 객체의 생성을 책임지고 생성주기를 관리하며, 의존성을 관리합니다.
- POJO의 생성, 초기화, 서비스, 소멸에 대한 권한을 갖습니다.

---

>[[Spring] IoC 컨테이너 (Inversion of Control) 란](https://dev-coco.tistory.com/80)

<br>
<br>

### Spring IoC/DI(의존성 주입)의 방법에 대해 아는대로 설명해주세요.

---

**핵심답변**

Spring에서는 @Autowired 어노테이션을 이용해 의존성 주입이 가능한데,

- 생성자에 어노테이션을 붙여 의존성 주입을 받는 생성자 주입
- 변수 선언부에 어노테이션을 붙여 의존성 주입을 받는 필드 주입
- Setter 메서드에 어노테이션을 붙여 의존성 주입을 받는 Setter 주입

가 있습니다.

---

>[[Spring] DI(Dependency Injection) 세 가지 방법](https://velog.io/@gillog/Spring-DIDependency-Injection-%EC%84%B8-%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95)

<br>
<br>

### 의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.

---

**핵심답변**

- 생성자를 통한 주입은 스프링 레퍼런스에서 권장하는 방법입니다.
- OCP 원칙을 지키며 객체의 불변성을 확보할 수 있게 됩니다.
- 컴파일 시점에 객체를 주입받아 테스트 코드를 작성할 수 있게 됩니다.
- 순환 참조 문제를 애플리케이션 구동 시점에 확인할 수 있게됩니다.

---

>[[Spring] 다양한 의존성 주입 방법과 생성자 주입을 사용해야 하는 이유 - (2/2)](https://mangkyu.tistory.com/125)

<br>
<br>

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

>[일반적인 MVVM 패턴](https://jhtop0419.tistory.com/m/21)

>[[디자인패턴] MVC 패턴이란?](https://m.blog.naver.com/tlstjd436/222010976665)

<br>
<br>

### 프론트 컨트롤러 패턴이란 무엇인가요?

---

**핵심답변**

공통되는 컨트롤러 코드에 대해 애플리케이션의 일괄적인 처리를 위해 만들어진 패턴으로 뷰에서 들어오는 모든 요청을 담당하여 요청에 맞는 컨트롤러를 찾아서 호출시켜주는 역할을 합니다.  스프링에서는 Dispatcher Servlet이 프론트 컨트롤러에 해당합니다.

---

>[[MVC] 프론트 컨트롤러 패턴](https://yeonyeon.tistory.com/103)

<br>
<br>

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

![image](https://user-images.githubusercontent.com/82690689/153920718-d57055fb-c278-47c8-94e8-9febe440e96b.png)

---

>[[Spring]Dispatcher-Servlet(디스패처 서블릿)이란? 디스패처 서블릿의 개념과 동작 과정](https://mangkyu.tistory.com/18)

>[Spring MVC - DispatcherServlet 동작 원리](https://jess-m.tistory.com/15)

<br>
<br>

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

>[관점지향 프로그래밍(Aspect - Oriented Programming)이란 무엇인가?](https://dev-coco.tistory.com/81)

****[[Spring] AOP(Aspect Oriented Programming)란 무엇일까?](https://devlog-wjdrbs96.tistory.com/398)****

<br>
<br>

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

>[[Spring Boot] CORS 를 해결하는 3가지 방법 (Filter, @CrossOrigin, WebMvcConfigurer)](https://wonit.tistory.com/572)

>[[Spring Boot] CORS와 Preflight에 관한 이슈](https://velog.io/@change/Spring-Boot-CORS%EC%99%80-Preflight%EC%97%90-%EA%B4%80%ED%95%9C-%EC%9D%B4%EC%8A%88)


### Bean에 대해 설명해보세요.

---

**핵심답변**

JAVA Bean은 특정 형태의 클래스를 가르키는 뜻으로 사용됩니다. 일반적으로 DTO가 JAVA Bean이라고 생각하면 됩니다. 

모든 필드가 private로 구성되어 있어 getter와 setter을 통해서만 접근할 수 있고, 전달 인자가 없는 생성자를 가지는 형태(no-argument)의 클래스입니다. 일반적으로 POJO와 거의 동일한 개념이라고 이해하면 됩니다.

****🤔 Spring Bean이란 무엇인가요?****

Spring IoC 컨테이너가 관리하는 자바 객체로 Container에 의해 생명주기가 관리되는 객체를 의미합니다. 

****🤔 스프링 Bean의 생성 과정을 설명해주세요.****

1. 객체 생성
2. 의존 설정
3. 초기화
4. 사용
5. 소멸

스프링 컨테이너가 초기화 될 때, 먼저 빈 객체를 설정 정보에 맞춰 생성합니다. 의존 관계를 설정한 뒤에 해당 프로세스가 완료되면 빈 객체가 지정한 메서드를 호출해서 초기화 합니다.  객체를 사용한 뒤 컨테이너가 종료 될 때, 빈이 지정한 메서드를 호출해 소멸 과정을 진행합니다.

****🤔 스프링 Bean의 Scope에 대해서 설명해주세요.****

Bean이 존재하는 범위를 뜻하는 말로, 기본적으로 Spring Bean은 하나의 객체만 생성하는 싱글톤의 범위를 갖고 있습니다. 그 외의 Scope로는 매번 새로운 객체를 생성하는 prototype이 있습니다.

****🤔 Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.****

두 어노테이션 모두 IoC 컨테이너에 빈을 등록하게 해주는 어노테이션입니다.

Bean 어노테이션의 경우 메서드 단위로 선언하며 일반적으로 개발자가 컨트롤할 수 없는 외부 라이브러리 사용시에 사용합니다.

Component 어노테이션의 경우는 클래스 단위로 선언되며, 개발자가 직접 컨트롤이 가능한 내부 클래스에 사용됩니다.

---

### Getter와 Setter를 사용해야 하는 이유에 대해서 설명해주세요.

---

**핵심답변**

객체의 무결성을 지키기 위함입니다. 

예를들어 만약 외부에서 몸무게라는 필드에 직접 접근한다면, 0보다 낮은 값을 줄 수도 있습니다. 이렇게 된다면, 객체의 무결성이 깨지기 때문에 이를 방지하기 위해 Getter를 사용해 본 필드의 값을 숨긴채 내부에서 가공된 값을 꺼내고, Setter를 사용해 전달받은 값을 내부에서 가공해 필드에 넣어주는 방식을 사용하게 됬습니다.

****🤔 무결성이란?****

데이터의 정확성과 일관성을 유지하고 보증하는 것

ex) 물건의 가격은 음수 일 수 없다.

```java
// set 함수를 통해 무결성 지키기
public void SetPrice() { 
  if(price >= 0) {
	  price = price; 
  } else {
  	  throw new IllegalArgumentException("가격은 음수가 될 수 없습니다.");
}
```

---

### Spring에서 예외처리하는 방법에 대해서 설명해주세요.

---

**핵심답변**

스프링에서는 예외를 처리하는 핸들러들을 추상화한 HandlerExceptionResolver 인터페이스를 만들었습니다.  이 인터페이스의 구현체들은 빈으로 등록되어 발생한 예외를 가로채서 처리하게 됩니다.  스프링에서는 다양한 HandlerExceptionResolver 인터페이스 구현체들을 빈으로 등록함으로써 발생한 예외 방식에 맞는 ExceptionResolver가 예외 처리를 진행하도록 만들어 줍니다. 스프링에서는 기본적으로 아래의 4가지 EsceptionResolver 구현체들이 빈으로 등록됩니다.

- DefaultErrorAttributes: 에러 속성을 저장하며 직접 예외를 처리하지는 않는다.
- DefaultHandlerExceptionResolver: 스프링의 예외들을 처리한다.
- ResponseStatusExceptionResolver: @ResponseStatus 또는 ResponseStatusException에 의한 예외를 처리한다.
- ExceptionHandlerExceptionResolver: Controller나 ControllerAdvice에 있는 ExceptionHandler에 의한 예외를 처리한다.

1. 컨트롤러에서 예외처리가 던져졌을 때, 스프링에서는 예외가 발생한 컨트롤러 안에 @ExceptionHandler가 있는지 검사합니다.
2. 만약 @ExceptionHandler에서 처리 불가능하다면, ControllerAdvice를 찾고 해당 클래스 안에 @ExceptionHandler가 있는지 검사하여 해당 @ExceptionHandler가 발생한 예외를 처리할 수 있다면 에러 응답을 제공합니다.
3. 만약 ControllerAdvice에도 예외가 구현되어 있지 않다면 @ResponseStatus가 있는지 확인합니다. 만약 있다면, ResponseStatusExceptionResolver에 의해 처리되고, 없다면 DefaultHandlerExceptionResolver에의해 처리가 됩니다. 
4. 스프링은 BasicErrorController를 구현해놨는데, ExceptionHandler나 ControllerAdvice처럼 직접 에러를 반환하는 경우는 이 컨트롤러를 거치지 않지만, @ResponseStatus, ResponseStatusException 등과 같이 에러 응답을 직접 반환하지 않는 경우에는 최종적으로 해당 컨트롤러를 거쳐서 에러가 반환됩니다.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/905280f6-7063-4057-8436-30c80e45b9ad/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220215%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220215T193153Z&X-Amz-Expires=86400&X-Amz-Signature=f83b4b0f45f3bf245336c823ee37c73b8fe16b83c3d8a50703b00aa411346c60&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

****🤔 스프링 예외처리 방식****

- @ResponseStatus - 에러 HTTP 상태를 변경하도록 도와줍니다.
- @ExceptionHandler - 컨트롤러의 메서드에 추가함으로서 Controller 단에서 발생하는 예외를 잡아줍니다. 해당 어노테이션에 의해 발생한 예외는 ExceptionHandlerExceptionResolver에 의해 처리됩니다.
- @ControllerAdvice, @RestControllerAdvice - 여러 컨트롤러에 대해 전역적으로 ExceptionHandler를 적용할 수 있도록 해줍니다.
- try/catch - 가장 일반적인 예외처리로 메서드 단위로 예외처리할 수 있습니다.

****🤔 JAVA 예외 처리란?****

자바에서는 ‘예외’를 클래스로 취급하는데, 이 중에는 Exception이라는 클래스를 상속받는 Checked Exception과 Unchecked Exception(Runtime Exception)으로 나눠집니다.

둘의 명확한 구분은 “꼭 처리해야하는 예외인가?”입니다.

Checked Exception이 발생할 가능성이 있다면 반드시 예외처리를 수행해줘야합니다.(컴파일 에러발생)

Unchecked Exception의 경우는 예외처리 하지 않아도 문제는 없으나, 클라이언트 입장에서 올바른 예외처리 메세지를 받을 수 있도록 재정의 해주는 것이 필요합니다.

****🤔 내가 궁금한것****

- @ExceptionHandler을 사용했을 때, @ExceptionHandler 같은 경우는 @Controller, @RestController가 적용된 Bean내에서 발생하는 예외를 잡아서 하나의 메서드에서 처리해주는 기능을 한다. 라는데, Controller 내에 hadler 메서드를 구현한다고 어떻게 예외를 감지할 수 있는 것인지?

```java
// Service
/**
 * @Created by Bloo
 * @Date: 2021/07/08
 */
@RequiredArgsConstructor
@Service
public class ApiUserService {

    private final UserRepository userRepository;

    @Transactional
    public void signUp ( SignupReqDto signupReqDto ) {
        String email = signupReqDto.getEmail();

        Optional<User> user = userRepository.findByEmail(email);
        if ( user.isEmpty() ) {
            userRepository.save(signupReqDto.toEntity());
        } else {
            throw new AlreadyExistEmailException();
        }
    }
}

// Controller
@ExceptionHandler(AlreadyExistEmailException.class)
   ResponseEntity<String> handleAlreadyExistEmail(AlreadyExistEmailException ex) {
   return new ResponseEntity<>(ex.getMessage(), HttpStatus.BAD_REQUEST);
}
```

---

[https://bloowhale.tistory.com/72](https://bloowhale.tistory.com/72)

### Filter와 Interceptor 차이에 대해서 설명해주세요.

---

**핵심답변**

Filter의 경우 톰캣과 같은 웹 컨테이너에 의해 관리가 되고 디스패처 서블릿에 요청이 전달되기 전/후에 url 패턴에 맞는 모든 요청에 대해 부가 작업을 처리할 수 있는 기능입니다. 일반적으로 보안 관련 공통 작업이나 이미지/데이터 압축 및 문자열 코딩에 사용됩니다.

Interceptor의 경우 스프링에서 제공하는 기술로써, 디스패처 서블릿이 컨트롤러를 호출하기 전과 후에 요청과 응답을 참조하거나 가공할 수 있는 기능을 제공합니다.  즉, 필터와 다르게 스프링내에서 동작합니다. 일반적으로 인증/인가 등과 같은 공통작업과 Controller로 넘겨주는 정보의 가공에 사용됩니다.

****🤔 Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?****

???

---

### DTO를 사용하는 이유

---

**핵심답변**

- 데이터를 모아서 전달할 수 있어 통신횟수를 줄일 수 있게 됩니다.
- Entity 자체를 반환하지 않고 DTO를 반환함으로서, 원하는 정보만을 전달할 수 있게 됩니다. 덕분에 불필요한 정보를 클라이언트에게 전달하지 않을 수 있게됩니다.

****🤔 DTO란?****

외부와 통신하는 것은 큰 비용입니다. 이를 줄이기 위해서는 효율적으로 데이터를 전달해야했는데, 그 중 하나의 방법으로 데이터를 하나의 클래스에 담아 전달하는 방법이 고안되었는데, 이것이 DTO입니다. 

---

### JPA를 사용할 때의 이점에 대해서 설명해주세요.

---

**핵심답변**

- JPA에 객체를 전달만 하면 되므로 SQL을 작성하고 JDBC API를 사용할 필요가 없어 생산성이 향상됩니다.
- 필드가 추가되거나 삭제되어도 JPA가 일련의 과정을 대신 처리해주므로 수정해야할 코드가 SQL을 직접 다룰때보다 줄어듭니다.
- 상속, 연관관계, 객체그래프 탐색 등의 패러다임 불일치 문제를 해결해줍니다.
- 특정 데이터베이스 기술에 종속되지 않도록 해줍니다.

****🤔 JPA란?****

애플리케이션의 데이터를 객체지향 관점으로 바라보고 다룰 수 있게 해주는 자바 진영의 ORM 기술표준인 객체지향 기술입니다.

****🤔ORM이란?****

객체와 관계형 데이터베이스를 매핑해주는 것으로 SQL 작성 없이 객체를 데이터베이스에 직접 저장할 수 있게 도와주는 기술로 애플리케이션과 JDBC 사이에서 동작합니다.

****🤔 JPA를 구현한 ORM 프레임워크****

하이버네이트, EclipseLink, DataNucleus

---

### JPA에서 N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.

---

**핵심답변**

JPA는 메서드 이름을 분석해서 JPQL을 생성하여 실행하게 됩니다. 이때, JPQL은 SQL을 추상화한 객체지향 쿼리 언어로서 엔티티 객체와 필드 이름을 갖고 쿼리를 만듭니다. 그렇기 때문에, 객체에 대해서 조회하면, 객체의 다양한 연관관계들의 매핑에 의해서 관계가 맺어진 다른 객체가 함께 조회되고 이때, N+1이 발생하게 됩니다.

- 지연로딩 - FetchType.LAZY
연관된 객체를 “사용”하는 시점에 로딩을 해주는 방법으로서 엔티티를 조회할 때 N+1문제가 발생하지 않으나 추가로 엔티티의 연관된 객체를 조회하게 되면 이미 캐싱된 엔티티에 대한 쿼리가 추가로 발생하게됩니다.

- 지연로딩 해결책1 - fetch join
JPQL을 이용해 바로 사용할 객체에 대해서 join을 걸 수 있도록 조정해주는 방식을 이용해 이 지연로딩의 문제점을 해결할 수 있습니다. fetch는 지연 로딩이 걸려있는 연관관계에 대해서 한번에 같이 즉시로딩해주는 구문입니다.

```java
@Query("select distinct u from User u left join fetch u.articles")
List<User> findAllJPQLFetch();
```

- 지연로딩 해결책2 - @EntityGraph
JPQL에서 fetch join을 하게 되면 하드코딩해야하는 단점이 있습니다. 이를 보완하기 위해 엔티티그래프 어노테이션을 사용할 수 있습니다.

```java
@EntityGraph(attributePaths = {"articles"}, type = EntityGraphType.FETCH)
@Query("select distinct u from User u left join u.articles")
List<User> findAllEntityGraph();
```

- Pagination에서의 문제 발생
distinct를 쓰는 이유는 연관관계에 대해서 fetch join으로 가져온다고 했을 때, 중복된 데이터가 많기 때문에 중복 데이터를 처리하기 위함인데, Paging 처리는 쿼리를 날릴 때 진행되기 때문에 JPA에게 pagination 요청을 하여도 distinct때와 마찬가지로 중복된 데이터가 있을 수 있으니 limit offset을 걸지 않고 인메모리에 다 가져오게 됩니다. 이렇게 되면 paging을 하는 의미가 사라지게 됩니다.
- Paging 해결방법 - ~ToOne
~ToOne 관계에 있는 경우에는 fetch join을 걸어도 Pagination이 원하는대로 제공됩니다.

```java
@EntityGraph(attributePaths = {"user"}, type = EntityGraphType.FETCH)
@Query("select a from Article a left join a.user")
Page<Article> findAllPage(Pageable pageable);
```

- Paging 해결방법 - Batch Size
사용자가 임의로 연관관계에 대해 데이터의 사이즈를 알때 사용할 수 있는 방법으로 지연로딩하는 객체에 대해서 Batch성 loading하는 것입니다. 기존의 지연로딩은 객체를 조회할 때 그때그때 쿼리문을 날려서 N+1이 발생한 반면 객체를 조회하는 시점에 쿼리를 하나만 날리는게 아니라 해당하는 Article에 대해서 쿼리를 batch size개를 날리게 되는 것입니다.
즉, 지연 로딩으로 생길 N+1 문제를 batch size만큼 가져와 미연에 방지하는거라고 볼 수 있습니다.

- Paging 해결방법 - @Fetch(FetchMode.SUBSELECT)
BatchSize와 동일한 동작을 하지만, size를 개발자가 임의로 정하는 것이 아닌 스프링에서 자동으로 설정해줍니다. 일반적으로 모든 batchsize를 가져오기 때문에, 성능적인 테스트가 필요합니다.

- MultipleBagFetchException 해결책 - fetch join
 두개 이상의 fetch join을 설정할 경우 메모리에 너무 많은 값이 들어와 MultipleBagFetchException을 발생합니다. 이 경우에는 Set자료구조를 사용해 해결할 수 있습니다. 하지만 Pagination에는 사용할 수 없습니다.

```java
@OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
private Set<Article> articles = emptySet();

@OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
private Set<Question> questions = emptySet();
```

- MultipleBagFetchException 해결책 - batchsize
    - List 자료구조를 꼭 사용해야하는 경우에 사용할 수 있습니다.
    - 2개 이상의 Collection join을 사용하는데, Pagination을 사용해야해서 인메모리 OOM을 방지하고자 하는 경우에 사용할 수 있습니다.
    
    ```java
    @BatchSize(size = 100)
    @OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
    private Set<Article> articles = emptySet();
    
    @BatchSize(size = 100)
    @OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
    private Set<Question> questions = emptySet();
    ```
    
    ```java
    @BatchSize(size = 100)
    @OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
    private List<Article> articles = new ArrayList<>();
    
    @BatchSize(size = 100)
    @OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
    private List<Question> questions = new ArrayList<>();
    ```
    
    ```java
    @Query("select distinct u from User u left join u.articles left join u.questions")
    Page<User> findAllPage2(Pageable pageable);
    ```
    

****🤔 N + 1 문제가 무엇인지 설명부탁드립니다.****

연관 관계에서 발생하는 문제로 연관관계가 설정된 엔티티를 조회할 경우 조회된 데이터 갯수(n) 만큼 연관관계의 조회 쿼리가 추가로 발생하여 데이터를 읽어오는 것을 N+1 문제라고 합니다.

---

[https://velog.io/@jinyoungchoi95/JPA-모든-N1-발생-케이스과-해결책](https://velog.io/@jinyoungchoi95/JPA-%EB%AA%A8%EB%93%A0-N1-%EB%B0%9C%EC%83%9D-%EC%BC%80%EC%9D%B4%EC%8A%A4%EA%B3%BC-%ED%95%B4%EA%B2%B0%EC%B1%85)
