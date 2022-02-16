# Spring Framework
## POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?
### 핵심답변
POJO는 객체지향적 원리에 충실하고, 특정 규약과 환경에 종속되지 않게 재활용될 수 있는 방식으로 설계된 객체를 말합니다.     
POJO는 프레임워크 인터페이스, 클래스를 구현하거나 확장하지 않은 단순한 클래스로 Java에서 제공하는 API 외에 종속되지 않습니다.    
POJO로 개발하면, 특정 환경에 종속되지 않아 코드가 간결하고 테스트 자동화에 유리하며, 유지보수성을 높일 수 있습니다.        
스프링에서는 도메인과 비즈니스 로직을 수행하는 대상이 POJO대상이 될 수 있습니다.
<br><br>
#### 🤔 POJO의 예시
```java
import javax.jms.MessageListener; 
import javax.jms.Message;
import javax.jms.JMSException;

// 저수준의 기술과 환경에 종속적인 객체
public class OrderProcesser implements MessageListener {
    @Override
    public void onMessage(Message message) { 
        if (message instanceof TextMessage) {
            try {   
                    OrderPlaced event = OrderPlaced.fromJson(((TextMessage) message).getText()); // 주문 접수 처리하기
            } catch (JMSException error) {
                throw new RuntimeException("The message could not be read.", error);
            }
        } else {
            throw new IllegalArgumentException("Message must be of type TextMessage"); 
        }
    }
}
```
자바 엔터프라이즈 기술(= 트랜잭션, 보안, 메일, 메시징, 캐시와 같은 엔터프라이즈 애플리케이션에서 요구되는 기술) 중 하나인     
자바 메세지 서비스로 작성된 객체가 있습니다.         
이 객체는 자바 메세지 서비스 API를 사용해 메세지를 수신하고   
메세지에 담긴 JSON 데이터를 OrderPlaced 객체로 변환 후 비즈니스 로직을 처리합니다.    
그리고 메세지를 다룰 때 발생할 수 있는 checked exception도 처리하고 있습니다.
```java
import org.springframework.jms.annotation.JmsListener;

// 저수준의 기술과 환경에 종속되지 않게 설계된 객체
public class OrderProcesser {
    
    @JmsListener(destination = "pos") 
    public void accept(OrderPlaced event) {
        // 주문 접수 처리하기 
    }

}
```
아래는 스프링에 이식 가능한 서비스 추상화 기술을 사용해 작성된 POJO 방식의 코드입니다.   
annotation으로 메세지 수신을 선언하고 method parameter를 통해 수신 받은 데이터를 OrderPlaced 객체로 다루겠다고 작성 후          
바로 비즈니스 로직을 처리합니다.   
이렇듯 특정 기술과 환경에 종속되지 않는 객체는 깔끔한 코드가 될 수 있습니다.    

