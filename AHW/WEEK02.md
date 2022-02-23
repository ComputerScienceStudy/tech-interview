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
  - AOP란 Aspect Oriented Programming, 관점 지향 프로그래밍을 의미합니다. 관점지향이란, 어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 각각 모듈화하는 프로그래밍 기법을 의미합니다. 따라서 AOP는 핵심기능과 부가기능을 나누어서 설계, 구현하는 것을 의미합니다.
  - ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/83f575d7-dd75-40eb-9973-0b7fbb0920c7/Untitled.png)

### **🤔 AOP 기술을 적용하는 이유가 뭔가요?**

필수적이지만 반복적으로 사용되는 코드, log 출력이나, 예외처리 같은 부분을 모듈화 시켜, 리팩토링과 유지보수에 이점을 주기 때문입니다.스프링에서 AOP를 사용하게 되면, 개발 코드에서는 비지니스 로직에 집중할 수 있고, 런타임 실행 시 부가기능을 비지니스 로직 앞과, 뒤 원하는 지점에서 공통 관심사를 수행하게 하여 중복코드를 줄일 수 있습니다.

### **🤔 AOP가 적용되는 위치는 어떻게 제어하나요?**

스프링 AOP에서는 Advice가 적용되는 5가지 시점을 제공합니다.

1. @Around() : 첫번째로, Around() 어노테이션은 핵심기능 전과 후 모두 실행됨을 의미합니다.
2. @Before() : Before() 어노테이션은 핵심기능 호출전에 실행됨을 의미합니다.
3. @After() : 세번째로, After() 어노테이션은 '핵심기능'의 수행 성공 여부와 상관없이 수행 후 언제나 실행됨을 의미합니다.
4. @AfterReturning() : AfterReturning()은 '핵심기능'의 호출 성공시에만 실행될 것임을 의미합니다.
5. @AfterThrowing() : 마지막으로, AfterThrowing()은 '핵심기능' 호출 실패 시, 즉 예외(Exception) 발생한 경우만 동작할 것을 의미합니다.
  
  - 예시코드:
```java
@Aspect
@Component
public class Advice {

	/*
	 * Before : 클래스의 메소드 실행 전
	 * within : BoardController 클래스를 지정
	 */
	@Before("within (com.wipia.study.controller.BoardController)")
	public void beforeAdvice() {
		System.out.println("BoardController Before");
	}
	
	/*
	 * After : 메소드 실행 후
	 * execution : getBoardList 메소드 지정 * 로 모든 메소드 지정 가능
	 * 접근지정자 : 생략 가능 ex) public, private
	 * * : 변환 타입
	 * 
	 */
	@After("execution(* com.wipia.study.controller.BoardController.getBoardList(..))")
	public void afterAdvice() {
		System.out.println("after getBoardList");
	}
	
	/*
	 * AfterThrowing : 예외 발생 시
	 * 모든 클래스에서 메소드 호출 에러가 발생했을 때 동작
	 */
	@AfterThrowing(pointcut="execution(* com.wipia*..*.*(..))", throwing="e")
	public void afterThrowingAdvice(Exception e) {
		System.out.println("에러다 : "+e);
	}
	
	/*
	 * 모든 메소드 실행시 얼마나 걸리는지 시간 출력
	 */
	@Around("execution (* com.wipia..*.*(..))")
	public Object time(ProceedingJoinPoint pjp) {
		
		long start = System.currentTimeMillis();
		
		System.out.println("--- Target : "+pjp.getTarget());
		System.out.println("--- Parameter : "+Arrays.toString(pjp.getArgs()));
		
		Object result = null;
		
		try {
			result=pjp.proceed();
		}catch (Throwable e) {
			e.printStackTrace();
		}
		
		long end = System.currentTimeMillis();
		System.out.println("--- Time : "+(end-start));
		
		return result;
	}

}
```

### **🤔 AOP의 특징에 대해서 설명부탁드립니다.**

- 프록시 패턴 기반이기 때문에, 접근 제어가 가능합니다.
- 프록시가 호출을 인터셉터해서 핵심 로직 전과 후에 부가기능을 수행할 수 있습니다.
- 핵심 기능의 메소드가 호출되는 런타임 시점에만 부가 기능을 적용할 수 있습니다.

