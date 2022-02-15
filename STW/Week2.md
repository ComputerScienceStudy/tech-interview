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
Getter를 사용하는 이유는 은닉성과 때문입니다. 
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
<br>
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
<br>
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
<br>
2.화면에 필요한 데이터를 선별할 수 있다.
애플리케이션이 확장되면 엔티티의 크기는 점차 커지며, view단도 다양해지며 API 스펙도     
더 많아질 것입니다. 이때 request/response를 엔티티로 보내면 엔티티의 모든 속성이        
함께 전송되기 때문에 속도가 느려집니다. 따라서 특정 API에 필요한 데이터를 포함해        
DTO를 만들면 화면에서 요구하는 데이터만 선별하여 request/response할 수 있습니다.        
<br>
3.순환참조를 예방할 수 있다.        
양방향 참조된 엔티티를 컨트롤러에서 response로 return하게 되면, 엔티티가 참조하고 있는      
객체는 지연 로딩 되고, 로딩된 객체는 또 다시 본인이 참조하고 있는 객체를 호출하는 순환참조의        
문제를 낳습니다. 따라서 이를 방지하기 위해 return으로 DTO를 두는 것이 더 안전합니다.
<br>
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

<Br><Br>

### 🤔 Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?

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


<Br><Br>

### 🤔 JPA를 사용할 때의 이점에 대해서 설명해주세요.

<Br><Br>

### 🤔 JPA 영속성 컨텍스트의 이점(5가지)를 설명해주세요.

<Br><Br>

### 🤔 JPA에서 N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.

<Br><Br>

### 🤔 JPA를 사용할 때 쿼리를 사용하는 방법에 대해서 설명해주세요.

---
<Br><Br>