첫번째 코드와 같이 기술과 환경에 종속적인 객체가 비즈니스 로직과 함께 섞여 있으면 지저분한 코드가 발생합니다.    
읽고 이해하기도 어려울 뿐더러 검증이나 테스트 작성에도 어려움이 있으므로 유지 보수에 큰 부담이 됩니다.    
스프링은 엔터프라이즈 애플리케이션 개발의 모든 영역과 계층에서 POJO 방식의 구현이 가능하도록 만들어졌습니다.    
이를 이용하면 POJO 프로그래밍의 장점을 그대로 살려 엔터프라이즈 애플리케이션의 핵심 로직을 객체 지향적인 POJO 기반으로 깔끔하게 구현하고            
동시에 엔터프라이즈 환경에 각종 서비스와 기술적인 필요를 POJO 방식으로 만들어진 코드에 적용할 수 있습니다.
<br><br>
#### 📚 유익했던 자료
- [Plain old Java Object](https://en.wikipedia.org/wiki/Plain_old_Java_object)
- [당신의 코드는 POJO하신가요?](https://www.youtube.com/watch?v=5NcqgXgmmjg&t=2863s)
---
<br><br>

## Spring DI/IoC는 어떻게 동작하나요?
### 핵심답변
IoC(제어의 역전)은 프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부에서 관리하는 것으로 코드의 최종호출은 개발자가 제어하는 것이 아닌 프레임워크의 내부에서 결정된 대로 이루어집니다.       
스프링에서는 스프링 컨테이너에서 객체 생성 및 관리를 합니다.

DI(의존관계 주입)은 Spring 프레임워크에서 지원하는 IoC의 형태로 클래스 사이의 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 자동으로 연결해줍니다.

스프링에서는 스프링 컨테이너 ApplicationContext를 이용하여 설정 정보를 생성, 등록하고 필요한 객체를 생성자 혹은 setter를 통해 주입합니다.
<br><br>
#### 🤔 IoC 컨테이너의 역할은 무엇이 있을까요?
애플리케이션 실행시점에 빈 오브젝트를 인스턴스화하고 DI 한 후에 최초로 애플리케이션을 기동할 빈 하나를 제공해줍니다.
<br><br>
#### 🤔 IoC를 Spring에서 왜 사용했을까요? (= IoC의 이점은 무엇인가요?)
수많은 객체들을 편리하게 관리하고 변경에 유연한 코드 구조를 가져가기 위함입니다.    

IoC의 예시 중 하나는 개발자가 직접 객체를 관리하지 않고 스프링 컨테이너에서 직접 객체를 생성하여 해당 객체에 주입 시키는 것입니다.    
작성하고자 하는 코드에서 객체 생성, 소멸 등 객체를 관리하는 코드와 함께 비즈니스 코드까지 같이 있으면, 변경이 어렵습니다.            
객체를 관리해주는 컨테이너와 그 외 내가 구현 하고자 하는 부분으로 각각 관심을 분리하면, 변경에 유연한 코드를 작성 할 수 있는 구조가 되기 때문에 제어를 역전합니다.
<br><br>
#### 🤔 의존관계는 무엇인가요?
어떤 클래스가 다른 클래스에 접근할수 있는 경로를 가지거나 해당 클래스의 객체의 메소드를 호출하는 경우, 두 클래스 사이에 의존 관계가 있다고 말합니다.
의존 관계는 객체와 객체 사이에 협력하는데 반드시 필요합니다.      
하지만 과도한 의존 관계 애플리케이션을 수정하기 어렵게 만듭니다.
<br><br>
#### 🤔 DI란 무엇인가요?
DI는 외부의 독립적인 존재가 객체를 생성한 후 이를 전달해서 의존 관계를 해결하는 방법을 말합니다.    
의존 관계를 관리하는 것이고, 객체가 변경을 받아들일 수 있게 의존 관계를 정리하는 기술이라고 할 수 있습니다.          
외부에서 의존 관계 대상을 해결한 후 이를 사용하는 객체 쪽으로 주입하기에 DI라고 부릅니다.
<br><br>
#### 📚 유익했던 자료
- [IoC, DI란 무엇일까](https://biggwang.github.io/2019/08/31/Spring/IoC,%20DI%EB%9E%80%20%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C/)
- [의존성 주입(Dependency Injection, DI)이란? 및 Spring이 의존성 주입을 지원하는 이유 - (1/2)](https://mangkyu.tistory.com/150)

---
<br><br>

## Spring IoC/DI(의존성 주입)의 방법에 대해 아는대로 설명해주세요.
### 핵심답변
DI는 세가지 방법이 있습니다. 생성자 삽입, Setter를 이용한 메소드 매개 변수 삽입, 필드 주입이 있습니다.
- 생성자 주입은 생성자 호출시점에 딱 1번만 호출되는 것을 보장하며 불변, 필수 의존관계에 사용합니다.
- Setter주입은 선택, 변경 가능성이 있는 의존관계에 사용되며 스프링빈을 선택적으로 등록이 가능합니다.
- 필드 주입은 `@Autowired` 를 사용하는데 외부에서 변경이 불가능하여 테스트 하기 힘듭니다.
  <br>DI 프레임워크 없이는 작동하기 힘들며, 주로 애플리케이션과 관계없는 테스트코드나 `@Configuration` 같은 스프링 설정 목적으로 사용합니다.
<br><br>
#### 🤔 각 DI 주입 방식의 차이점과 이점에 대해서 설명해주세요.
<br><br>
#### 🤔 의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.
모든 의존성을 생성자를 통해 주입하면, 인스턴스 생성 시 즉시 어떠한 동작을 실행할 수 있습니다.      
또한 추가적인 설정은 필요하지 않으며, 뜻하지 않게 의존성과 설정값을 빠뜨리는 일이 발생하지 않고 테스트에도 용이합니다.
<br><br>
#### 🤔 생성자 주입은 언제 사용할까요?
<br><br>
#### 🤔 Setter 주입은 언제 사용할까요?
<br><br>
#### 📚 유익했던 자료
- [세 가지 DI 컨테이너로 향하는 저녁 산책](https://www.nextree.co.kr/p11247/)
- [DI 기초](https://github.com/cheese10yun/TIL/blob/master/Spring/IoC/DI-%EA%B8%B0%EC%B4%88.md)
- [스프링 - 생성자 주입을 사용해야 하는 이유, 필드인젝션이 좋지 않은 이유](https://yaboong.github.io/spring/2019/08/29/why-field-injection-is-bad/)
- [다양한 의존성 주입 방법과 생성자 주입을 사용해야 하는 이유 - (2/2)](https://mangkyu.tistory.com/125)
---
<br><br>

## MVC 패턴이란?
### 핵심답변
MVC 패턴은 애플리케이션을 Model, View, Controller 이 3가지 역할로 구분한 개발 방법론입니다.
- Model은 데이터와 행동을 갖는 객체로서, 비즈니스 로직을 수헹합니다.
- View는 데이터의 시각화로, 모델이 처리한 데이터를 받아서 사용합니다.
- Controller는 사용자의 요청을 해석하여 처리하고 결과를 반환합니다.
  <br>Model과 View의 사이를 연결해주며, 데이터의 흐름을 제어합니다.
<br><br>
#### 🤔 MVC 패턴을 사용하는 이유는 무엇일까요?
MVC 패턴을 사용하지 않는 경우에는 로직 코드와 출력 코드가 한 페이지에 삽입된 형태였습니다.   
이 경우에는 유지 보수가 어렵다는 단점이 있습니다.    
요소와 기능이 많아지고 구조가 이것 저것 얽힐 수록 코드가 길어지고 난해해지기 때문입니다.          
거대해지고 복잡해질 경우 특정 기준으로 분리, 모듈화해서 접근을 합니다.      
그 중에 하나의 패턴이 MVC 패턴입니다.     
MCC 패턴을 사용함으로써, 책임이 구분되어 있어, 코드 수정하는 것이 편하고 개발하기가 쉬워집니다.      
또한, 논리적인 관련있는 기능을 하나의 컨트롤러로 묶거나, 특정 모델과 관련있는 뷰를 그룹화하여, 결합도를 높일 수 있습니다.
<br><br>
#### 🤔 MVC 패턴의 동작 과정은 어떻게 되나요?
<img src="https://t1.daumcdn.net/cfile/blog/13705949504C57EB0E?original" width="600">

사용자가 입력을 담당하는 View를 통해 요청을 보내면 해당 요청을 Controller가 받고,       
Controller는 Model을 통해 데이터를 가져오고, 해당 데이터를 바탕으로 출력을 담당하는 View를 제어해서 사용자에게 전달합니다.
<br><br>
#### 🤔 Model, View, Controller 자세히
###### Model
- Model이란?
  - 도메인 객체 또는 DTO로 화면에 전달할 또는 화면에서 전달 받은 데이터를 담고 있는 객체
  - 모델의 상태에 변화가 있을 때 컨트롤러와 뷰에 이를 통보할 수도 있고, 반대로 컨트롤러와 뷰가 직접 모델의 상태를 읽어오기도 한다.
  - Model은 사용자에게 어떻게 보일지에 대해 신경쓰지 않아도 되고, 모델은 순수하게 public 함수로만 이루어져 있다. (POJO)
- 구성 요소
  - Service : DB 트랜잭션 처리와 도메인에게 비즈니스 로직 처리를 위임
  - 도메인 객체 : 비즈니스 로직을 수행
  - DAO(or Repository) : DB CRUD
  - DTO : Layer간 통신용
###### Controller
- Controller란?
  - 사용자 입력을 받아 모델 객체의 데이터를 변경하거나, 모델 객체를 뷰에 전달하는 역할
  - 클라이언트의 요청을 받았을 때 그 요청에 대해 실제 업무를 수행하는 모델 컴포넌트를 호출하는 일을 한다.
  - 클라이언트가 보낸 데이터가 있다면, 모델을 호출할 때 전달하기 쉽게 데이터를 적절히 가공하는 일을 한다.
  - 모델이 업무 수행을 완료하면, 그 결과를 가지고 화면을 생성하도록 뷰에 전달한다.
- 책임
  - 입력값 검증 
  - 입력 받은 데이터로 모델 객체 변경 
  - 변경된 모델 객체를 뷰에 전달 
  - Service Layer에 비즈니스 로직 처리 요청
    → Service는 도메인 객체를 통해 비즈니스 로직 처리후 결과 반환
###### View
- View란?
  - 데이터를 보여주는 역할
  - 다양한 형태로 보여줄 수 있다.
- 예시
  - HTML, JSON, XML, JSP, Thymleaf 등
<br><br>
#### 📚 유익했던 자료
- [[10분 테코톡] 🐝범블비의 MVC Pattern](https://www.youtube.com/watch?v=es1ckjHOzTI&list=PLgXGHBqgT2TvpJ_p9L_yZKPifgdBOzdVH&index=138&t=369s)

---
<br><br>

## 프론트 컨트롤러 패턴이란 무엇인가요?
### 핵심답변
프론트 컨트롤러 하나가 서블릿 컨테이너의 제일 앞에서 서버로 들어오는 클라이언트의 모든 요청을 처리하도록 디자인한 패턴을 말합니다.     
프론트 컨트롤러 패턴은 MVC 구조에서 함께 사용되는 디자인 패턴입니다.          

개발할 때 사용하는 MVC 디자인 패턴에서 컨트롤러는 뷰에서 요청이 들어왔을 때 요청을 받아 처리합니다.      
그런데 하나의 웹 애플리케이션에는 많은 뷰와 컨트롤러가 존재해서 각각의 뷰와 컨트롤러가 연결되어 독립적으로 실행되면,     
서버 입장에서는 현재 웹 애플리케이션 실행에 대하여 일괄적으로 처리하기 어렵습니다.

이럴 때 대표 컨트롤러(Front Controller)를 두고 뷰에서 들어오는 모든 요청을 담당하여       
웹 애플리케이션을 실행하는 모든 요청을 일괄적으로 처리할 수 있습니다.

이러한 구조를 '프론트 컨트롤러 패턴'이라고 합니다.
<br><br>
#### 🤔 스프링 MVC 프레임워크는 프론트 컨트롤러 패턴을 어떻게 사용할까?
프론트 컨트롤러 패턴을 사용한 대표적인 프레임워크는 스프링 MVC 프레임워크 입니다.     
스프링이 프론트 컨트롤러를 사용하는 경우는 Servlet에서 확인할 수가 있습니다.      

<img width="600" src="https://blog.kakaocdn.net/dn/cJHUnM/btq4yk2X0Tv/OVWBm9TH6qvJDk1bdjLfDK/img.png">

Servlet은 동적인 페이지를 만들기 위해, 웹 서버에 붙이는 프로그램 중 하나인데,             
Servlet을 이용해서 웹 요청을 다루게 되면, 개발자들이 처리 로직에 집중할 수 있습니다.      

그러나, 요청당 서블릿을 정해주는 곳에는 되게 비효율적인 부분이 있었습니다.        
관리의 측면에서는 멀티 스레딩을 다뤄야 한다는 어려움이 있고,    
개발의 측면에서는 핸들러의 공통 로직이 매번 중복된다는 문제가 있었습니다.                    
(요청마다 서블릿을 정의하고, 요청을 수행할 때마다 매번 스레드를 생성)      

<img width="600" src="https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwQuP6%2Fbtq4Cq2vafc%2FVNito9BZcudNgGyitMKRuK%2Fimg.png">

이제는 하나의 서블릿만 정의하고 그 서블릿이 모든 요청을 수행할 수 있도록 하는 전략이 생겼습니다.       
이때, 모든 요청을 처리하는 프론트 컨트롤러는 Dispatcher Servlet입니다.
<br><br>
#### 🤔 Spring Web MVC에서 요청 마다 Thread가 생성되어 Controller를 통해 요청을 수행할텐데, 어떻게 1개의 Controller만 생성될 수 있을까요?

<br><br>
#### 📚 유익했던 자료
- [[10분 테코톡] 🐶 코기의 Servlet vs Spring](https://www.youtube.com/watch?v=calGCwG_B4Y&list=PLgXGHBqgT2TvpJ_p9L_yZKPifgdBOzdVH&index=63&t=50s)

---
<br><br>

## Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.
### 핵심답변
Dispatcher Servlet은 모든 요청을 처리하는 프론트 컨트롤러입니다.        
Spring Web MVC의 Dispatcher Servlet의 동작 원리는 다음과 같습니다.

1. 브라우저의 모든 요청이 Dispatcher Servlet에게 전달됩니다.
2. Dispatcher Servlet은 요청을 처리할 핸들러를 Handler Mapping에게 물어봄으로써, Handler를 찾습니다.
3. 해당 Handler를 실행 할 수 있는 Handler Adapter를 찾습니다.
4. 찾아낸 Handler Adapter를 사용해서 Handler의 응답을 처리합니다.
5. 부가적으로 예외가 발생했다면, 예외 처리 핸들러에 요청 처리를 위임합니다.
6. ViewResolver를 통해 Handler의 리턴값을 보고 어떻게 처리할지를 판단합니다.
이때, 뷰 이름에 해당하는 뷰를 찾아 모델 데이터를 렌더링 합니다.
@ResponseBody가 있다면, Converter를 이용해서 응답 본문을 만듭니다.
7. 최종적으로 응답을 보냅니다.
<br><br>
#### 🤔 Spring Web MVC의 Dispatcher Servlet의 동작원리 자세히 설명해주세요.
<img width="1000" src="https://github.com/cheese10yun/TIL/raw/master/assets/spring-mvc-flow.png">

1. 브라우저의 모든 요청이 Dispatcher Servlet에게 전달됩니다. 
2. Dispatcher Servlert이 요청을 받으면 그 요청을 처리할 수 있는 Hanlder의 이름을 Handler Mapping 에게 물어봅니다. 
3. Handler Mapping은 요청 URL을 보고 Handler를 판단하고 Handler Name을 과 함께 제어권을 Dispacher Servlet에게 넘겨줍니다.
4. Handler 실행 전에 전처리, 후처리로 실행해야할 인터셉터 목록을 결정합니다.
5. Service의 비즈니스 로직을 실행합니다.
6. Handler는 랜더링해야하는 View Name을 판단해서 Dispatcher Servlet에 전송합니다.
7. Dispatcher Servlet은 View name을 View Resolver에 전달합니다.
8. View Resolver는 전달받은 값으로 적절한 View를 생성하여 Dispatcher Servlet에 전달합니다.
9. Dispatcher Servlet은 View에 Model과 Controller를 전달합니다.
10. View로 부터 받은 응답을 클라이언트에게 전달합니다.
<br><br>
#### 🤔 인터셉터는 무엇인가요?
스프링 MVC 모듈에서 인터셉터를 이용해서 컨트롤러가 요청을 처리하기 전 혹은 후에 대한 로직을 추가할 수 있습니다.         
컨트롤러가 실행되기 전에 인터셉터를 실행할 수 있음으로 주로 특정 URI에 대한 공통 로직 적용이 필요한 경우에 유용합니다.
<br><br>
#### 🤔 DispatherServlet 구성 요소
- HanderMapping
  - 요청을 처리할 핸들러를 찾는 인터페이스 
- HandlerAdapter 
  - HandlerMapping이 찾아낸 핸들러를 처리하는 인터페이스
  - 스프링 MVC 확장력의 핵심 (Why? 컨트롤러가 실행되기 전 Intercepter를 실행해서 특정 URI에 대한 공통 로직 적용할 수 있기 때문이다.)
- ViewResolver
  - 뷰 이름에 해당하는 뷰를 찾아내는 인터페이스
<br><br>
#### 📚 유익했던 자료
- [Spring MVC의 핵심 객체 DispatcherServlet에 대한 모든 것(DispatcherServlet이 하는 역할 정리, 동작 프로세스)](https://jeong-pro.tistory.com/225)
- [스프링 MVC](https://github.com/cheese10yun/TIL/blob/master/Spring/mvc/mvc-basic.md)
- [Spring MVC 흐름](https://github.com/cheese10yun/TIL/blob/master/Spring/mvc/mvc-flow.md)
- [Spring 웹 MVC 강의 정리](https://github.com/cheese10yun/TIL/blob/master/Spring/mvc/Spring-%EC%9B%B9MVC-%EA%B0%95%EC%9D%98-%EC%A0%95%EB%A6%AC.md)

---
<br><br>

## AOP(Aspect Oriented Programming)란 무엇일까요?
### 핵심답변
여러 layer에 걸친 공통된 관심사 분리하는 것을 말합니다.      
여러 layer에 걸친 공통된 관심사를 분리하면, 애플리케이션의 부가 기능을 모듈화하고, 핵심기능과 상호작용 할 수 있게 합니다.    
스프링은 IoC/DI를 이용해 프락시 기반 관점 지향 프로그래밍을 지원합니다.


<br><br>
#### 🤔

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료
- 클린 코드 11장 시스템

---
<br><br>

## Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.
### 핵심답변
- Servlet Filter를 사용하여 커스텀한 CORS 설정하는 방법이 있습니다. 
- Controller 클래스에 @Crossorigin 어노테이션을 통해 해결할 수 있습니다.
- WebMvcConfiguer를 구현한 Configuration 클래스를 만들어서 addCorsMappings()를 재정의할 수도 있습니다. 
- 마지막으로 Spring Security에서 CorsConfigurationSource를 Bean으로 등록하고 config에 추가해줌으로써 해결할 수 있습니다.
<br><br>
#### 1️⃣ Servlet Filter를 사용하여 커스텀한 CORS 설정하는 방법
서버의 응답을 보내기 전에 Access-Control-Allow-Origin 헤더를 싣는 필터를 작성하는 방법입니다.   
```java
import org.springframework.core.Ordered;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

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
이 방법은 실제로 응답 헤더에 실릴 값들을 모두 설정해줍니다.    
복잡한 설정이 필요한 경우에 사용하면 좋을 것 같습니다.
<br><br>
#### 2️⃣ Controller 클래스에 @Crossorigin 어노테이션을 활용하는 방법
Controller 클래스 상단이나 Controller Mapping 메소드 상단에 CrossOrigin(origins="도메인 url")을 어노테이션으로 작성하는 방법입니다.   
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
1번 방법에 비해, 코드가 간결하고, 어노테이션 형태라 사용할 곳에 붙여 쓰면 되어 편리합니다.     
메소드 단위로 어노테이션을 사용할 수 있는 것은 AWS Lambda로 API를 개발할 때 유용할 것 같습니다.      
<br><br>
#### 3️⃣ WebMvcConfig를 구현한 Configuration 클래스를 만드는 방법
WebMvcConfig 클래스를 활용하는 방법입니다.   
WebMvcConfiguer를 implement한 클래스를 만들고, @Configuration 어노테이션으로 어플리케이션에 연결하는 방법입니다.      
allowedOrigins, allowedMethods 메서드를 통해 cors를 설정해줄 수 있습니다.   
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
프로젝트 때, 3번 방법을 활용했습니다.    
간단한 코드로 전체 범위의 CORS를 설정해줄 수 있어서 선택했습니다.
<br><br>
#### 📚 유익했던 자료
- [CORS를 해결하는 3가지 방법](https://wonit.tistory.com/572)
- [CORS는 왜 이렇게 우리를 힘들게 하는걸까?](https://evan-moon.github.io/2020/05/21/about-cors/)

---
<br><br>

## Spring Bean이란 무엇인가요?
### 핵심답변

<br><br>
#### 🤔 스프링 Bean의 생성 과정을 설명해주세요.

<br><br>
#### 🤔 스프링 Bean의 Scope에 대해서 설명해주세요.

<br><br>
#### 🤔 Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.

<br><br>
#### 📚 유익했던 자료


---
<br><br>

## Getter와 Setter를 사용해야하는 이유에 대해서 설명해주세요.
### 핵심답변

<br><br>
#### 🤔

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료


---
<br><br>

## Spring에서 예외처리하는 방법에 대해서 설명해주세요.
### 핵심답변
스프링에서 예외처리는 크게 3가지로 나눌 수 있습니다.                
정확히는 DispatcherServlet에서 발생하는 예외를 HandlerExceptionResolver가 처리하는 처리 방법들입니다.             
Controller Level에서 처리하는 방법, Global Level에서 처리하는 방법, Method Level에서 처리하는 방법이 있습니다.       
<br><br>
#### 1. Controller Level에서 처리 - @ExceptionHandler       
@ExceptionHandler 어노테이션을 통해 Controller의 메서드에서 throw된 Exception에 대한 공통적인 처리를 할 수 있습니다.     
###### 예시
```java
@RestController
public class TestController {

    private final Logger logger = LoggerFactory.getLogger(UserController.class);

    // 예외 핸들러
    @ExceptionHandler(value = TestException.class)
    public String controllerExceptionHandler(Exception e) {
        logger.error(e.getMessage());
        return "/error/404";
    }

    @GetMapping("hello1")
    public String hello1() {
        throw new TestException("hello1 에러 "); // 강제로 예외 발생
    }

    @GetMapping("hello2")
    public String hello2() {
        throw new TestException("hello2 에러 "); // 강제로 예외 발생
    }
}
```

TestController내에서 발생하는 TestException에 대해서 예외가 발생하면 `controllerExceptionHandler`메서드에서 모두 처리해준다.

- Controller 메서드 내의 하위 서비스 (Service, Repository등등)에서 예외가 발생하더라도, 중간에 처리하지 않는 이상 Controller단까지 예외가 던져지게 되고 `@ExceptionHandler`가 예외를 처리하게 된다.
  - Checked Exception, Runtime Exception 상관 없이 Controller 단까지 예외를 throw하면 처리가 가능하다.
<br><br>
#### 2. Global Level에서 처리 - @ControllerAdvice                     
만약 하나의 Controller말고 여러 Controller에서 발생하는 예외를 처리하려면 @ControllerAdvice를 사용해야 합니다.          
@ControllerAdvice는 DispatcherServlet에서 발생하는 예외만 처리할 수 있습니다. 필터에서 발생하는 예외는 따로 처리해주지 않으면 처리가 불가능 합니다.

###### 종류
- @ControllerAdvice
  -모든 Controller에서 발생하는 예외를 처리할 수 있게 해주는 애노테이션
  - DispatcherServlet에서 발생하는 예외를 전역적으로 처리해준다.
- @RestControllerAdvice
  - @ControllerAdvice + @ResponseBody
  
###### 예시
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    private final Logger logger = LoggerFactory.getLogger(GlobalExceptionHandler.class);

    @ExceptionHandler(value = TestException.class)
    public String testExceptionHandler(Exception e) {
        logger.error(e.getMessage());
        return "/error/404";
    }
}
```
- Controller에서 발생하는 예외를 전역적으로 처리해준다.
<br><br>
#### 3. Method Level에서 처리 - try/catch     
try catch를 최대한 지양하는 패턴입니다. 왜냐하면, 이미 예외가 발생했음에도 불가하고 다음 로직을 실행하게 되기 때문입니다.          
하지만, Checked Exception 같은 경우에는 예외를 반드시 감싸야 하므로 이러한 경우에는 try catch를 사용해야 합니다. <br>
try catch를 사용하게 된다면 더 구체적인 Exception을 발생시키는 것이 좋습니다.      

###### 예시
```java
try {
    // 비즈니스 로직 수행...
}catch (Exception e){
    e.printStackTrace();
}
```
```java
try {
    // 비즈니스 로직 수행...
}catch (Exception e){
    e.printStackTrace();
    throw new XXX비즈니스로직예외(e);
}
```
<br><br>
#### 🤔 Controller의 `@ExceptionHandler`와 ControllerAdvice의 `@ExceptionHandler`중 높은 우선순위는?
- Controller의 `@ExceptionHandler`가 먼저입니다.
<br><br>
#### 🤔 스프링 예외 발생 위치는 어디에 있고, 각각 처리 방법은 무엇인가요?
스프링의 처리과정을 보면 예외가 발생하는 부분은 크게 두가지로 나눌 수 있습니다.       

<img width="600" src="https://terasolunaorg.github.io/guideline/5.3.0.RELEASE/en/_images/exception-handling-description-target.png">

Dispatcher Servlet내에서 발생하는 예외 (Controller, Service, Repository등등)와 <br>
Dispatcher Servlet전의 서블릿 (Filter)에서 발생하는 예외가 있습니다. <br>

###### DispatcherServlet 예외
DispatcherServlet내에서 발생하는 예외는 내부에서 자체적으로 해결할 수 있습니다.
바로 HandlerExceptionResolver를 사용한 예외 전략입니다.      

###### Filter 예외
클라이언트의 요청을 DispatcherServlet 밖에서 처리하는 도중 예외가 발생하면 DispatcherServlet이 예외를 처리해줄 수 없습니다.           
즉, HandlerExceptionResolver의 처리를 받을 수 없습니다.
처리 못하는 이유는 DispatcherServlet에서 처리하기도 전에 예외가 발생되기 때문입니다.
Filter 예외가 발생하면, Web Application 레벨에서 처리해줘야 합니다.          

Web Application 레벨에서 처리해줄 수 있는 방법은 크게 3가지가 있습니다.      
1. web.xml에 error-page를 잘 등록해줘서 에러를 사용자에게 응답
2. Filter 내부에서 예외를 처리하기 위한 필터를 따로 둬서 try-catch문을 사용하여 예외 처리 
<br>실제 시큐리티 인가 처리중 예외가 발생하면 ExceptionTranslationFilter에게 예외를 던져 처리한다. (try-catch)
3. Filter 내부에서 try-catch 구문을 통해 예외 발생 시, HandlerExceptionResolver를 빈으로 주입받아 @ExceptionHandler에서 처리하는 방법
<br>즉, 필터에서 발생하는 예외를 DispatcherServlet의 예외 처리기인 HandlerExceptionResolver에 보내서 처리하는 방식이다.
```java
// 자바 시큐리티 설정
@Configuration
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

    @Autowired
    private FilterChainExceptionHandler filterChainExceptionHandler;

    @Override
    protected void configure(HttpSecurity http) throws Exception {
      	// 필터 앞에 FilterExceptionHandler를 추가해준다.
        http
            .addFilterBefore(filterChainExceptionHandler, xxx.class) 
            (...)
    }
}
```
```java
@Component
public class FilterChainExceptionHandler extends OncePerRequestFilter {
  private final Logger log = LoggerFactory.getLogger(getClass());

  @Autowired
  private HandlerExceptionResolver resolver; // HandlerExceptionResolver를 빈으로 주입 받는다.

  @Override
  protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
    throws ServletException, IOException {

    // 다음 필터를 호출하기 전에 doFilter를 try/catch문으로 감싼다.
    try {
      filterChain.doFilter(request, response);
    } catch (Exception e) {
      log.error("Spring Security Filter Chain Exception:", e);
      resolver.resolveException(request, response, null, e);
    }
  }
}
```
<br><br>
#### 🤔 HandlerExceptionResolver에 대해 구체적으로 설명해주세요.
https://joont92.github.io/spring/HandlerExceptionResolver-LocaleResolver-MultipartResolver/
https://jaehun2841.github.io/2018/08/30/2018-08-25-spring-mvc-handle-exception/#handlerexceptionresolver%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EC%B2%98%EB%A6%AC
<br><br>
#### 📚 유익했던 자료
- [How to manage exceptions thrown in filters in Spring?](https://stackoverflow.com/questions/34595605/how-to-manage-exceptions-thrown-in-filters-in-spring)
- [Spring Handle Exception](https://jaehun2841.github.io/2018/08/30/2018-08-25-spring-mvc-handle-exception/#%EC%98%88%EC%99%B8exception-%EC%B2%98%EB%A6%AC%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C)
- [Spring Framework 5.3.13 API. "ControllerAdvice"](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/ControllerAdvice.html)
- 토비의 스프링 3.1
---
<br><br>

## Filter와 Interceptor 차이
### 핵심답변
Filter는 Servlet Filter로써 javax.servlet 스펙에 포함되는 클래스입니다.       
Interceptor는 Spring MVC 스펙에 포함되어 있는 클래스입니다.
<br><br>
#### 🤔 Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?
Filter는 DispatcherServlet 외부에 존재하기 때문에 예외가 발생했을 때 ErrorController에서 처리해야 합니다.                       
하지만 Interceptor는 DispatcherServlet 내부에 존재하기 때문에 @ControllerAdvice를 적용해서 처리할 수 있습니다.

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료
- [Exception Handling](https://terasolunaorg.github.io/guideline/5.3.0.RELEASE/en/ArchitectureInDetail/WebApplicationDetail/ExceptionHandling.html#exception-handling-basic-flow-label)

---
<br><br>

## DTO를 사용하는 이유
### 핵심답변

데이터를 주고 받을 때, DTO를 사용하는 이유는 다음과 같습니다.
1. 첫번째는 비즈니스 로직의 캡슐화 입니다.          
기존 클래스를 사용하지 않고 데이터를 DTO를 사용하여, 비즈니스 로직의 캡슐화를 할 수 있습니다.<br>
기존 클래스를 통해 데이터를 통신하면, 외부 사용자에게 데이터베이스의 스키마 형태, 데이터베이스의 구조, 서비스 내부 로직을 유출 될 수 있습니다.<br>
대표적인 예로, JPA를 사용할 때, 모델은 데이터베이스의 테이블 구조와 매우 유사합니다.<br>
이때, DTO는 변수의 접근자를 private로 설정하고 public한 getter함수, setter함수를 만들어 캡슐화 할 수 있습니다.

2. 두번째는 클라이언언트에게 필요한 정보를 Model이 전부 담을 수 없을 때 사용합니다.    
가장 대표적으로 에러 메세지가 있습니다.<br>
서비스 실행 도중 사용자 측에 에러가 발생하면, 에러 메세지를 담아 전송해주어야 합니다.<br>
모델은 서비스 로직과 관련이 없기 때문에 모델에 에러메세지를 담기에는 애매합니다. <br>
이런 경우 DTO에 에러 메세지 필드를 선언하고 에러 메세지를 포함시키면 됩니다.
<br><br>
#### 🤔

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료
- [DTO란 무엇인가, VO와의 비교](https://kafcamus.tistory.com/13)
- [Entity, DTO, 그 사이의 ModelMapper 이야기](https://yonguri.tistory.com/m/entry/Entity-DTO-%EA%B7%B8-%EC%82%AC%EC%9D%B4%EC%9D%98-ModelMapper-%EC%9D%B4%EC%95%BC%EA%B8%B0)

---
<br><br>

## JPA를 사용할 때의 이점에 대해서 설명해주세요.
### 핵심답변
JPA가 있다면, 자바 언어로 구현하다가, 갑자기 SQL로 구현해주지 않아도 됩니다.      
JPA를 통해 SQL을 자바로 만들 수 있고, 그 결과 유지보수가 쉽습니다.      

JPA를 사용하지 않았을 때는 필드 변경 시, 모든 SQL을 수정해야 했습니다.      
JPA를 사용했을 때는 필드가 변경 시, 필드만 변경해주면 됩니다. SQL은 JPA가 처리하기 때문에 손댈 것이 없습니다.
<br><br>
#### 🤔

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료


---
<br><br>

## JPA에서 N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.
### 핵심답변
JPA에서 발생하는 케이스들은 2가지 입니다. 즉시로딩 N+1과 지연로딩 N+1입니다.      
N + 1 문제의 원인은 다음과 같습니다.   
즉시 로딩의 경우,
지연 로딩의 경우,

해결방법은 다음과 같습니다.
###### 1. Join Fetch
첫번째 방법은 Join Fetch를 사용하는 것입니다.
###### 2. @EntityGraph
두번째 방법은 EntityGraph 어노테이션을 사용하는 것입니다.

<br><br>
#### 🤔 설명해주신 해결 방법의 한계점은 무엇이 있을까요?

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료
- [JPA N+1 발생원인과 해결방법](https://cheese10yun.github.io/jpa-nplus-1/)

---
<br><br>

## 
### 핵심답변

<br><br>
#### 🤔

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료


---
<br><br>

## 
### 핵심답변

<br><br>
#### 🤔

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료


---
<br><br>

## 
### 핵심답변

<br><br>
#### 🤔

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료


---
<br><br>

## 
### 핵심답변

<br><br>
#### 🤔

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료


---
<br><br>

## 
### 핵심답변

<br><br>
#### 🤔

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료


---
<br><br>

## 
### 핵심답변

<br><br>
#### 🤔

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료


---
<br><br>

## 
### 핵심답변

<br><br>
#### 🤔

<br><br>
#### 🤔

<br><br>
#### 📚 유익했던 자료


---
<br><br>
