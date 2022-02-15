# [2주차] Spring

## Spring Framework

## 스프링 프레임워크란?
### 핵심답변

#### 🤔 스프링 프레임워크의 종류: Spring, Spring MVC, Spring Boot, Spring Data JPA, Spring AOP

<br><br>
## 스프링 프레임워크의 특징
### 핵심답변

## POJO란 무엇인가요?
### 핵심답변
POJO란, Plan Old Java Object의 약자로, 다른 클래스나 인터페이스를 상속받지 않은, 기본적인 기능만 가진 자바객체를 말합니다.       
POJO는 객체지향적 원리에 충실하고, 특정 규약과 환경에 종속되지 않게 재활용 될 수 있게 설계된 객체를 말합니다.       
POJO를 사용할때의 이점은, 종속된 코드를 분리함으로 코드의 간결함과 자동화 테스트의 유리하고 유지보수성을 높일 수 있습니다.
<br><br>

#### 🤔 Spring Framework에서 POJO는 무엇이 될 수 있을까요?
Spring은 가장 대표적인 POJO프레임워크이며, POJO란 객체지향적인 원리에 충실한 방식으로 설계된 자바 객체입니다.
Spring에서는 도메인과 비지니스 로직을 수행하는 대상이 POJO가 될 수 있습니다.

<Br>