### **🤔 프록시 패턴이란?**

어떤 객체에 대한 접근을 제어하거나 부가기능을 추가하는 용도로 실제 객체를 대신하는 객체를 제공하는 패턴입니다.

### **🤔 프록시 패턴 동작 원리에 대해서 설명해주세요.**

클라이언트가 인터페이스 타입으로 프록시 객체를 사용하게 되고, 프록시는 핵심 기능을 갖는 실제 객체를 감싸서 클라이언트의 요청을 처리하게 됩니다. 이런 특징 덕분에 프록시 패턴은 접근을 제어할 수 있고 부가 기능을 추가할 수 있게 됩니다.

### **🤔 AOP의 주요 개념들에 대해 설명해주세요**

- Aspect : 흩어진 관심사를 모듈화 한 것입니다. 주로 부가기능을 모듈화함을 의미합니다.
- Target : Aspect를 적용하는 곳울 의미합니다. Target은 주로 클래스, 메서드 등이 됩니다.
- Advice : 실질적으로 어떤 일을 해야할 지에 대한 것을 의미하빈다.Advice는 실질적인 부가기능을 담은 구현체입니다.
- JoinPoint : Advice가 적용될 위치, 끼어들 수 있는 지점, 메서드 진입 지점, 생성자 호출 시점, 필드에서 값을 꺼내올 때의 시점을 말합니다. 앱을 실행할 때 특정 작업이 시작되는 시점입니다.
- PointCut : JoinPoint가 적용되는 대상, Adivice가 실행될 지점을 설정합니다.

---
- **Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.**
### **핵심답변**

- 첫 번째로, Servlet Filter를 사용하여 커스텀한 CORS 설정하는 방법이 있습니다.
- 두 번째로, Controller 클래스에 @Crossorigin 어노테이션을 통해 해결할 수 있습니다.
- 세 번째로,WebMvcConfiguer를 구현한 Configuration 클래스를 만들어서 addCorsMappings()를 재정의할 수도 있습니다.
- 마지막으로, Spring Security에서 CorsConfigurationSource를 Bean으로 등록하고 config에 추가해줌으로써 해결할 수 있습니다.

### **🤔 CORS에러가 나는 이유가 무엇인가요?**

CORS(Cross-Origin-Resource-Sharing)는 Origin이 다른 경우(Cross-Oirgin) 리소스를 공유한다는 것을 의미합니다.하지만 웹브라우저는 원래 동일 출처 원칙(Same Origin Policy)를 보안상 기본으로 합니다.

따라서 CORS에러는, 동일한 출처의 Origin, 즉 스키마, Host, Port가 같아야만 리소스를 공유할 수 있다는 보안 정책 때문에 발생합니다.

### **🤔 CORS 에러를 해결하기 위한 방법을 자세히 설명해주세요**

### **1️⃣ Servlet Filter를 사용하여 커스텀한 CORS 설정하는 방법**

서버의 응답을 보내기 전에 Access-Control-Allow-Origin 헤더를 싣는 필터를 작성하는 방법입니다.

1. 빈으로 등록된 CorsFilter 클래스를 생성합니다.
2. 해당 클래스에 doFilter를 직접 오버라이드해서 Options 메서드에 response로 Access-Control-Allow-Origin헤더에 허용된 Origin이라는 코드를 작성합니다.
- 예시코드
    
    ```java
    @Component
    @Order(Ordered.HIGHEST_PRECEDENCE)
    public class CorsFilter implements Filter {
    
        @Override
        public void init(FilterConfig filterConfig) throws ServletException {
        }
    
        @Override
        public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain) throws IOException, ServletException {
            HttpServletRequest request = (HttpServletRequest) req;
            HttpServletResponse response = (HttpServletResponse) res;
    
            response.setHeader("Access-Control-Allow-Origin", "http://localhost:5500");
            response.setHeader("Access-Control-Allow-Credentials", "true");
            response.setHeader("Access-Control-Allow-Methods","*");
            response.setHeader("Access-Control-Max-Age", "3600");
            response.setHeader("Access-Control-Allow-Headers",
                    "Origin, X-Requested-With, Content-Type, Accept, Authorization");
    
            if("OPTIONS".equalsIgnoreCase(request.getMethod())) {
                response.setStatus(HttpServletResponse.SC_OK);
            }else {
                chain.doFilter(req, res);
            }
        }
    
        @Override
        public void destroy() {
    
        }
    }
    ```
    

