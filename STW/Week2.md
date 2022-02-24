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
Field Injection은 의존성 주입이 너무 쉬워 무분별하게 의존성이 주입될 위험성이 있습니다.    
그렇게 되면 객체 지향 프로그래밍의 모든 클래스는 하나의 책임만을 가진다는 '단일 책임 원칙'이   
깨지기 쉽습니다. 이 경우 생성자 인자로 의존성과 설정값을 주입하면 의존성을 주입해야 하는    
대상이 많아질수록 생성자의 인자도 늘어나 의존관계의 복잡성을 쉽게 파악할 수 있게 됩니다.    
따라서 리팩토링이 필요한 경우 문제를 해결할 실마리를 얻기 쉽습니다.    
<br><br>

### MVC 패턴이란?

---
****핵심 답변****   
MVC 패턴은 개발 과정에서 상황에 따른 문제점들을 정리해 특정 규약을 통해 쉽게 쓸 수 있도록 만든 디자인 패턴 중의 하나입니다.
Model, View, Controller의 약자로 하나의 애플리케이션, 프로젝트를 구성할 때 구성 요소를 세가지 역할로 구분해준 패턴입니다.
![](https://images.velog.io/images/apolontes/post/d7ce7bf3-073b-49e8-8429-9de854f18865/2022-02-14_09-13-33.png)   
 -Model: 애플리케이션의 정보, 데이터를 나타냅니다. 또한 이러한 데이터를 가공하는 컴포넌트입니다. 
   ①사용자가 편집하기를 원하는 모든 데이터를 가지고 있어야 합니다.
   ②View나 Controller를 참조하는 내부 속성값을 가지면 안됩니다.
   ③변경이 일어나면, 이를 전달하고 변경 요청 이벤트를 받을 경우를 위해 수신 처리 방법도 구현해야 합니다.

 -View: 사용자 인터페이스 요소를 나타냅니다. 데이터 및 객체의 입출력을 담당합니다. 데이터를 기반으로 사용자들이 볼 수 있는 화면을 구성합니다.
   ①Model이 가지고 있는 정보를 따로 저장해서는 안됩니다.
   ②Model이나 Controller를 참조하거나 동작 등의 구성 요소를 알아서는 안됩니다.
   ③변경이 일어나면 이를 전달하는 변경 통지 방법을 구현해야 하고, 쉬운 정보 표현과 재사용이 가능한 설계가 필요합니다. 

 -Controller: 데이터와 사용자 인터페이스를 잇는 역할을 합니다. 사용자가 데이터를 클릭하고 수정하는 '이벤트'에 대한 처리를 합니다. 애플리케이션의 메인 로직을 담당합니다.
   ①Model과 View에 대해 알고 있어야 합니다. Controller는 이들을 중재해야 하기 때문입니다.
   ②Model과 View의 변경을 모니터링하고 변경 통지를 받으면 해석해서 각 구성 요소에 통지해야 합니다.
<br><br>    

**🤔 왜 MVC 패턴을 사용하나요?**   
사용자가 보는 페이지, 데이터 처리, 이를 중간에서 제어하는 컨트롤, 이 3가지로 기능을 분리하면     
각각 맡은 바에 집중하여 개발할 수 있어 효율적입니다.    
또한 유지보수성과 클라이언트의 요구사항을 반영하는 측면에서의 유연성이 증가하고 중복코딩도 해결할 수 있습니다.   

---
<br><br>

### 프론트 컨트롤러 패턴이란 무엇인가요?

---
****핵심 답변****  
MVC 디자인 패턴에서 수많은 View와 Controller가 연결되어 독립적으로 실행 되면, 서버 입장에서는   
웹 애플리케이션이 실행하는 것들을 일괄적으로 처리하기 어렵게 됩니다.    
따라서 대표 컨트롤러 역할을 할 수 있는 Front Controller를 두고 뷰에서 들어오는 모든 요청을 담당하게 하여    
웹 애플리케이션을 실행하는 모든 요청에 대한 일괄 처리를 하도록 하는 구조입니다.   

---
<br><br>

### Spring Web MVC의 Dispatcher Servlet의 동작 원리   

---
****핵심 답변****   
![](https://images.velog.io/images/apolontes/post/ce9004a8-4b64-4b94-b5dc-8e5c46c2ba4d/2022-02-14_22-38-16.png)   
DispatcherServelet은 프론트 컨트롤러 패턴을 구현한 Servlet으로,   
웹의 모든 요청은 서블릿 컨테이너(ex.Tomcat)가 받아 공통 작업은    
DispatcherServelet이 처리하고 결과를 돌려주는 창구 역할을 합니다.   

---
<br><br>

### AOP(Aspect Oriented Programming)란 무엇일까요?   

---
****핵심 답변****   
관점 지향 프로그래밍.    
어떤 로직이 있을 때 핵심적인 관점과 부가적인 관점을 나누고 그 관점을 기준으로 각각 모듈화해 나가는 개발을 말합니다.    
예컨대 소스 코드 중에서 자주 사용하고 반드시 필요하지만, 매번 하기 번거로운 반복적 코드가 있는데     
이를 Crosscutting Concerns(횡단 관심사)라고 부릅니다.(ex. log 출력, 예외처리, transaction etc)   
AOP관점에서는 이를 모듈화 해 핵심적인 비즈니스 로직(종단 관심사)과 분리합니다.    
이 경우 개발자는 핵심적인 비즈니스 로직에 더욱 집중하여 개발을 할 수 있게 됩니다.     

---
<br><br>

### Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.   

---
****핵심 답변****     
교차 출처 리소스 공유(Cross-Origin Resource Sharing)은 Origin이 다른 경우에도(Cross-Origin)       
리소스를 공유할 수 있음을 의미합니다. 하지만 웹브라우저는 원래 동일 출처 원칙(Same Origin Policy)을   
보안상의 이유로 요구합니다. CORS에러를 피하기 위해서는 request origin과 response origin을   
일치시키는 작업이 필요합니다.    
<br>    
Spring 에서는 아래의 3가지 방식으로 처리할 수 있습니다.    
1.CorsFilter를 생성해 직접 response에 header를 넣어주기    
2.Controller에서 @CrossOrigin annotation 추가하기   
3.WebMvcConfigurer를 이용해서 처리하기 

<Br><Br>

### Bean에 대해 설명해보세요.       

---
****핵심 답변****    
일반적으로 Java Bean은 Java로 작성된, 데이퍼 표현을 목적으로 하는 자바 클래스입니다.        
클래스의 멤버 변수는 properties라고 하며 private 접근 제한자를 갖습니다.        
이 properties는 getter와 setter로만 접근할 수 있고, 전달 인자(argument)가 없는        
기본 생성자(Default constructor)를 갖는 형태입니다.

```java
Java Bean 예시
public class AboutJavaBean {

	// 필드는 private로 선언
    private String bean;
    private int beanValue;

	// 전달 인자가 없는(no-argument) 생성자
    public AboutJavaBean() {
    
    }
		
	// getter
    public String getBean() {
        return beanName;
    }
    
	// setter
    public void setBean(String bean) {
        this.bean = bean;
    }

    public int getBeanValue() {
        return beanValue;
    }

    public void setBeanValue(int beanValue) {
        this.beanValue = beanValue;
    }
}
```
<Br><Br>

### 🤔 Spring Bean이란 무엇인가요?
스프링에서 Bean은 Spring IoC 컨테이너가 관리하는 Java 객체를 의미합니다.     
즉, 스프링에 의해 생성, 라이프 사이클 수행, 의존성 주입이 일어나는 객체들을 Spring Bean     
이라고 합니다. 자바 빈은 Class를 생성하고 new를 입력하여 원하는 객체를 직접 생성하지만,     
스프링은 ApplicationContect.getBean()와 같은 메서드를 사용해 스프링으로부터 직접        
자가 객체를 얻어서 사용합니다.
<Br><Br>

### 🤔 스프링 Bean의 생성 과정을 설명해주세요.
1.자바 어노테이션(Java Annotation)을 사용하는 방법      
Bean을 등록하기 위해 @Component 어노테이션을 사용합니다.     
이 어노테이션이 등록되어 있는 경우 스프링이 이를 확인하고 자체적으로 Bean을 등록합니다.     
@Component, @Controller, @Service, @Entity등의 어노테이션이     
내부적으로 @Component 어노테이션을 사용하는 예시입니다.
<br>
2.Bean Configuration File에 직접 Bean을 등록하는 방법
@Configuration과 @Bean 어노테이션을 이용해 Bean을 직접 등록할 수도 있습니다.
먼저 @Configuration을 이용해 Spring Project에서 Configuration역할을 하는        
Class를 지정합니다. 그리고 해당 File 하위에 Bean으로 등록하고자 하는 Class에        
@Bean 어노테이션을 지정하면 Bean을 등록할 수 있습니다.      
```java
@Configuration
public class HelloConfiguration {
    @Bean
    public HelloController sampleController() {
        return new SampleController;
    }
}
```

<Br><Br>

### 🤔 스프링 Bean의 Scope에 대해서 설명해주세요.
스프링은 빈으로 객체를 만들고 싱글톤화 시켜서 관리합니다. 싱글톤이란 기본 스코프로,     
스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프를 말합니다.      
여기에서 알 수 있듯이 스코프란 빈이 관리되는 범위를 말합니다. 스프링은 싱글톤 스코프        
외에도 프로토 타입 빈의 생성과 DI까지만 관여하는 매우 짧은 프로토타입 스코프도 갖고 있습니다.              
또한 웹 관련 스코프로 웹 요청이 들어오고 나갈때까지 유지되는 request scope,          
웹 세션이 생성되고 종료될 때까지 유지되는 session scope,        
웹의 서블릿 컨텍스트와 같은 범위로 유지되는 application scope가 있습니다.      
<Br><Br>

### 🤔 Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.
@Bean 어노테이션은 개발자가 컨트롤을 할 수 없는 외부 라이브러리들을 bean으로 등록하고       
싶을 때 사용하는 어노테이션입니다. 예를 들어 Spring Security에서 제공하는       
PasswordEncoder는 외부 클래스(라이브러리)이기 때문에 사용하기 위해서 bean       
어노테이션을 사용합니다.        
```java
@Bean
public PasswordEncoder passwordEncoder(){
    return new BCryptPasswordEncoder();
}
```         
@Component는 반대로 개발자가 직접 만들어 컨트롤할 수 있는 Class의 경우에 사용합니다.        
```java
@Component
@RequiredArgsConstructor
public class CustomAuthManager implements AuthenticationManager{

}
```


---
<Br><Br>

### Getter와 Setter를 사용해야하는 이유에 대해서 설명해주세요.
---
****핵심 답변****    
Setter를 사용하는 이유는 변수에 임의로 접근하여 잘못된 기본 값을 대입함으로써 에러를        
발생시키는 상황을 막기 위해서 입니다.
Getter를 사용하는 이유는 은닉성 때문입니다.		 
변수 중에서 다른 사람들이 필요로하는 최소한의 주요 변수만을 getter를 통해 드러내고 
나머지는 private 처리를 해서 해당 클래스 안에서만 노출되게 해줍니다.        
이렇게 Getter/Setter를 사용함으로써 데이터의 정확성과 일관성을 유지하고 보증하는        
무결성을 갖게 됩니다.
<br>

---
<br><br>

### Spring에서 데이터를 받는 방식(과정)과 종류에 대해서 설명해주세요.		
---
****핵심 답변****    
1.정적 컨텐츠: 파일을 그대로 웹 브라우저에 전달하는 방식입니다. 예를 들어 웹 브라우저에서       
hello.html을 요청하면 tomcat 내장 서버는 이 요청을 스프링에게 알립니다.     
스프링은 컨트롤러에 우선권을 주어 hello라는 메서드를 찾는데, 이 메서드가 있으면 실행하고        
없으면 resource/static에 있는 hello.html파일을 찾아 서버에 전달합니다.      
정적 컨텐츠이기 때문에 동적인 프로그래밍은 불가하다는 단점이 있습니다.
<Br><Br>
2.MVC와 템플릿 엔진: hello-mvc라는 요청이 들어오면 tomcat 내장 서버는 스프링 컨테이너       
에게 알립니다. helloController에 hello-mvc라는 메서드가 있으면 이를 실행합니다.       
<HelloController.java>   
```java
@GetMapping("hello-mvc")
public String helloMvc(@RequestParam("name") String name, Model model) {
    model.addAttribute("name", name);
    return "hello-template";
}
```
<hello-template.html>
```java
<html xmlns:th="http://www.thymeleaf.org">
<body>
<p th:text="'hello ' + ${name}">hello! empty</p>
</body>
</html>
```		
			
위와 같이 hello-mvc에서 model에 name이라는 키와 value값을 넘겨주면 viewResolver에서     
템플릿 엔진을 사용해 hello-template에 있는 name이라는 키를 요청 키 value값으로 변환해       
웹 브라우저에 전달합니다. 정적 컨텐츠와 달리 동적 프로그래밍이 가능해집니다.        
<Br><Br>
3.API: API는 json형태로 데이터를 바로 받습니다. @ResponseBody라는 태그를 이용합니다.        
웹 브라우저에서 hello-api를 요청하면 tomcat 내장 서버가 스프링 컨테이너에 알립니다.     
HelloController에서 hello-api 메서드가 있는지 확인하고, @ResponseBody라는       
어노테이션이 있다면 HttpMessageConverter로 전달해 json 형태로 데이터를 변환하여     
전달해 줍니다.
---
<br><br>

### Spring에서 예외처리하는 방법에 대해서 설명해주세요.
---
****핵심 답변****   
프로그램이 처리되는 동안 특정 문제가 발생 했을 때 처리를 중단하고 다른 처리를 하는 것을     
예외 처리라고 합니다. 스프링에서는 아래 3가지 방법으로 예외 처리를 하고 있습니다.        
1.Method level - try/catch를 사용       
2.Controller level - @ExceptionHandler를 이용       
3.Global level - controller 이후 Client에게 전달되기 직전 처리 @ControllerAdvice이용        

<br><br>

### 🤔 Spring Boot의 예외처리의 내부 구현은 어떻게 되어 있나요?

---
<Br><Br>

### DTO를 사용하는 이유?**
---
****핵심 답변****    
1.Entity 내부 구현을 캡슐화 할 수 있다.     
Entity는 도메인의 핵심 로직과 속성을 가지며, 실제 DB의 테이블과 매칭되는 클래스입니다.      
따라서 엔티티가 getter와 setter를 갖게 된다면 보안상 문제가 발생할 수 있고,     
비즈니스 로직과 크게 상관 없는 곳에서 리소스의 속성이 실수로라도 변경될 가능성이 있습니다.      
따라서 이를 방지하고자 Entity는 내부 구현을 캡슐화 하고, DTO를 사용하여 데이터 전달     
역할만을 맡기면 됩니다.     
<Br>
2.화면에 필요한 데이터를 선별할 수 있다.
애플리케이션이 확장되면 엔티티의 크기는 점차 커지며, view단도 다양해지며 API 스펙도     
더 많아질 것입니다. 이때 request/response를 엔티티로 보내면 엔티티의 모든 속성이        
함께 전송되기 때문에 속도가 느려집니다. 따라서 특정 API에 필요한 데이터를 포함해        
DTO를 만들면 화면에서 요구하는 데이터만 선별하여 request/response할 수 있습니다.        
<Br>
3.순환참조를 예방할 수 있다.        
양방향 참조된 엔티티를 컨트롤러에서 response로 return하게 되면, 엔티티가 참조하고 있는      
객체는 지연 로딩 되고, 로딩된 객체는 또 다시 본인이 참조하고 있는 객체를 호출하는 순환참조의        
문제를 낳습니다. 따라서 이를 방지하기 위해 return으로 DTO를 두는 것이 더 안전합니다.		
<Br>
4.validation 코드와 모델링 코드를 분리할 수 있다.       
엔티티 클래스는 db 테이블과 매칭되는 필드가 속성으로 선언되어 있고, 비즈니스 로직도 복잡합니다.     
따라서 속성에 모델링을 위해 @Column, @JoinColumn, @ManyToOne, @OneToOne     
등의 코드가 추가됩니다. 이때 @NotNull, @NotEmpty, @NotBlank같은 요청에 대한     
validation 코드가 들어가면 엔티티 코드가 더 복잡해질 것입니다. 따라서 validation을      
DTO에서 정의하면 엔티티는 모델링과 비즈니스 로직에 집중할 수 있도록 할 수 있습니다.
<Br><Br>

### 🤔 DAO와 DTO의 차이를 설명해주세요				
Data Access Object는 실제로 DB에 접근을 하기 위해 생성하는 객체이고,        
Data Transfer Object는 데이터 교환을 위해 사용하는 객체로, DB의 데이터를        
controller 혹은 service로 보낼 때 사용합니다. 
---
<Br><Br>

### Filter와 Interceptor 차이		
---
****핵심 답변****    
필터와 인터셉터는 모두 공통적으로 처리해야 하는 일들(ex.로그인 관련 세션 처리, 권한 체크,       
XSS 방어 등)을 처리하는 역할을 합니다.      
![](https://images.velog.io/images/apolontes/post/01c5865b-d1a7-4e6e-8f98-d8402e651c39/2022-02-15_21-27-54.png)     
필터는 디스패처 서블릿(Dispatcher Servlet)에 요청이 전달되기 전/후에 url 패턴에 맞는 모든 요청에 대해     
부가작업을 처리할 수 있는 기능을 제공해줍니다.      
반면 인터셉터는 Spring이 제공하는 기술로써, 디스패처 서블릿(Dispatcher Servlet)이 컨트롤러를 호출하기       
전과 후에 요청과 응답을 참조하거나 가공할 수 있는 기능을 제공합니다.        
즉 필터는 웹 컨테이너에서, 인터셉터는 스프링 컨테이너에서 동작한다는 차이가 있습니다.       
| 대상 | 필터(Filter) | 인터셉터(interceptor) |
| --- | --- | --- |
| 동작 | 웹 컨테이너 | 스프링 컨테이너 |
| Request/Response 조작 가능 여부 | O | X |
| 용도 | ①보안 관련 공통 작업 ②모든 요청에 대한 로깅 및 감사 ③이미지,데이터 압축 및 문자열 인코딩 | ①인증,인가 공통작업 ②Controller로 넘겨주는 정보 가공 ③API 호출에 대한 로깅 또는 감사 |


<Br><Br>

### 🤔 Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?		
동작 대상이 다르기 때문에 필터는 예외가 발생하면 Web Application에서 처리해야 합니다.       
<error-page>선언이나 필터 내에서 request.getRequestDispatcher(String)과 같이        
예외 처리 할 수 있습니다.       
반면 인터셉터는 스프링의 ServletDispatcher내부에 있으므로 @ConstrollerAdvice에서        
@ExceptionHandler를 사용해 예외처리 할 수 있습니다.     
---
<Br><Br>

### Spring Application을 구동할 때 메서드를 실행시키는 방법에 대해 설명해주세요.
---
****핵심 답변****    

---
<Br><Br>

## JPA

### JPA란?
---
****핵심 답변****    
JPA에는 '자바 ORM 표준'이라는 수식어가 붙습니다. ORM은 객체 관계 매핑의 약자로,     
객체는 객체대로 설계하고, 관계형 DB는 관계형 DB대로 설계한 후 ORM 프레임워크가      
중간에서 매핑해준다는 의미입니다.       
JPA(Java Persistence API)는 Java 진영에서 ORM 기술 표준으로 사용하는        
인터페이스의 모음입니다. Hibernate, OpenJPA등이 JPA를 구현합니다.       

<Br><Br>

### 🤔 JPA를 사용할 때의 이점에 대해서 설명해주세요.
1.생산성: 자바 컬렉션에 저장하듯이 JPA에 저장할 객체를 전달하면 되므로 반복적인 코드를      
개발자가 직접 작성하지 않아도 되기 때문에 객체 설계 중심의 개발이 가능합니다.     
<Br>  
2.유지보수: 필드 추가시 필요한 SQL 및 JDBC 코드를 JPA가 대신 처리해주어 개발자가 직접       
유지보수를 해야 할 필요성이 줄어듭니다.     
<Br>
3.패러다임 불일치 해결: JPA는 연관된 객체를 사용하는 시점에 SQL을 전달하고,     
같은 트랜잭션 내에서 조회할 때 동일성도 보장해 주어 다양한 패러다임 불일치를 해결합니다. 
<Br>       
4.성능 최적화: 같은 트랜잭션 안에서 같은 엔티티를 반환해 DB와의 통신 횟수를 줄여줍니다.     
또한 트랜잭션을 commit하기 전까지 쓰기 지연 메모리에 쌓아주었다가 한번에 SQL을 전송해 성능이 최적화 됩니다. 
<Br>      
5.데이터 접근 추상화와 벤더 독립성: 관계형 DB는 벤더마다 사용법이 달라 처음 선택한 DB에         
종속되는 문제가 발생합니다. JPA를 사용하면 Application과 DB 사이에서 추상화된 데이터 접근을     
제공하기 때문에 종속이 되지 않도록 합니다.
<Br><Br>

### 🤔 JPA 영속성 컨텍스트의 이점(5가지)를 설명해주세요.
영속성 컨텍스트는 엔티티를 영구 저장하는 환경이라는 뜻입니다. em.persist()를 통해       
객체를 저장하는 시점부터 영속성 컨텍스트에 관리되는 상태가 됩니다. 		     
1.1차 캐시   
영속성 컨텍스트의 관리되는 상태가 되면 DB에 바로 저장하는 것이 아니라 영속성 컨텍스트에     
의해 관리되고, 1차 캐시에서 조회가 가능합니다. 만약 DB에는 저장되어 있지만 1차 캐시에는     
데이터가 없다면 DB에서 조회해 가져온 뒤 1차 캐시에 저장하고 그 엔티티를 반환합니다.     
<Br>  
2.동일성 보장      
영속성 컨텍스트에서 관리되는 엔티티를 가져왔을 경우 동일성을 보장합니다.        
<Br>  
3.트랜잭션을 지원하는 쓰기 지연(Transaction write-behind)       
트랜잭션 commit 전까지 SQL을 쓰기 지연 메모리에 쌓아두었다가 commit시 한번에 전송해 통신 횟수를     
줄여 성능을 최적화 합니다.		
4.변경 감지(Dirty Checking)     
1차 캐시에 들어온 데이터를 스냅샷합니다. commit되는 시점에 엔티티와 스냅샷을 비교해       
변경이 일어나면 이를 감지합니다.      
5.지연 로딩     
엔티티에서 해당 엔티티를 불러올 때 SQL을 날려 해당 데이터를 가져옵니다.

<Br><Br>

### 🤔 JPA에서 N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.
N + 1 문제는 1번 조회해야 할 데이터를 N개 종류의 데이터 각각 추가로 조회하게 되는 문제입니다.       
문제는 N에 들어갈 숫자가 무한히 커지는 경우입니다. 이렇게 되면 성능에 큰 영향을 줄 수 있기 때문입니다.      
이 문제는 JPA의 프록시로 인한 지연 로딩 때문에 발생 합니다.     
해결 방법으로는     
1.Fetch Join        
2.FetchType을 LAZY에서 EAGER로 변경     
3.@EntityGraph 사용     
[참고 블로그](https://blog.advenoh.pe.kr/database/JPA-N1-%EB%AC%B8%EC%A0%9C-%ED%95%B4%EA%B2%B0%EB%B0%A9%EB%B2%95/)

<Br><Br>

### 🤔 JPA를 사용할 때 쿼리를 사용하는 방법에 대해서 설명해주세요.		
Spring Data JPA에서 정해놓은 네이밍 컨벤션을 지키면 JPA가 해당 메서드를 분석해 적절하게 JPQL을 구성합니다.          
대표적인 키워드로는 And, Or, Is, Equal, Between, LessThan, After, Before, IsNull                
OrderBy, Not 등이 있습니다.     
| Keyword | Sample | JPQL snippet |
| --- | --- | --- |
| And | findByLastnameAndFirstname | … where x.lastname = ?1 and x.firstname = ?2 |
| Or | findByLastnameOrFirstname | … where x.lastname = ?1 or x.firstname = ?2  |
| Is, Equals | findByFirstname,findByFirstnameIs,findByFirstnameEquals | … where x.firstname = ?1 |
| Between | findByStartDateBetween | … where x.startDate between ?1 and ?2 |
| LessThan | findByAgeLessThan | … where x.age < ?1 |
| After | findByStartDateAfter | … where x.startDate > ?1 |
| Before | findByStartDateBefore | … where x.startDate < ?1 |
| IsNull, Null | findByAge(Is)Null | … where x.age is null |
| OrderBy | findByAgeOrderByLastnameDesc | … where x.age = ?1 order by x.lastname desc |
| Not | findByLastnameNot | … where x.lastname <> ?1 |
        
[공식문서](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods.query-creation)
---
<Br><Br>

--- 
<Br><Br>
# 피드백 반영 자료 조사

# POJO
### 예상 추가질문
1. POJO와 Java bean, Spring bean는 같은 것들인가요?     
👉 아닙니다. POJO는 단어 그 자체로는 단순한 자바 객체(Plain Old Java Object)를 의미하지만, 객체 자체를 나타낸다기보다 객체지향적인 설계원칙에 충실하도록 개발되어 있는지, 테스트 코드 개발의 용이성이 있는지를 나타내는 조건에 가깝습니다. 예컨대 getter/setter를 가진 단순한 자바 오브젝트는 의존성이 없고 테스트가 용이한 특성을 가지고 있으므로 POJO라고 할 수 있습니다. 

# DI/IoC
### 예상 추가질문
1. IoC가 무엇인지는 아시는 것 같은데, IoC가 필요한 이유는 무엇인가요? 왜 외부에서 제어 흐름을 관리해야하죠?     
👉 객체 지향 원칙을 잘 지키기 위해 IoC가 필요합니다. 객체를 관리하는 프레임워크와 개발자가 개발해야 하는 필수 비즈니스 로직을 분리하여 결합도는 낮추고 응집도를 높여줄 수 있기 때문입니다. 이렇게 되면 변경해야 하는 사항에 유연하게 대처할 수 있게 되기 때문에 제어를 역전시켜 준 것입니다.
2. BeanFactory와 ApplicationContext는 각각 무엇인가요?      
👉  BeanFactory는 빈을 생성하고 의존 관계를 주입하는 기능을 담당하는 가장 기본적인 IoC 컨테이너, 클래스를 뜻합니다.     
👉 ApplicationContext란 BeanFactory를 구현하고 있는, BeanFactory의 확장된 버전이라고 이해할 수 있습니다. BeanFactory의 모든 기능을 포함하고 있으면서 Environment(Profile과 Source 설정, properties 값 불러오기 가능)나, MessageSource(메세지 설정파일을 localizing하는 i18n)을 제공하는 인터페이스)와 같은 추가 기능을 사용할 수 있으므로 특별한 이유가 없다면 BeanFactory보다 ApplicationContext를 사용하는 것이 더 바람직합니다.

# MVC - Dispatcher Servlet 동작 원리
### 예상 추가질문
1. Dispatcher Servlet은 어느 시점에 생성되나요?     
👉 Tomcat이 실행되어 web.xml파일을 통해 서블릿 컨텍스트를 초기화하는 시점에 옵션에 따라 lazy loading(클라이언트로부터 최초로 요청을 받을 때 서블릿 컨테이너는 DispatcherServlet에 대한 객체를 생성하고 다음 요청부터는 싱글톤으로 활용) 혹은 pre loading(서블릿 컨텍스트를 초기화하는 시점에 미리 DispatcherServlet 인스턴스를 생성) 방식으로 생성됩니다.

2. Dispatcher Servlet이 Controller 객체를 직접 메모리에 생성하나요? 직접 생성하지 않는다면 무엇이 그 역할을 수행하나요?       
👉 아닙니다. Front-Controller 역할을 하는 DispatcherServelt이 request를 받으면 DispatcherServelt은 적절한 controller를 선택하는 일을 HandlerMapping에게 요청합니다. HandlerMapping은 적합한 Controller를 선택합니다.
	
3. DispatcherServlet이 생성된 이후의 과정은 잘 알고 계신 것 같은데, 웹 어플리케이션이 실행된 이후부터 DispatcherServlet이 생성되기전까지 Spring framework가 어떤 준비를 하는지 설명해주실 수 있나요?        
👉 Tomcat(WAS)에 의해 web.xml이 로딩 -> web.xml에 등록된 ContextLoaderListener(Java Class) 생성 -> 생성된  ContextLoaderListener는 root-context.xml을 로딩 -> root-context.xml에 등록된 Spring Container가 구동 -> 클라이언트로부터 웹 어플리케이션 요청 -> DispatcherServlet이 생성됨
	
# AOP
### 예상 추가질문
1. 프로젝트에서 AOP를 활용한 부분이 있으실까요?
    - 사용자 인증과 로깅을 구현하셨던데 이건 AOP를 활용한 것이 아닌가요?		
	👉 맞습니다. AOP는 인증, 로깅, 트랜잭션 등 전체 시스템에 공통적으로 필요한 기능에 적용될 수 있습니다.핵심 기능과 횡단 관심사를 분리해 코드를 일일히 구현하는 대신 어드바이스로 정의해 코드의 특정 위치에 실행하기 위한 포인트컷을 정의해주기 때문에 이와같은 기능에 적용할 수 있습니다.		
	
    - 그럼 @Transactional 어노테이션은 AOP를 활용한 기능인가요?		
	👉 맞습니다. Spring에서 AOP는 Dynamic Proxy와 CGLIB (Byte Code Instrument) 두가지 방식으로 구현됩니다. 인터페이스를 클래스로 구현할 경우 Dynamic Proxy가, 단일 클래스는 CGLIB (Byte Code Instrument)를 사용합니다. 비즈니스 로직을 구현할 때 클래스보다 인터페이스로 유연하게 설계할 것을 권장하고 있으므로 인터페이스와 구현체로 이루어진 구성에서는 Dynamic Proxy를 통해 사용됩니다. 하지만 Spring Boot에서는 CGLIB가 예외를 덜 발생시키는 장점이 있어 CGLIB를 기본으로 적용하여 사용하는 것으로 알고 있습니다. 		[레퍼런스](https://private-space.tistory.com/98)

2. 만약 프로젝트의 모든 Entity에서 Entity 생성시간과 수정시간 필드를 사용한다면, 이 필드를 한 곳에서 관리할 수 있는 방법이 있을까요? Spring framework를 사용하는 환경입니다.        
👉 JPA Auditing을 사용하여 생성시간과 수정 시간을 자동화 할 수 있습니다. Domain 패키지에 BaseTimeEntity 클래스를 작성하고, 생성 및 수정 시간을 자동화 하고 싶은 Entity 클래스에 상속시킨 후 스프링 부트의 Main함수 클래스에 @EnableJpaAudting을 선언해 주면 됩니다. 

# Bean
### 예상 추가질문
1. Spring framework로 웹 어플리케이션을 개발할 때 Bean Scope 중 프로토타입 스코프는 어떤 경우에 활용하면 좋을까요?      
👉 프로토타입 스코프는 컨테이너에 빈을 요청할 때마다 매번 새로운 객체를 생성합니다. 또한 IoC 기본원칙을 따르지 않기에 생성 후 초기화와 DI까지는 이루어지지만 그 이후에는 컨테이너가 더이상 Bean Object를 관리하지 않습니다. 따라서 매번 새로운 객체가 필요하면서 DI를 통해 다른 Bean을 사용해야 할 경우 프로토타입 스코프를 활용할 수 있습니다. 예컨대 여러 사람이 같은 객체를 사용해야 하는 경우 요청시마다 Bean 객체가 생성되기 때문에 데이터 변경이나 충돌 현상을 방지할 수 있습니다.

# DTO
### 예상 추가질문
1. DTO 활용시의 Serialize/Deserialize와 ObjectMapper에 대해서
 - Serialize/Deserialize를 하는 이유        
 👉 직렬화는 자바 시스템 내부에서 사용되는 객체 또는 데이터를 외부 자바 시스템에서도 사용할 수 있도록 바이트(byte) 형태로 데이터를 변환하는 기술입니다. 이를 스트림화 한다고도 하는데, 데이터, 패킷 등을 일련의 연속성을 갖는 흐름으로 만들어 데이터가 잘 넘어갈 수 있도록 만들어주는 것입니다.  
객체(Object) 또는 데이터 (Data) -> 직렬화 -> Byte       
👉 역직렬화는 바이트로 변환된 데이터를 다시 객체로 변환하는 기술입니다.     
Byte -> 역직렬화 -> 객체(Object) 또는 데이터 (Data)
 - ObjectMapper     
 👉 JSON 컨텐츠를 Java 객체로 deserialize하거나, Java 객체를 JSON으로 serialization할 때 사용하는 Jackson 라이브러리의 클래스.
2. DTO로 넘긴 데이터가 어떻게 JSON 형식으로 변환되고, JSON 데이터가 어떻게 객체에 매핑되는지, 그 과정에서 어떤 라이브러리가 관여하는지.