>[POJO에 대하여](https://limmmee.tistory.com/8)

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
1. 수정자 주입(Setter Injection)은 선택적인 의존성을 사용할 때 유용합니다. setter 메소드를 사용하기때문에, 런타임시 의존관계를 주입해 낮은 결합도를 가진다는 장점이 있지만,     
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
   @Autowired를 사용하여 자동으로 의존성이 주입되기 때문에 간편하지만, 참조 관계를 눈으로 확인하기 어렵고, 너무 많은 필드 주입을 하게되면 참조관계과 꼬일 수 있다는 단점이 있습니다.
3. 생성자 주입(Contructor Injection)은 선언된 를, 생성자를 이용하여 의존성을 주입하는 방법입니다.      
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
    
>[IOC와 DI에 대하여](https://mo-world.tistory.com/entry/IOC%EC%99%80-DI-%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC-%EC%8A%A4%ED%94%84%EB%A7%81-%EA%B0%9C%EB%85%90-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-%EC%89%BD%EA%B2%8C-%EC%84%A4%EB%AA%85)    
[IOC 컨테이너](https://dev-coco.tistory.com/80)   
[생성자 주입을 사용해야하는이유](https://yaboong.github.io/spring/2019/08/29/why-field-injection-is-bad/)

<br><br>

## MVC 패턴이란?
### 핵심답변

Model-View-Controller로 나누어진 디자인 패턴입니다.
- Model은, 어플리케이션에서 사용되는 데이터를 다룹니다.
- View는, 데이터의 시각화로, 모델이 처리한 데이터를 받아 이것을 기반으로 사용자가 보는 페이지를 구성합니다.
- Controller는, 사용자의 요청을 해석하여 처리하고, 그 결과를 반환해줍니다. Model과 View사이를 연결해주며, 데이터의흐름을 제어합니다.

<Br><br>
#### 🤔 MVC 패턴을 사용하는 이유는 무엇일까요?

MVC 패턴을 사용하여, 특정기준에 따라 모듈을 분리하여 모듈화해놓기 때문에,     
책임이 구분되어 있어, 유지보수 및 코드의 수정을 편하게 할 수 있습니다.

<br><Br>
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
<br>

<img src="https://user-images.githubusercontent.com/42319300/153905949-7ab73ff7-59a3-4445-a994-5cd39f439a61.png" width="60%" height="60%">

<br><br>

#### 🤔 AOP 기술을 적용하는 이유가 뭔가요?
필수적이지만 반복적으로 사용되는 코드, log 출력이나, 예외처리 같은 부분을 모듈화 시켜, 리팩토링과 유지보수에 이점을 주기 때문입니다.       
스프링에서 AOP를 사용하게 되면, 개발 코드에서는 비지니스 로직에 집중할 수 있고, 런타임 실행 시 부가기능을 비지니스 로직 앞과, 뒤 원하는 지점에서
공통 관심사를 수행하게 하여 중복코드를 줄일 수 있습니다.

<br><br>

#### 🤔 AOP가 적용되는 위치는 어떻게 제어하나요?

스프링 AOP에서는 Advice가 적용되는 5가지 시점을 제공합니다.
1. @Around() : 첫번째로, Around() 어노테이션은 핵심기능 전과 후 모두 실행됨을 의미합니다.
2. @Before() : Before() 어노테이션은 핵심기능 호출전에 실행됨을 의미합니다.
3. @After() : 세번째로, After() 어노테이션은 '핵심기능'의 수행 성공 여부와 상관없이 수행 후 언제나 실행됨을 의미합니다.
4. @AfterReturning() : AfterReturning()은 '핵심기능'의 호출 성공시에만 실행될 것임을 의미합니다.
5. @AfterThrowing() : 마지막으로, AfterThrowing()은 '핵심기능' 호출 실패 시, 즉 예외(Exception) 발생한 경우만 동작할 것을 의미합니다.

<br>

<details><summary>예시 코드</summary>

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

</details>

<br><br>

#### 🤔 AOP의 특징에 대해서 설명부탁드립니다.

- 프록시 패턴 기반이기 때문에, 접근 제어가 가능합니다.
- 프록시가 호출을 인터셉터해서 핵심 로직 전과 후에 부가기능을 수행할 수 있습니다.
- 핵심 기능의 메소드가 호출되는 런타임 시점에만 부가 기능을 적용할 수 있습니다.
<br><br>
#### 🤔 프록시 패턴이란?

어떤 객체에 대한 접근을 제어하거나 부가기능을 추가하는 용도로 실제 객체를 대신하는 객체를 제공하는 패턴입니다.
<Br><br>

#### 🤔 프록시 패턴 동작 원리에 대해서 설명해주세요.

클라이언트가 인터페이스 타입으로 프록시 객체를 사용하게 되고, 프록시는 핵심 기능을 갖는 실제 객체를 감싸서 클라이언트의 요청을 처리하게 됩니다. 이런 특징 덕분에 프록시 패턴은 접근을 제어할 수 있고 부가 기능을 추가할 수 있게 됩니다.

<br><Br>

#### 🤔 AOP의 주요 개념들에 대해 설명해주세요
- Aspect : 흩어진 관심사를 모듈화 한 것입니다. 주로 부가기능을 모듈화함을 의미합니다.
- Target : Aspect를 적용하는 곳울 의미합니다. Target은 주로 클래스, 메서드 등이 됩니다.
- Advice : 실질적으로 어떤 일을 해야할 지에 대한 것을 의미하빈다.Advice는 실질적인 부가기능을 담은 구현체입니다.
- JoinPoint : Advice가 적용될 위치, 끼어들 수 있는 지점, 메서드 진입 지점, 생성자 호출 시점, 필드에서 값을 꺼내올 때의 시점을 말합니다. 앱을 실행할 때 특정 작업이 시작되는 시점입니다.
- PointCut : JoinPoint가 적용되는 대상, Adivice가 실행될 지점을 설정합니다.

<br>

>[AOP란 - (AOP, Spring AOP, AOP 어노테이션)](https://thalals.tistory.com/271)

<Br><br>

## Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.
### 핵심답변
- 첫 번째로, Servlet Filter를 사용하여 커스텀한 CORS 설정하는 방법이 있습니다.
- 두 번째로, Controller 클래스에 @Crossorigin 어노테이션을 통해 해결할 수 있습니다. 
- 세 번째로,WebMvcConfiguer를 구현한 Configuration 클래스를 만들어서 addCorsMappings()를 재정의할 수도 있습니다. 
- 마지막으로, Spring Security에서 CorsConfigurationSource를 Bean으로 등록하고 config에 추가해줌으로써 해결할 수 있습니다.
<br><br>

#### 🤔 CORS에러가 나는 이유가 무엇인가요?
CORS(Cross-Origin-Resource-Sharing)는 Origin이 다른 경우(Cross-Oirgin) 리소스를 공유한다는 것을 의미합니다.       
하지만 웹브라우저는 원래 동일 출처 원칙(Same Origin Policy)를 보안상 기본으로 합니다.

따라서 CORS에러는, 동일한 출처의 Origin, 즉 스키마, Host, Port가 같아야만 리소스를 공유할 수 있다는 보안 정책 때문에 발생합니다.

<Br><Br>
#### 🤔 CORS 에러를 해결하기 위한 방법을 자세히 설명해주세요
#### 1️⃣ Servlet Filter를 사용하여 커스텀한 CORS 설정하는 방법      
서버의 응답을 보내기 전에 Access-Control-Allow-Origin 헤더를 싣는 필터를 작성하는 방법입니다.
1. 빈으로 등록된 CorsFilter 클래스를 생성합니다.
2. 해당 클래스에 doFilter를 직접 오버라이드해서 Options 메서드에 response로 Access-Control-Allow-Origin헤더에 허용된 Origin이라는 코드를 작성합니다.

<Details>
<summary>예시코드</summary>

```Java
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
</Details>

#### 2️⃣ Controller 클래스에 @Crossorigin 어노테이션을 활용하는 방법
- Controller 클래스 상단이나 Controller Mapping 메소드 상단에 CrossOrigin(origins="도메인 url")을 어노테이션으로 작성하는 방법입니다.
- CorsFilter를 직접 구현해서 사용하는 것 보다, 어노테이션만 붙히면 되기에 더 간편하게 사용할 수 있습니다.

<details><summary>예시코드</summary>

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
</details>

<br>

#### 3️⃣ WebMvcConfig를 구현한 Configuration 클래스를 만드는 방법
- WebMvcConfig 클래스를 활용하는 방법입니다. 
- WebMvcConfiguer를 implement한 클래스를 만들고, @Configuration 어노테이션으로 어플리케이션에 연결하는 방법입니다. 
- allowedOrigins, allowedMethods 메서드를 통해 cors를 설정해줄 수 있습니다.
- 간단한 코드로 전체범위의 CORS를 설정해 준다는 장점이 있습니다.

<details><summary>예시코드</summary>

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
</details>

<Br><Br>
## Bean에 대해 설명해보세요.
### 핵심답변
Spring Bean이란, IOC 컨테이너가 관리하는 자바 객체를 이야기합니다.
스프링 빈을 등록하는 방법은     
1. 컴포넌트 스캔을 사용하여 @Component 어노테이션으로 빈을 등록하거나       
2. @Configuration 과 @Bean 어노테이션을 사용하여 자바 코드를 직접 등록하는 방법        
3. 마지막으로, XML파일 설정을 통해 일반 객체를 Bean으로 등록할 수 있습니다.

<Br><Br>
#### 🤔 스프링 Bean을 사용하는 이유를 알려주세요
Spring Bean으로 등록되어 IOC 컨테이너에서 객체를 관리하게 되면, 
컨테이너에서 관리되는 객체를 사용하여, 코드에 의존성을 주입할 수 있습니다.

<br><br>
#### 🤔 스프링 Bean의 생성 과정을 설명해주세요.
Bean의 생명주기는     
1. spring 어플리케이션이 구동하면, Bean으로 등록할 객체를 탐색합니다.
2. Bean으로 등록할 객체를 초기화하고, 의존관계를 주입해 줍니다.
3. 모든 Bean의 초기화 끝나, 컨테이너에서 관리되며 사용가능한 상태를 bean 준비상태라 합니다.
4. 마지막으로, 스프릥 프로젝트가 종료될 때, destroy메소드가 호출되어 Bean을 소멸합니다.

<Br>

>[Bean LifeCycle](https://n1tjrgns.tistory.com/257)

<Br><Br>

#### 🤔 스프링 Bean의 Scope에 대해서 설명해주세요.
스프링에서 Bean의 Scope는 별다른 설정이 없으면, Singleton Scope로 설정 됩니다.        
싱글톤방식으로 설정이되면, 스프링이 bean마다 하나의 객체를 생성해주고, 스프링을 통해 Bean을 제공받으면,     
제공받은 Bean은 언제나 같은 객체임을 의미합니다.
<Br><Br>

#### 🤔 Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.
Spring Bean을 등록하는 방법은 2가지가 있습니다.    
첫 번째는, 컴포넌트 스캔을 이용하는 방법이고, 이는 @Component 어노테이션을 이용합니다.      
@Component 어노테이션은 클래스 단에 선언되며 스프링 런타임시 빈으로 등록이 됩니다.      
@Controller, @Service, @Repository 가 대표적인 컴포넌트 스캔 방식입니다.    

두 번째는, 자바클래스를 사용자가 직접 빈으로 등록하는 방법입니다.     
이때 @Bean 어노테이션을 사용합니다.     
@Bean어노테이션은 메소드 레벨에서 선언되며, 객체를 개발자가 수동으로 빈으로 등록하는 어노테이션입니다.

정리하자면,
Bean은 메소드에 사용하며, Component는 클래스에 사용이 됩니다.    
개발자가 컨트롤이 불가능한 외부 라이브러리를 빈으로 등록하고 싶을 때 @Bean을 사용하며,      
개발자가 직접 컨트롤이 가능한 내부 클래스의 경우 @Compoenet를 사용하여 스프링 빈으로 등록합니다.    

<br>

>[Bean과 Componet의 차이](https://youngjinmo.github.io/2021/06/bean-component/)

<Br><Br>

## Getter와 Setter를 사용해야하는 이유에 대해서 설명해주세요.
### 핵심답변

Getter와 Setter를 사용하는 이유는 데이터의 무결성을 지키기 위해서 입니다.

<br><br>
#### 🤔 데이터 무결성이 무엇이 인가요?
데이터 무결성이란, 데이터의 값과, 현실의 실제값이 일치하는 정확성을 의미합니다.  

<br><br>

#### 🤔 Getter/Setter를 사용할 때 왜 데이터 무결성이 지켜지나요?
getter, setter를 이용해서 데이터를 생성 및 접근을 하게 되면 들어오는 값을 바로저장하는게 아닌,      
한번 검증하고 처리할 수 있도록 할 수 있기때문에 데이터의 무결성이 지켜집니다.

<br><br>

#### 🤔 Getter/Setter를 사용할 때의 다른 이점은 없나요?
Getter Setter같은 엑세스 함수를 사용하면, 위와같은 데이터 무결성과 유효성검사를 할 수 있다는 장점과    
객체의 필드를 private와 같은 접근제한자를 두면서 객체지향의 목적인 정보은닉이 가능하다는 장점이 있습니다.

<br><br>
## Spring에서 데이터를 받는 방식(과정)과 종류에 대해서 설명해주세요.
### 핵심답변

<br><br>
## Spring에서 예외처리하는 방법에 대해서 설명해주세요.
### 핵심답변

<br><br>
#### 🤔 Spring Boot의 예외처리의 내부 구현은 어떻게 되어 있나요?

<Br><Br>
## Filter와 Interceptor 차이
### 핵심답변
<Br><Br>

#### 🤔 Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?

<Br><Br>
## Spring Application을 구동할 때 메서드를 실행시키는 방법에 대해 설명해주세요.
### 핵심답변

## DTO를 사용하는 이유?
### 핵심답변
DTO를 사용하는 이유는, 자바 Domain 객체에 직접적으로 접근하지 않기 위해서 입니다.      
데이터에 집적 접근하지 않음으로써, 데이터를 은닉 및 보호할 수 있고,

DTO를 사용하여, 간결하게 원하는 정보만을 제공해주거나     
엔티티의 정보뿐만이 아닌, 개발자가 원하는 형식의 데이터들을 추가하여 정보를 주고받을 수 있다는 편리함이 있습니다.

<Br><Br>
#### 🤔 DAO와 DTO의 차이를 설명해주세요
DTO는, 데이터 전송 객체의 약자로서, 데이터를 담아 보내는 객체입니다.    
DAO는, 데이터에 접근하는 객체로서, 데이터의 
<Br><Br>

<Br><Br>
## JPA

## JPA란?
### 핵심답변

<Br><Br>
#### 🤔 JPA를 사용할 때의 이점에 대해서 설명해주세요.
<Br><Br>
#### 🤔 JPA 영속성 컨텍스트의 이점(5가지)를 설명해주세요.
<Br><Br>
#### 🤔 JPA에서 N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.
<Br><Br>
#### 🤔 JPA를 사용할 때 쿼리를 사용하는 방법에 대해서 설명해주세요.
<Br><Br>