### **2️⃣ Controller 클래스에 @Crossorigin 어노테이션을 활용하는 방법**

- Controller 클래스 상단이나 Controller Mapping 메소드 상단에 CrossOrigin(origins="도메인 url")을 어노테이션으로 작성하는 방법입니다.
- CorsFilter를 직접 구현해서 사용하는 것 보다, 어노테이션만 붙히면 되기에 더 간편하게 사용할 수 있습니다.
- 예시코드
    
    ```java
    @CrossOrigin(origins = "http://127.0.0.1:5500/")  // 컨트롤러 클래스의 상단
    @RequiredArgsConstructor
    @RestController
    public class ArticleRestController {
    
        public final ArticleRepository articleRepository;
        public final ArticleService articleService;
        public final LocationDistance location;
    
        @CrossOrigin(origins = "http://127.0.0.1:5500/")  // 컨트롤러 맵핑 메소드 상단
        @GetMapping("/api/articles/{query}")
        public ResponseEntity<List<Article>> getArticles (@PathVariable("query") String query) {
            List<Article> articles = articleRepository.findAllByTitleContains(query);
            return ResponseEntity.ok().body(articles);
        }
    }
    ```
    

### **3️⃣ WebMvcConfig를 구현한 Configuration 클래스를 만드는 방법**

- WebMvcConfig 클래스를 활용하는 방법입니다.
- WebMvcConfiguer를 implement한 클래스를 만들고, @Configuration 어노테이션으로 어플리케이션에 연결하는 방법입니다.
- allowedOrigins, allowedMethods 메서드를 통해 cors를 설정해줄 수 있습니다.
- 간단한 코드로 전체범위의 CORS를 설정해 준다는 장점이 있습니다.
- 예시코드

    ```java
    import org.springframework.context.annotation.Configuration;
    import org.springframework.web.servlet.config.annotation.CorsRegistry;
    import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;
    
    @Configuration
    public class WebConfig implements WebMvcConfigurer {
    
        @Override
        public void addCorsMappings(CorsRegistry registry) {
            registry.addMapping("/**")
                    .allowedOrigins("http://localhost:5500", "http://127.0.0.1:5500")
                    .allowedMethods("POST", "PUT", "GET", "HEAD", "OPTIONS", "DELETE");
        }
    }
    ```

---
- **Bean에 대해 설명해보세요.**
  - **Spring Bean이란 무엇인가요?**
    - Spring IoC 컨테이너에 의해 인스턴스화, 관리, 생성되는 자바 객체
    - ApplicationContext가 알고있는 객체, 즉 ApplicationContext가 만들어서 그 안에 담고있는 객체
    - 따라서, 기존의 Java Programming에서처럼 Class를 생성하고 new 연산자로 생성된 객체가 아니라 Spring에서 `ApplicationContext.getBean()`과 같은 메소드를 사용하여 생성된 객체 
      
  - **스프링 Bean의 생성 과정을 설명해주세요.**
    - 객체 생성 -> 의존 설정 -> 초기화 -> 사용 -> 소멸 순서의 라이프 사이클을 지닌다.
    1. 객체 생성
      - 스프링 컨테이너가 초기화 될 때 먼저 빈 객체를 설정 정보에 맞추어 생성
    2. 의존 설정
    3. 초기화
      - 의존 관계를 설정한 뒤에 해당 프로세스가 완료되면 빈 객체가 지정한 메소드를 호출해서 초기화
    4. 사용
    5. 소멸
      - 객체를 사용한 뒤 컨테이너가 종료 될 때 빈이 지정한 메소드를 호출해 소멸 과정을 진행 
[](https://takoyummy.tistory.com/91)

  - **스프링 Bean의 Scope에 대해서 설명해주세요.**
    - Bean이 존재하는 범위이며, 기본적으로 모든 bean을 singleton으로 생성하여 관리한다.
    - 구체적으로는 애플리케이션 구동 시 JVM 안에서 Spring이 bean마다 하나의 객체를 생성하는 것을 의미
    - 그래서 개발자들은 Spring을 통해서 bean을 제공받으면 언제나 주입받은 bean은 동일한 객체라는 가정하에서 개발
    - prototype bean은 의존성 관계의 bean에 주입될 때 새로운 객체가 생성되어 주입된다
    
    1. `singleton` : 스프링 컨테이너의 시작과 종료까지 단 하나의 객체만 사용하는 방식
      ![image](https://user-images.githubusercontent.com/90819869/154178392-70e96c18-6a96-4b26-9ec9-8430aa7f491b.png)
    2. `prototype` : 모든 요청에서 새로운 객체를 생성하는 방식
      ![image](https://user-images.githubusercontent.com/90819869/154178422-3304cff2-d566-482f-b191-68c10613fc3f.png)
 [](https://gmlwjd9405.github.io/2018/11/10/spring-beans.html)
 
  - **Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.**
    1. **`@Bean`**
      -  @Bean은 개발자가 직접 제어가 불가능한 외부 라이브러리를 사용할 때 사용한다.
      -  @Configuration을 선언한 클래스 내부에서 사용해준다.
      -  즉, 개발자가 작성한 메소드를 통해 반환되는 객체를 Bean으로 만든다.
      
      < 개발자가 직접 제어가 불가능한 외부 라이브러리를 사용한 경우 >
      ```java
      @Configuration
      public class ExampleConfig {

          @Bean
          public ArrayList<String> array(){
            return new ArrayList<String>();
          }
      }
      ```

      < 개발자가 만들어준 클래스를 import해 사용한 경우 >
         ```java
        @Configuration
        public class ExampleConfig {

            @Bean(name="mybean")
            public Product aaa(){
                  Battery p1 = new Battery("AAA", 2.5);
                  p1.setRechargeable(true);
                  return p1;
            }
        }
          ```

    2. **`@Component`**
      - @Component는 개발자가 직접 작성한 Class를 Bean으로 등록 할 수 있게 만들어 준다.
      - 즉, 개발자가 작성한 class를 Bean으로 만든다.
      ```java
      @Component(value="mybean")
      public class Example {
        puiblic Example(){
            System.out.println("Hello world");
          }
      }
    ```
[](https://withseungryu.tistory.com/64)

---
- Getter와 Setter를 사용해야하는 이유에 대해서 설명해주세요.
  - 객체의 무결성을 보장하기 위해 사용한다
  - `Getter` : 본 필드의 값을 숨긴 채 내부에서 가공된 값을 꺼낼 수 있다.
  - `Setter` : 필드를 private로 만들어 외부의 접근을 제한한 후, Setter를 사용해 전달받은 값을 내부에서 가공해 필드에 넣어주는 방식을 사용한다.
[](https://thiago6.tistory.com/75)

---
- Spring에서 예외처리하는 방법에 대해서 설명해주세요.
![image](https://user-images.githubusercontent.com/90819869/154179980-61e486a0-42ad-412f-a0cb-09ece90c51fb.png)
  1. `메서드 레벨` : 메서드 단위에서 try/catch를 통해 처리
  2. `컨트롤러 레벨` : 컨트롤러단에서 @ExceptionHandler를 이용해서 처리
  3. `글로벌 레벨` : 컨트롤러 이후 Client에게 전달되기 직전 처리
[](https://devkingdom.tistory.com/118)

---
- **Filter와 Interceptor 차이**
  - 실행되는 시점이 다르다
	1. Filter
		- 디스패처 서블릿(Dispatcher Servlet)에 요청이 전달되기 전/후에 url 패턴에 맞는 모든 요청에 대해 부가작업을 처리할 수 있는 기능을 제공
	2. Interceptor
		- 디스패처 서블릿(Dispatcher Servlet)이 컨트롤러를 호출하기 전과 후에 요청과 응답을 참조하거나 가공할 수 있는 기능을 제공
  - `Filter`는 Web Application에 등록하고, `Intercptor`는 Spring의 Context에 등록을 한다

[](https://mangkyu.tistory.com/173)

- **Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?**
	- 실행 시점이 다르기 때문에 가장 큰 영향을 받는 것이 바로 예외처리이다.
	- `Filter`에서 예외가 발생하면 Web Application에서 처리해야 하고, `Interceptor`에서 예외가 발생하면 실행 시점이 Spring의 ServletDispatcher 내에 있기 때문에 @ControllerAdvice에서 @ExceptionHandler를 사용해서 예외를 처리를 할 수 있다.
[](https://devdavelee.tistory.com/25)

---
- **DTO를 사용하는 이유**
	- DTO(Data Transfer Object, 데이터 전송 객체)는 프로세스 간에 데이터를 전달하는 객체이다
	- 외부와 통신하는 프로그램에게 있어 호출은 큰 비용이며, 이를 줄이고 더욱 효율적으로 값을 전달하기 위해 데이터를 모아 한 번에 전달하는 방법이 고안되었고, 이 때 이 클래스를 DTO라고 한다. 즉, 통신의 횟수를 감소시키고 로직을 효율적으로 하기 위해 사용한다.
	- 데이터를 묶어서 하나의 요청으로 보내면 검증과 로직 처리 역시 한 번에 할 수 있다
	- 안정성과 수행시간 모두 묶어 보내는 쪽이 유리하다
[](https://kafcamus.tistory.com/13)

---
### JPA
- **JPA를 사용할 때의 이점에 대해서 설명해주세요.**
	1. 생산성
		- 쿼리를 직접 생성하는 것이 아니라, 만들어진 객체로 데이터베이스를 다루기 때문에 객체 중심으로 개발 가능
	2. 유지보수
		- SQL을 직접적으로 작성하지 않고 엔티티 필드가 되는 객체를 다뤄서 데이터베이스를 동작시키기 때문에 유지보수가 더욱 간결하다
		`WHY?` 쿼리가 수정되면 그에 따라서 그를 담을 DTO 필드도 모두 변경이 되야 하지만, JPA를 사용하게 되면 단순히 엔티티 클래스 정보만 변경하면 쉽게 관리가 가능하기 때문
	3. 성능
		- 일반적인 Spring의 encache 기능처럼 동일한 쿼리에 대한 캐시 기능을 사용하기 때문에 더욱 높은 성능적 효율성

💡 **제약사항 및 단점**
JPA(Java Persistence Api)는 통계처리와 같이 복잡한 쿼리보다는 실시간 처리용 쿼리에 더 최적화되어 있다.
물론 JPA에서 제공하는 Native query기능을 사용할 수 있지만 통계처럼 복잡하고 미세하게 쿼리 작업이 필요하다면 Mybatis와 같은 Mapper 방식을 사용하는 것이 더 효율적일 수 있다.
Spring에서 JPA와 Mybatis를 혼용해서 사용할 수 있기 때문에 필요에 따라 적절한 방식으로 선택해가면서 사용하면 될 것 같다.

[wedul](https://wedul.site/506)

---
- **JPA에서 N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.**
[JPA N+1 발생원인과 해결 방법](https://www.popit.kr/jpa-n1-%EB%B0%9C%EC%83%9D%EC%9B%90%EC%9D%B8%EA%B3%BC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95/)
[JPA N+1) 문제 완전 정리](https://galid1.tistory.com/800)

<br><br>
---
# 💡 피드백
## POJO
#### POJO와 Java bean, Spring bean는 같은 것들인가요?
| 구분 | 개념 |
| :--: | :--: |
| POJO | 특정 프레임워크에 바인딩되지 않은 Java 객체 |
| Java Bean | \*엄격한 컨벤션을 지키는 특수 유형의 POJO |
| Spring Bean | 개발자가 관리하는 객체가 아닌, 스프링 IoC 컨테이너에서 관리되는 객체 |

- **\* 엄격한 컨벤션**
	1. Access Level - 모든 클래스의 속성은 private
	2. Getter/Setter 메소드로 제어
	3. 기본 생성자(인수가 없는 public 생성자) 필수
	    - 역직렬화 시에 인수 없이 인스턴스를 생성하기 위함
	4. Serializable 인터페이스를 구현하여 상태를 저장할 수 있게 함
<br>

[📚 Reference](https://2jinishappy.tistory.com/324)
<br><br>

---
## DI/IoC

#### 1. IoC가 무엇인지는 아시는 것 같은데, IoC가 필요한 이유는 무엇인가요? 왜 외부에서 제어 흐름을 관리해야하죠?

- 객체지향적으로 **Single Responsibility Principle**을 지킬 수 있다.
	
	즉, A class가 B의 의존관계를 선택할 필요 X = B class의 변경에 대해 A class는 변경 X

- 개발자가 객체를 `new`로 직접 만들지 않고 IoC Container가 객체를 Bean으로써 대신 관리해주는 것이 IoC이다.

	따라서, `new`로 객체 생성시 `new`를 쓸 때마다 시스템 용량을 차지하는데, bean에 한번만 등록해줌으로써 편리성이 높아지고, 속도가 빨라진다.

<br>

[📚 Reference](https://okky.kr/article/1034744?note=2487385)
<br><br>

#### 2. BeanFactory와 ApplicationContext는 각각 무엇인가요?
- BeanFactory
	- Bean을 등록, 생성, 조회 등의 관리를 하고, 의존관계를 설정하는 기능을 담당하는 가장 기본적인 IoC 컨테이너이자 클래스

- ApplicationContext
	- BeanFactory의 확장된 버전으로, BeanFactory의 모든 기능을 포함하고, 추가 기능 또한 제공하는 컨테이너

<br>

[📚 Reference](https://beststar-1.tistory.com/39#빈_팩토리(BeanFactory)
<br><br>

---
## MVC - Dispatcher Servlet 동작 원리

#### 1. Dispatcher Servlet은 어느 시점에 생성되나요?
- 웹 애플리케이션의 서블릿 컨텍스트를 초기화하는 시점에 옵션에 따라 `lazy loading` 혹은 `pre loading` 방식으로 생성됩니다.

<details>
<summary>💡 ServletContext</summary>

- 톰캣이 실행되면서 서블릿과 서블릿 컨테이너 간 연동을 위해 사용되는 Context
- 하나의 웹 애플리케이션마다 하나의 서블릿 컨텍스트를 가진다.
- 서블릿 컨테이너가 생성될 때 컨텍스트가 생성되고 종료되면 소멸된다.

</details>

<br>
	
#### 2. Dispatcher Servlet이 Controller 객체를 직접 메모리에 생성하나요? 직접 생성하지 않는다면 무엇이 그 역할을 수행하나요?

- **NO**
	- DispatcherServlet은 적절한 controller를 선택하는 일을 HandlerMapping에게 요청한다.
	- HandlerMapping이 적합한 controller를 선택 후 DispatcherServlet에 전달한다.
	- 즉, HandlerMapping이 Controller 객체를 직접 메모리에 생성하는 역할을 수행한다(고 생각합니다).

<br>

#### 3. DispatcherServlet이 생성된 이후의 과정은 잘 알고 계신 것 같은데, 웹 어플리케이션이 실행된 이후부터 DispatcherServlet이 생성되기전까지 Spring framework가 어떤 준비를 하는지 설명해주실 수 있나요?
	
a. Tomcat(WAS)에 의해 web.xml이 로딩됨

b. web.xml에 등록외어 있는 ContextLoaderListener (Java Class) 생성

c. 생성된 ContextLoaderListener가 root-context.xml을 로딩

d. root-context.xml에 등록되어 있는 Spring Container가 구동됨

e. 클라이언트로부터 웹 어플리케이션 요청을 받음

f. 최초의 클라이언트 요청에 의해 **DispatcherServlet 생성**

<br>

<details>
<summary>💡 용어 사전</summary>

- `web.xml`: 각종 설정을 위한 파일
- `ContextLoaderListener` 객체: src/main/resources 소스 폴더에 있는 applicationContext.xml 파일을 로딩하여 스프링 컨테이너를 구동 (= Root 컨테이너)
- `root-context.xml`: view와 관련되지 않은 객체를 정의하고, Service, Repository(DAO), DB등 비즈니스 로직과 관련된 설정을 수행하는 파일

![image](https://user-images.githubusercontent.com/90819869/155349278-75cce6a8-0139-447e-99fc-74ed93368a86.png)

</details>	

<br>

[📚 1. Reference](https://velog.io/@suhongkim98/DispatcherServlet과-스프링-컨테이너-생성-과정)
	
[📚 2. Reference](https://velog.io/@hsw0194/Spring-MVC-HandlerMapping%EC%9D%98-%EB%8F%99%EC%9E%91%EB%B0%A9%EC%8B%9D-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-1%ED%8E%B8)
	
[📚 3. Reference](https://javannspring.tistory.com/231)
	
[📚 3. Reference](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc)

<br><br>

## AOP

#### 1. 프로젝트에서 AOP를 활용한 부분이 있으실까요?

<br>

#### 1-1. 사용자 인증과 로깅을 구현하셨던데 이건 AOP를 활용한 것이 아닌가요?

- AOP를 활용한 로깅

	- 기존에 서비스 로직에 로깅하는 코드(cross-cutting)를 제거하고, 핵심 로직에서 분리하여 핵심 로직 부분을 전혀 수정하지 않고 원하는곳에 적용할 수 있습니다.

#### 1-2. 그럼 @Transactional 어노테이션은 AOP를 활용한 기능인가요?

- **YES**. 어노테이션 기반 AOP를 통해 구현되어 있기 때문에, 아래와 같은 특징이 있습니다.

	- 클래스, 메소드에 @Transactional이 선언되면 해당 클래스에 트랜잭션이 적용된 프록시 객체 생성
	- 프록시 객체는 @Transactional이 포함된 메서드가 호출될 경우, 트랜잭션을 시작하고 Commit or Rollback을 수행
	- CheckedException or 예외가 없을 때는 Commit
	- UncheckedException이 발생하면 Rollback

<br>

#### 2. 만약 프로젝트의 모든 Entity에서 Entity 생성시간과 수정시간 필드를 사용한다면, 이 필드를 한 곳에서 관리할 수 있는 방법이 있을까요? Spring framework를 사용하는 환경입니다.

- **YES**. JPA Auditing을 활용하여 관리 가능

	- JPA Auditing 적용 방법
		1. Posts 클래스에서 BaseTimeEntity를 상속받아 자동으로 Entity의 시간을 관리
		2. Application 클래스에 @EnableJpaAuditing을 추가

<br>

[📚 1-1. Reference](https://velog.io/@znftm97/Spring-AOP를-활용하여-로깅)

[📚 1-2. Reference](https://imiyoungman.tistory.com/9)
	
[📚 2. Reference](https://frtt0608.tistory.com/114)

<br><br>

## Bean

#### 1. Spring framework로 웹 어플리케이션을 개발할 때 Bean Scope(Bean의 생성과 의존 설정까지만 관여하는 매우 짧은 스코프) 중 프로토타입 스코프는 어떤 경우에 활용하면 좋을까요?

- 용도
	- `new` 키워드로 오브젝트를 생성하는 것을 대신하기 위해 사용
	
- 활용 사례
	- `new`가 아닌, 컨테이너의 DI 기능을 사용하고 싶은 경우
	- 매번 새로운 오브젝트가 필요하면서 DI를 통해 다른 빈을 사용해야할 경우

<br>

[📚 1. Reference](https://gunju-ko.github.io/toby-spring/2019/04/15/%ED%94%84%EB%A1%9C%ED%86%A0%ED%83%80%EC%9E%85%EA%B3%BC-%EC%8A%A4%EC%BD%94%ED%94%84.html)

<br><br>

## DTO

#### 1. Serialize/Deserialize란?

- **Serialize(직렬화)**
	- 자바 시스템 내부에서 사용되는 객체(Object) 또는 데이터(Data)를 외부 자바 시스템에서도 사용할 수 있도록 바이트(byte) 형태로 데이터를 변환하는 기술
	- JVM(Java Virtual Machine)의 메모리에 상주(힙 또는 스택)되어 있는 객체 데이터를 바이트 형태로 변환하는 것
	
- **Deserialize(역직렬화)**
	- 직렬화와 반대로, 바이트로 변환된 데이터를 원래대로 객체(Object)나 데이터(Data)로 변환하는 기술
	- 직렬화된 바이트 형태의 데이터를 객체로 변환해서 JVM에 상주시키는 것

<br>

#### 1-1. ObjectMapper란?

-  Java 객체를 JSON으로 직렬화하거나 JSON 컨텐츠를 Java 객체로 역직렬화 할 때 사용하는 Jackson 라이브러리의 클래스
- ObjectMapper를 통해 직렬화와 역직렬화 설정을 해줄 수 있습니다.
- **장점**: 코드량을 줄일 수 있다.
- **단점**: 모든 dto나 entity에 설정해줘야 한다. 또, 외래키로 묶여있는 다른 entity나 dto는 변환되지 않는다.

<br>

#### 1-2. Serialize/Deserialize를 하는 이유는 무엇인가요?
- 대부분 OS의 프로세스 구현은 서로 다른 가상 메모리 주소 공간(Virtual Address Spage, VAS)을 갖기 때문에, *Object 타입의 참조값(주소 값) 데이터 인스턴스를 전달할 수 없습니다*.
- 만약 전달한다고 하더라도, *서로 다른 메모리 공간에서는 전달된 참조값이 무의미*합니다.
- 따라서, **서로 다른 메모리 공간 사이의 데이터 전달을 위해** 메모리 공간의 주소 값이 아닌 바이트(byte) 형태로 직렬화(변환)된 객체 데이터를 전달하고, 사용하는 쪽에서는 역직렬화 하여 사용하는 방법이 사용됩니다.

<br>
	
#### 2. DTO로 넘긴 데이터가 어떻게 JSON 형식으로 변환되고, JSON 데이터가 어떻게 객체에 매핑되는지, 그 과정에서 어떤 라이브러리가 관여하는지 설명해주세요.

- **Jackson이란?**
	- Java Object를 Json으로 변환하거나 Json을 Java Object로 변환하는데 사용할 수 있는 Java 라이브러리

- **Java Object → JSON**
	- Java 객체를 JSON으로 직렬화하기 위해 ObjectMapper의 **`writeValue()` 메서드**를 이용
	- 파라미터로 JSON을 저장할 파일과 직렬화시킬 객체를 넣어줍니다.
	- 정상 실행 시, 개발자가 지정한 경로(`src/person.json`)에 json 파일(`{"name":"hwon","age":20,"address":"seoul"}`)이 생성됩니다.

	```java
	import com.fasterxml.jackson.databind.ObjectMapper;

	import java.io.File;
	import java.io.IOException;

	public class ObjectMapperEx {
	    public static void main(String[] args) {
		ObjectMapper objectMapper = new ObjectMapper();

		// Java Object ->  JSON
		Person person = new Person("hwon", 20, "seoul");
		try {
		    objectMapper.writeValue(new File("src/person.json"), person);
		} catch (IOException e) {
		    e.printStackTrace();
		}
	    }
	}
	```
	
- **JSON → Java Object**
	- JSON 파일을 Java 객체로 역직렬화하기 위해 ObjectMapper의 **`readValue()` 메서드**를 이용
	- 파라미터로 JSON 형태의 문자열 or 객체와 역직렬화 시킬 클래스를 넣어줍니다.
	- 실행 결과, 파일 내 정보(`Person(name=hwon, age=20, address=seoul)`)가 확인됩니다.

	```java
	import com.fasterxml.jackson.core.JsonProcessingException;
	import com.fasterxml.jackson.databind.ObjectMapper;

	public class ObjectMapperEx {
	    public static void main(String[] args) {
		ObjectMapper objectMapper = new ObjectMapper();

		// JSON -> Java Object
		String json = "{\"name\":\"zooneon\",\"age\":25,\"address\":\"seoul\"}";
		try {
		    Person deserializedPerson = objectMapper.readValue(json, Person.class);
		    System.out.println(deserializedPerson);
		} catch (JsonProcessingException e) {
		    e.printStackTrace();
		}
	    }
	}
	```
	
<br>

[📚 1. Reference](https://wildeveloperetrain.tistory.com/97)
	
[📚 1-1. Reference](https://way-be-developer.tistory.com/240)

[📚 1-1. Reference](https://velog.io/@a45hvn/Java-dto%EC%99%80-entity-%EB%B3%80%ED%99%98%ED%95%98%EA%B8%B0-2)
	
[📚 1-2. Reference](https://wildeveloperetrain.tistory.com/97)
	
[📚 2. Reference](https://velog.io/@leyuri/Java-Json-lib-Jackson)

[📚 2. Reference](https://velog.io/@zooneon/Java-ObjectMapper%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%98%EC%97%AC-JSON-%ED%8C%8C%EC%8B%B1%ED%95%98%EA%B8%B0#java-object-%E2%86%92-json)
