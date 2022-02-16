# Spring Framework
## 목차
### Spring
- POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?
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

#### 핵심답변

POJO란, Plain Old Java Object의 약자로, 다른 클래스나 인터페이스를 상속받지 않은, 기본적인 기능만 가진 자바 객체를 말합니다.           
즉, POJO는 객체지향적 원리에 충실하고, 특정 규약과 환경에 종속되지 않게 재활용 될 수 있게 설계된 객체를 말합니다.                                   
POJO를 사용할때의 이점은, 종속된 코드를 분리함으로 코드의 간결해집니다.               
또한, 자동화 테스트의 유리하고 유지보수성을 높일 수 있습니다.
<br><br>

#### 🤔 Spring Framework에서 POJO는 무엇이 될 수 있을까요?
Spring은 가장 대표적인 POJO프레임워크이며, POJO란 객체지향적인 원리에 충실한 방식으로 설계된 자바 객체입니다.                
Spring에서는 도메인과 비즈니스 로직을 수행하는 대상이 POJO가 될 수 있습니다.
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
annotation으로 메세지 수신을 선언하고 method parameter를 통해 수신 받은 데이터를 OrderPlaced 객체로 다루겠다고 작성 후 바로 비즈니스 로직을 처리합니다.             
이렇듯 특정 기술과 환경에 종속되지 않는 객체는 깔끔한 코드가 될 수 있습니다.

첫번째 코드와 같이 기술과 환경에 종속적인 객체가 비즈니스 로직과 함께 섞여 있으면 지저분한 코드가 발생합니다.          
읽고 이해하기도 어려울 뿐더러 검증이나 테스트 작성에도 어려움이 있으므로 유지 보수에 큰 부담이 됩니다.          

스프링은 엔터프라이즈 애플리케이션 개발의 모든 영역과 계층에서 POJO 방식의 구현이 가능하도록 만들어졌습니다.                  
이를 이용하면 POJO 프로그래밍의 장점을 그대로 살려 엔터프라이즈 애플리케이션의 핵심 로직을 객체 지향적인 POJO 기반으로 깔끔하게 구현하고            
동시에 엔터프라이즈 환경에 각종 서비스와 기술적인 필요를 POJO 방식으로 만들어진 코드에 적용할 수 있습니다.

---

<br><br>

### Spring DI/IoC는 어떻게 동작하나요?

---

#### 핵심답변

IoC(제어의 역전)은 main() 메서드가 다음 사용 객체를 결정, 생성, 호출해 나가는 일반적인 프로그램 흐름과 달리 외부에서 제어 흐름을 관리하는 것입니다.                  
스프링에서는  IoC 컨테이너를 제공하여 런타임 시점에 객체간의 의존 관계를 결정하고, 객체 레퍼런스도 제공해 줍니다.          

DI는 클래스 간 직접적인 의존 관계 형성시 발생하는 높은 결합도(coupling)문제를 해결하기 위해           
interface의 활용을 통해 외부에서 생성된 객체를 주입 후 setter나 생성자를 통해 사용합니다.              
이렇게 하면 결합도를 낮추어 코드의 재활용성을 높이고 사용자 요구에 대해 유연하게 대처할 수 있습니다.

---

<br><br>

### IoC 컨테이너의 역할은 무엇이 있을까요?

---

#### 핵심답변

컨테이너는 객체의 생명 주기를 관리하고, 생성된 인스턴스들에게 추가적인 기능을 제공하는 역할을 합니다.           
스프링에서는 IoC 컨테이너가 객체의 생성과 의존성 관리를 하고, POJO의 생성, 초기화, 서비스, 소멸에 대한 권한을 가지고 있습니다.               
따라서 개발자는 핵심 비즈니스 로직에 집중하여 개발 할 수 있습니다.

---

<br><br>

### Spring IoC/DI(의존성 주입)의 방법에 대해 아는대로 설명해주세요.

---

#### 핵심답변

- 생성자(Constructor Injection) 주입
- 필드(Field Injection) 주입
- 수정자(Setter Injection) 주입

---

<br><br>

### 각 DI 주입 방식의 차이점과 이점에 대해서 설명해주세요.

---

#### 핵심답변

수정자 주입(Setter Injection)은 Setter 메서드를 사용해 의존성 주입을 하기 때문에, 런타임시 의존관계를 주입해 낮은 결합도를 갖는다는 장점이 있지만, Setter 메서드를 사용하기 때문에, 의존성을 주입해주지 않는 경우에도 객체가 생성되어 NullPointException이 발생한다는 문제가 있습니다.

필드 주입(Field Injection)은 변수 선언부에 @Autowired 어노테이션을 사용합니다. 어노테이션을 사용하여 자동으로 의존성이 주입되기 때문에 간편하지만, 참조 관계를 눈으로 확인하기 어렵고 수정자 주입과 마찬가지로 런타임시 의존관계를 주입해 NullPointerException이 발생할 수 있다는 문제가 있습니다.

생성자 주입(Constructor Injection)은 선언된 생성자를 이용해 의존성을 주입하는 방법입니다. 수정자 주입과 필드 주입과는 다르게 의존관계를 주입하지 않는 경우에 객체를 생성할 수가 없습니다. 이러한 특징 덕분에 애플리케이션 구동시에 해당 오류를 잡아낼 수 있습니다.

---

<br><br>

### 의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.

---

#### 핵심답변

필드 주입과 수정자 주입의 경우 빈이 생성된 후에 참조를 하기 때문에 애플리케이션이 런타임 시까지 오류나 경고 없이 구동되지만, 생성자 주입의 경우 애플리케이션 구동 시에 순환 참조에 대한 예외처리를 받을 수 있어 서버 구동에 있어 크리티컬한 문제를 방지할 수 있기 때문에 생성자 주입을 사용합니다.

이러한 문제로 스프링 레퍼런스에서도 생성자 주입을 권장하고 있습니다.
<br><br>

#### 🤔 순환 참조가 뭐죠?

Bean A → Bean B → Bean A 처럼, 빈들이 서로 계속 연결되어 있는 상태를 의미합니다.           
순환 참조가 발생하면 컨테이너는 어느 빈을 먼저 생성해야하는지 판단하지 못하고 에러를 발생시킵니다.

---

<br><br>

### MVC 패턴이란?

---

#### 핵심답변

애플리케이션을 3가지 역할로 구분한 개발 방법론입니다.

1. `Model`: 비즈니스 로직 수행 및 데이터베이스 관리
2. `View`: Model이 처리한 데이터의 시각화 = 사용자에게 보여주는 화면
3. `Controller`: Model과 View의 사이 연결 및 데이터 흐름 제어
<br><br>

#### 🤔 MVC 패턴을 사용하는 이유는 무엇일까요?

역할을 3가지(사용자가 보는 페이지, 데이터 처리, 이를 중간에서 제어하는 컨트롤러)로 구분하여 담당함으로써 생기는 이점이 많습니다.

1. 코드 수정이 용이합니다.
   - 유지보수 또는 확장성 보장
2. 결합도를 높일 수 있습니다.
    1. 관련 있는 기능을 하나의 Controller로 묶거나, 특정 Model과 관련 있는 View 그룹화가 가능
    2. 단, 하나의 Controller에 다수의 Model과 View가 연결되어 있는 상황이 생길 수 있어, 서로의 의존성 문제 발생 가능
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
    - Model의 상태에 변화가 있을 때 컨트롤러와 View에 이를 통보할 수도 있고, 반대로 Controller와 View가 직접 Model의 상태를 읽어오기도 한다.
    - Model은 사용자에게 어떻게 보일지 신경 쓰지 않아도 되고, 순수하게 public 함수로만 이루어져 있다. (POJO)
- 구성 요소
    - Service : DB 트랜잭션 처리와 도메인에게 비즈니스 로직 처리를 위임
    - 도메인 객체 : 비즈니스 로직을 수행
    - DAO(or Repository) : DB CRUD
    - DTO : Layer간 통신용

###### Controller

- Controller란?
    - 사용자 입력을 받아 Model 객체의 데이터를 변경하거나, Model 객체를 View에 전달하는 역할
    - 클라이언트의 요청을 받았을 때 그 요청에 대해 실제 업무를 수행하는 Model 컴포넌트 호출
    - 클라이언트가 보낸 데이터가 있다면, Model 호출 시 전달하기 쉽게 데이터를 적절히 가공
    - Model이 업무 수행을 완료하면, 그 결과를 가지고 화면을 생성하도록 View에 전달한다.
- 책임
    - 입력값 검증
    - 입력 받은 데이터로 Model 객체 변경
    - 변경된 Model 객체를 View에 전달
    - Service Layer에 비즈니스 로직 처리 요청
      → Service는 도메인 객체를 통해 비즈니스 로직 처리 후 결과 반환

###### View

- View란?
    - 데이터를 보여주는 역할
    - 다양한 형태로 보여줄 수 있다.
- 예시
    - HTML, JSON, XML, JSP, Thymleaf 등

---

<br><br>

### 프론트 컨트롤러 패턴이란 무엇인가요?

---

#### 핵심답변

Front Controller 패턴이란 프론트 컨트롤러 하나가 서블릿 컨테이너의 제일 앞에서 서버로 들어오는 클라이언트의 모든 요청을 받아 처리하도록 디자인한 패턴입니다.     
<br><br>

#### 🤔 스프링 MVC 프레임워크는 프론트 컨트롤러 패턴을 어떻게 사용할까?

- 구조 비교
    1. **기존 패턴**
    - 각 클라이언트들은 Controller A, B, C에 대해 각각 호출한다.
    - 공통 코드들은 별도로 처리되어 있지 않고 각 Controller에 포함되어 있다.
    - 단점:
        - 요청을 수행할 때마다 매번 스레드를 생성해야 하므로, 멀티 스레딩을 다뤄야 한다는 어려움이 있다. (관리의 측면)
        - 핸들러의 공통 로직이 매번 중복된다. (개발의 측면)

  ![https://user-images.githubusercontent.com/90819869/153976572-3eb68212-1225-4e1b-b430-ab4b2e1e03b5.png](https://user-images.githubusercontent.com/90819869/153976572-3eb68212-1225-4e1b-b430-ab4b2e1e03b5.png)

  2. **Front Controller(대표 컨트롤러) 패턴**
    - 클라이언트로부터 요청이 들어올 경우, Front Controller가 각 요청에 맞는 컨트롤러를 찾아서 호출한다.
    - 공통 코드에 대해서는 Front Controller에서 처리하고, 서로 다른 코드들만 각 Controller에서 처리할 수 있도록 한다.
    - View에서 들어오는 모든 요청을 담당하여 웹 애플리케이션을 실행하는 모든 요청을 일괄적으로 처리할 수 있다.

      ![https://user-images.githubusercontent.com/90819869/153976771-7c6dad1f-480b-4883-82a0-d411f654f785.png](https://user-images.githubusercontent.com/90819869/153976771-7c6dad1f-480b-4883-82a0-d411f654f785.png)

    - 장점
        - 공통된 부분을 처리해주는 FrontController로 중복을 줄일 수 있다.
        - Front Controller 외에 다른 Controller에서 Servlet을 사용하지 않아도 된다.

<br>

#### 🤔 Spring Web MVC에서 요청마다 Thread가 생성되어 Controller를 통해 요청을 수행할텐데, 어떻게 1개의 Controller만 생성될 수 있을까요?

Controller 객체 하나를 생성하면 객체 자체는 Heap에 생성되지만, 해당 Class의 정보는 메소드 영역에 저장됩니다.         
모든 Thread는 객체의 Binary Code 정보를 공유할 수 있습니다.              
공유되는 정보를 사용하기 위하여 굳이 Controller 객체를 사용하고 있는 쓰레드나 Controller 객체 자체가 Block될 필요가 없습니다.                 
왜냐하면, 객체 내부적으로 상태를 갖는 것이 없으니, 내부의 상태를 변경할 일이 없고 그저 메소드에 대한 정보만 ‘같이 공유해서’ 쓰면 되기 때문입니다.               
Controller가 내부적으로 상태를 갖는 것이 없으니 메소드 호출만 하면 되기 때문에 굳이 동기화할 이유가 없고, 그저 처리 로직만 ‘공유되어’ 사용되는 것이기 때문에 몇 십만개의 요청이 들어오든 상관없습니다.         

---

<br><br>

### Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.

---

#### 핵심답변
Dispatcher Servlet은 모든 요청을 처리하는 프론트 컨트롤러입니다.        
Spring Web MVC의 Dispatcher Servlet의 동작 원리는 다음과 같습니다.

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
컨트롤러가 실행되기 전에 인터셉터를 실행할 수 있음으로 주로 특정 요청에 대한 공통 로직 적용이 필요한 경우에 유용합니다.
<br><br>
#### 🤔 DispatcherServlet 구성 요소
DispatcherServlet은 요청에 대응할 수 있는 Controller, ViewResolver, HandlerMapping과 같은 스프링 빈을 구성합니다.

* DispatcherSerlvet의 기본 전략
    * DispachersServlet.propertes 설정을 따라간다.
* MutilpartResolver
    * 파일 업로드 요청 처리에 필요한 인터페이스
    * HttpServletRequest를 MutilpartHttpServletRequest로 변환해주어 요청이 담고 있는 field을 꺼낼수 있는 API 제공한다.
* LocaleResolver
    * 클라이언트의 위치 정보를 파악하는 인터페이스
    * 기본 전략은 요청 accept-language를 보고 판단한다.
* HanderMapping
    * 요청을 처리할 핸들러를 찾는 인터페이스
* HandlerAdapter
    * HandlerMapping이 찾아낸 핸들러를 처리하는 인터페이스
    * 스프링 MVC 확장력의 핵심 <br>(여기서, controller를 호출하는데, controller가 실행되기 전 Interceptor를 실행해서 특정 요청에 대한 공통 로직 적용할 수 있기 때문이다.)
* ViewResolver
    * 뷰 이름에 해당하는 뷰를 찾아내는 인터페이스
* FlashMapManager
    * FlashMap 인스턴스를 가져오고 저장하는 인터페이스
    * FlashMap은 주로 리다이렉션을 사용할 때 요청 매개변수를 사용하지 않고 데이터를 전달하고 정리할 때 사용한다.
      <br><br>
---

<br><br>

### AOP(Aspect Oriented Programming) 

---

#### 🤔 AOP(Aspect Oriented Programming)란 무엇일까요?
AOP란 Aspect Oriented Programming, 관점 지향 프로그래밍을 의미합니다.   
관점지향이란, 어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 각각 모듈화하는 프로그래밍 기법을 의미합니다.   
따라서 AOP는 핵심기능과 부가기능을 나누어서 설계, 구현하는 것을 의미합니다.

<img src="https://user-images.githubusercontent.com/42319300/153905949-7ab73ff7-59a3-4445-a994-5cd39f439a61.png" width="60%" height="60%">
<br>

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

<br>

#### 🤔 AOP의 특징에 대해서 설명부탁드립니다.

- 프록시 패턴 기반이기 때문에, 접근 제어가 가능합니다.
- 프록시가 호출을 인터셉터해서 핵심 로직 전과 후에 부가기능을 수행할 수 있습니다.
- 핵심 기능의 메소드가 호출되는 런타임 시점에만 부가 기능을 적용할 수 있습니다.
<br><br>

#### 🤔 프록시 패턴이란?

어떤 객체에 대한 접근을 제어하거나 부가기능을 추가하는 용도로 실제 객체를 대신하는 객체를 제공하는 패턴입니다.
<br><br>

#### 🤔 프록시 패턴 동작 원리에 대해서 설명해주세요.

클라이언트가 인터페이스 타입으로 프록시 객체를 사용하게 되고, 프록시는 핵심 기능을 갖는 실제 객체를 감싸서 클라이언트의 요청을 처리하게 됩니다. 이런 특징 덕분에 프록시 패턴은 접근을 제어할 수 있고 부가 기능을 추가할 수 있게 됩니다.
<br><br>

#### 🤔 AOP의 주요 개념들에 대해 설명해주세요
- Aspect : 흩어진 관심사를 모듈화 한 것입니다. 주로 부가기능을 모듈화함을 의미합니다.
- Target : Aspect를 적용하는 곳울 의미합니다. Target은 주로 클래스, 메서드 등이 됩니다.
- Advice : 실질적으로 어떤 일을 해야할 지에 대한 것을 의미하빈다.Advice는 실질적인 부가기능을 담은 구현체입니다.
- JoinPoint : Advice가 적용될 위치, 끼어들 수 있는 지점, 메서드 진입 지점, 생성자 호출 시점, 필드에서 값을 꺼내올 때의 시점을 말합니다. 앱을 실행할 때 특정 작업이 시작되는 시점입니다.
- PointCut : JoinPoint가 적용되는 대상, Adivice가 실행될 지점을 설정합니다.

---
<br><br>


### Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요. 

---

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
<br><br>

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

<br>

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

---

<br><br>

### Bean에 대해 설명해보세요.

---

#### 핵심답변

Java Bean은 데이터 표현을 목적으로 Java로 작성된 클래스입니다.       
private으로 필드를 선언하고 전달 인자가 없는 기본 생성자를 갖습니다.
getter와 setter로만 접근할 수 있는 클래스의 멤버 변수인 Properties가 있습니다.
<br><br>

#### 🤔 Spring Bean이란 무엇인가요?          
Spring IoC 컨테이너가 인스턴스화, 관리, 생성하는 자바 객체이며
ApplicationContext가 만들어서 그 안에 담고 있는 객체입니다.

따라서 기존 자바 프로그래밍처럼 Class 생성 후 new 연산자로 객체를 생성하는 것이 아니라           
ApplicationContect.getBean()와 같은 메서드를 사용해 스프링으로부터 객체를 얻습니다.
<br><br>

#### 🤔 스프링 Bean의 생성 과정을 설명해주세요.          
객체 생성 → 의존 설정 → 초기화 → 사용 → 소멸 순서로 라이프 사이클을 지닙니다.            
1.스프링 컨테이너가 초기화 될 때 먼저 Bean 객체를 설정 정보에 맞춰 탐색, 생성합니다.            
2.Bean으로 등록할 객체를 초기화 하고 의존 관계를 주입합니다.               
3.해당 프로세스가 완료되면  Bean 객체가 지정한 메서드를 호출해서 초기화 합니다.        
4.객체를 사용한 뒤 컨테이너가 종료될 때 Bean이 지정한 메서드(destroy method)를 호출해 소멸합니다.
<br><br>

#### 🤔 스프링 Bean의 Scope에 대해서 설명해주세요.
Scope란 Bean이 존재하고 관리되는 범위를 의미합니다. 일반적으로 Sington Scope로 관리하게 되는데,
Singleton은 스프링 컨테이너의 시작과 종료까지 가장 넓은 범위로 한 객체가 유지됩니다.
애플리케이션 구동 시 JVM 안에서 Spring이  Bean마다 하나의 객체를 생성하므로 개발자들은 Spring을
통해 Bean을 제공받으면 언제나 주입받은 Bean은 동일한 객체라는 가정하에서 출발합니다.         

반면, ProtoType Scope는 Bean의 생성과 의존 설정까지만 관여하는 매우 짧은 스코프입니다.          
따라서 모든 요청에서 새로운 객체를 생성하게 됩니다.           

1.`singleton` : 스프링 컨테이너의 시작과 종료까지 단 하나의 객체만 사용하는 방식

![https://user-images.githubusercontent.com/90819869/154178392-70e96c18-6a96-4b26-9ec9-8430aa7f491b.png](https://user-images.githubusercontent.com/90819869/154178392-70e96c18-6a96-4b26-9ec9-8430aa7f491b.png)

2. `prototype` : 모든 요청에서 새로운 객체를 생성하는 방식

![https://user-images.githubusercontent.com/90819869/154178422-3304cff2-d566-482f-b191-68c10613fc3f.png](https://user-images.githubusercontent.com/90819869/154178422-3304cff2-d566-482f-b191-68c10613fc3f.png)
<br><br>

#### 🤔 Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.

1. @Bean

   개발자가 직접 제어가 불가능한 외부 라이브러리를 이용할 때 사용합니다.

   @Configuration을 선언한 클래스 내부에서 사용하는데,

   이는 개발자가 작성한 메서드를 통해 반환되는 객체를 Bean으로 만들기 때문입니다.

    ```java
    // 개발자가 직접 제어가 불가능한 외부 라이브러리를 사용할 경우
    @Configuration
    public class ExampleConfig {
    
        @Bean
        public ArrayList<String> array(){
          return new ArrayList<String>();
        }
    }
    ```

    ```java
    // 개발자가 만들어준 클래스를 import해 사용한 경우
    @Configuration
    public class ExampleConfig {
    
      @Bean(name="mybean")
       public Product aaa(){
              Battery p1 = new Battery("AAA", 2.5);
                      p1.setRechargeable(true);
                      return p1;
      }
    ```

2. @Component

   개발자가 직접 작성해 컨트롤 할 수 있는 Class를 Bean으로 등록할 때 사용합니다.

    ```java
    @Component(value="mybean")
    public class Example {
      puiblic Example(){
          System.out.println("Hello world");
        }
    }
    ```


---

<br><br>

### Getter와 Setter를 사용해야하는 이유에 대해서 설명해주세요. 

---

#### 핵심답변

- 객체의 무결성을 보장하기 위해 사용합니다.
    - 예를 들어, 만약 외부에서 몸무게라는 필드에 직접 접근한다면 0보다 낮은 값을 줄 수도 있습니다. 이 경우 객체의 무결성이 깨지기 때문에 이를 방지하기 위해 Getter/Setter를 사용하여 데이터의 무결성을 지켜줍니다.
<br><br>
  
#### 🤔 무결성이란 무엇인가요?

데이터의 정확성과 일관성을 유지하고 보증하는 것을 말합니다.
<br><br>

#### 🤔 Getter/Setter를 사용할 때 왜 데이터 무결성이 지켜지나요?

Getter, Setter를 이용해서 데이터를 생성 및 접근을 하게 되면 들어오는 값을 바로 저장하는 게 아닌,      
한번 검증하고 처리할 수 있도록 할 수 있기 때문에 데이터의 무결성이 지켜집니다.

- `Getter` : 본 필드의 값을 숨긴 채 내부에서 가공된 값을 꺼낼 수 있다.
- `Setter` : 필드를 private로 만들어 외부의 접근을 제한한 후, Setter를 사용해 전달받은 값을 내부에서 가공해 필드에 넣어줄 수 있다.
<br><br>

#### 🤔 Getter/Setter를 사용할 때의 다른 이점은 없나요?

1. Getter, Setter와 같은 엑세스 함수 사용 시, 위와 같은 데이터 무결성과 유효성 검사가 가능합니다.
2. 객체의 필드를 `private`과 같은 접근제한자를 두면서 객체지향의 목적인 정보은닉이 가능합니다.

---

<br><br>

### DTO를 사용하는 이유?

---

#### 핵심답변

- 데이터를 모아서 전달할 수 있어 통신 횟수를 감소시키고, 검증과 로직 처리를 효율적으로 할 수 있습니다.
    - 외부와 통신하는 프로그램에게 있어 호출은 큰 비용이며, 이를 줄이고 더욱 효율적으로 값을 전달하기 위해 데이터를 모아 한 번에 전달하는 방법이 고안되었는데, 이 때 이 클래스를 DTO라고 합니다.
- 데이터를 묶어 보내기 때문에 안정성이 높고, 수행시간은 감소시킬 수 있습니다.
<br><br>

#### 💡 보충지식
  DTO를 사용하는 이유는 자바 Domain 객체(데이터)에 직접적으로 접근하지 않음으로써, 아래와 같은 편리함이 있기 때문입니다.          

  ① 데이터를 은닉 및 보호할 수 있습니다.               
  ② DTO를 사용하여 간결하게 원하는 정보만을 제공해줄 수 있습니다.            
  ③ Entity의 정보뿐만 아니라, 개발자가 원하는 형식의 데이터들을 추가하여 정보를 주고받을 수 있습니다.
<br><br>

#### 🤔 DAO와 DTO의 차이를 설명해주세요.

- `DTO(Data Transfer Object, 데이터 전송 객체)`는 데이터 교환을 위해 사용하는 객체로, DB의 데이터를 Controller 혹은 Service로 보낼 때 사용합니다.
- `DAO(Data Access Object, 데이터 접근 객체)`는 실제로 데이터에 접근하는 객체로, DB에 접근하는 로직과 비즈니스 로직을 분리하기 위한 객체로 사용됩니다.

---

<br><br>

### Spring에서 예외처리하는 방법에 대해서 설명해주세요.

---

#### 핵심답변

스프링에서 예외를 처리하는 방법은 크게 3가지가 있습니다.            

정확히는 DispatcherServlet에서 발생하는 예외를 HandlerExceptionResolver가 처리하는 방법들입니다.        

1. 메소드 단에서, try/catch문 사용할 수 있습니다. 주로 Check Exception을 처리해야하는 경우에 사용합니다.
2. 컨트롤러단에서 @ExceptionHandler 사용할 수 있습니다. 주로 Controller의 메서드에서 throw된 Exception에 대해 공통적인 처리를 할 수 있게합니다.
3. 커스텀한 Exception 클래스를 만들어 Global Level에서, 컨트롤러 이후 Client에게 전달되기 전에 처리하는 AOP 방식이 있습니다.
<br><br>

#### 🤔 ExceptionHandler는 무엇인가요?

스프링에서 @ExceptionHandler 어노테이션을 사용하여 특정 예외 클래스를 지정해주면, 해당 예외가 발생했을 때 메서드에서 정의한 로직을 처리할 수 있습니다.

AOP 관점에서 @RestControllerAdvice 어노테이션을 클래스에 선언하게 되면, 컨트롤러 단에서 일어나는 모든 에러에 대해 전역적인 처리가 가능합니다.

ExceptionHandler를 사용하면 전역적으로 일어나는 에러 중 특정 에러 클래스에 지정하여 로직을 처리할 수 있습니다.
<br><br>

#### 🤔 Controller의 @ExceptionHandler와 ControllerAdvice의 @ExceptionHandler 중 우선순위게 높은것은 무엇인가요?

Controller의 @ExceptionHandler가 먼저입니다.
<br><br>

#### 🤔 Filter에서 발생하는 예외처리는 어떻게 해결하나요?

DisptatcherServlet 밖에서 발생하는 예외로 HandlerExceptionResolver의 처리를 받을 수 없습니다. 이러한 예외 처리는 Web Application 레벨에서 처리를 해줘야 합니다.

1. web.xml에 error-page를 잘 등록해줘서 에러를 사용자에게 응답하는 방법이 있습니다.
2. Filter 내부에서 예외를 처리하기 위한 필터를 따로 둬서 try-catch문을 사용하여 처리합니다.
3. Filter 내부에서 try-catch 구문을 통해 예외 발생 시, HandlerExceptionResolver를 빈으로 주입받아 @ExceptionHandler에서 처리하는 방법이 있습니다. 
   <br>즉, 필터에서 발생하는 예외를 디스패처 서블릿의 예외 처리인 HandlerExceptionResolver에 보내서 처리하는 방법이 있습니다.

---

<br><br>

### Filter와 Interceptor 차이 

---

#### 핵심답변
필터는 Servlet Filter로써 javax.servlet 스펙에 포함되는 클래스입니다.              
인터셉터는 Spring MVC 스펙에 포함되어 있는 클래스입니다.

<img width="500" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSz6DV%2Fbtq9zjRpUGv%2F68Fw4fZtDwaNCZiCFx57oK%2Fimg.png">

필터는 Dispatcher Servlet에 요청이 전달되기 전과 후에 url 패턴에 맞는 모든 요청에 대해 부가작업을 처리할 수 있는 기능을 제공해줍니다.          
반면 인터셉터는 Spring이 제공하는 기술로써, Dispatcher Servlet이 컨트롤러를 호출하기 전, 후로 끼어들기 때문에 스프링의 영역 내부에서 Controller(Handler)에 관한 요청과 응답에 대해 처리해줍니다.
<br><br>

#### 🤔 Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. <br>Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?
Interceptor는 DispatcherServlet 내부에 존재하기 때문에 HandlerExceptionResolver를 사용해서 예외를 처리할 수가 있습니다.

하지만, Filter는 DispatcherServlet 외부에 존재하기 때문에 예외가 발생했을 때 Web Application 레벨에서 처리해주어야 합니다.       
대표적인 방법으로는 Filter 내부에서 예외를 처리하기 위한 필터를 따로 둬서 try-catch문을 사용하여 처리하는 방식을 둘 수가 있습니다.
또한, HandlerExceptionResolver를 빈으로 주입받아 @ExceptionHandler에서 처리하는 방법이 있습니다.
<br><br>

#### 🤔 Filter와 Interceptor는 어떤 경우에 사용될 수 있을까요?
Filter와 Interceptor는 공통 업무를 프로그램 흐름의 앞, 중간, 뒤에 추가하여 자동으로 처리할 때 사용합니다.

자바 웹 개발을 하다보면, 공통적으로 처리해야 할 업무들이 많습니다.                
예를 들어 로그인 관련(세션 체크)처리, 권한 체크, XSS(Cross site script)방어, 페이지 인코딩 변환 등이 있습니다.         
공통업무에 관련된 코드를 모든 페이지 마다 작성 해야한다면 중복된 코드가 많아지게 되고 프로젝트 단위가 커질수록 서버에 부하를 줄 수도있으며, 소스 관리도 되지 않습니다.

즉, 공통 부분은 빼서 따로 관리하는게 좋습니다.     
이러한 공통업무를 프로그램 흐름의 앞, 중간, 뒤에 추가하여, 자동으로 처리하기 위해, Filter와 Interceptor를 활용할 수 있습니다.

- Filter는 전체적인 Request단에서 어떤 처리가 필요할 때 사용할 수 있습니다.
    - 인증, 이미지 변환, 데이터 압축, 암호화 필터, XML 컨텐츠를 변형하는 XSLT 필터, URL 및 기타정보를 캐시하는 필터, 문자 인코딩
- Interceptor는 세션 및 쿠키 체크와 같이 http 프로토콜 단위로 처리해야 하는 업무가 있을 때 사용할 수 있습니다.
---

<br><br>

### JPA란 무엇인가요? 

---

#### 핵심답변

JPA란 Java Persistance API의 약자로 JAVA ORM 표준 기술입니다.자바에서 데이터를 DBMS에 영구히 기록할 수 있는 환경을 제공하는 API입니다.
<br><br>

#### 🤔 ORM이란 무엇인가요

객체와 관계형 데이터베이스를 매핑해주는 것으로 쿼리문 작성 없이 객체를 데이터베이스에 직접 저장할 수 있게 도와주는 기술입니다.
<br><br>

#### 🤔 JPA를 사용할 때의 이점에 대해서 설명해주세요.

JPA는 ORM기술이기 때문에 RDBMS에 연결하여 데이터를 직접 조작할 필요없이, 자바코드로 표현하여 객체 중심으로 개발할 수 있다는 장점이 있습니다. 그로인해 JPA에 익숙하다면 생산성이 높아진다는 장점을 가지고 있습니다.

정리하자면, 생산성, 유지보수성, DB접근 최소화로인한 성능 최적화(영속성 컨텍스트), 패러다임 불일치 해결, 데이터 접근 추상화와 벤더 독립성이 있습니다.
<br><br>

#### 🤔 JPA의 단점은 무엇인가요

JPA는 자동으로 쿼리를 생성해주기 때문에, 통계처리와 같은 복잡한 쿼리보다 실시간 쿼리에 최적화 되어있씁니다.따라서, 미세하고 복잡한 쿼리문을 사용해야할 때는 Mybatis와 같은 Mapper방식을 사용하는 것이 더 효율적일 수 있습니다.
<br><br>

#### 🤔 JPA 영속성 컨텍스트의 이점(5가지)를 설명해주세요.

영속성 컨텍스트란, 데이터를 영구히 저장하는 환경을 의미합니다.

영속성 컨텍스트는 논리적인 개념이기때문에 눈에 보이지 않지만, JPA를 이용해서 데이터를 저장한다고 했을때, 영속성 컨텍스트에 저장이되고 이후 DB에 반영됩니다.

이런 어플리케이션과 DB사이 영속성컨텍스트를 두엇을 때의 이점은 1차캐시, 동일성 보장, 트랜젝션을 지원하는 쓰기 지연, 변경감지, 지연로딩 5가지가 있습니다.

1. 1차 캐시
    - 영속성 컨텍스트 내부에서는 1차 캐시가 존재하는 엔티티를 영속성 컨텍스트에 저장하는 순간, 데이터를 1차 캐시에 저장합니다.
    - 1차캐시는 데이터를 조회할 때 이점이 있는데, find()를 했을 당시 1차캐시에 데이터가 존재하면, DB에 접근하지 않고 바로 데이터를 반환합니다.
2. 동일성 보장
    - 영속성 컨텍스트에서 관리되는 엔티티를 가져왔을 경우 동일성을 보장합니다.
3. 트랙잭션을 지원하는 쓰기 지연
    - 엔티티들에대한 데이터 제어가 일어날 때, JPA는 바로 DB에 반영하지 않습니다.
    - 우선적으로 1차캐시에 저장하고, commit()시 쿼리문들을 DB에 보냅니다.
    - flush()는 1차캐시를 지우지 않고, 쿼리를 DB에 날려 DB와 싱크는 맞추는 역할을 하고
    - 쿼리를 보내고난 후 Commit()을 하게 됩니다.
    - 트랜잭션의 커밋은 이 flush()와 commit() 2가지 일을 하게 됩니다.
    -

    ![https://user-images.githubusercontent.com/42319300/154107978-2f0aafeb-ada3-414a-a55d-8211e2ffed17.png](https://user-images.githubusercontent.com/42319300/154107978-2f0aafeb-ada3-414a-a55d-8211e2ffed17.png)

4. 변경 감지 (Dirty checking)
    - JPA로 엔티티를 수정할 때는 update()나 persist()로 영속성컨텍스트에 알려주지 않고 단순히 엔티티를 조회해서 데이터를 변경하면 됩니다.
    - 변경 감지를 더티 체킹이라 하는데 데이터가 1차캐시에 저장될 때 동시에 스냅샷 필드도 저장이 됩니다.
    - commit()또는 flush()가 일어날 때, 변경된 엔티티의 내용과, 1차캐시에 저장된 스냅샷을 비교해서, 변경사항이 있으면 Update SQL을 만들어 반영합니다.
    - 변경감지의 흐름
        1. 트랙잭션을 커밋하면 엔티티 매니저 내부에서 먼저 플러시가 호출된다.
        2. 엔티티와 스냅샷을 비교하여 변경된 엔티티를 찾는다.
        3. 변경된 엔티티가 있으면 수정 쿼리를 생성해서 쓰기 지연 SQL 저장소에 저장한다.
        4. 쓰기 지연 저장소의 SQL을 플러시한다.
        5. 데이터베이스 트랜잭션을 커밋한다.

   ![https://user-images.githubusercontent.com/42319300/154106921-f2c2923a-ecce-465f-a1b1-135731baa245.png](https://user-images.githubusercontent.com/42319300/154106921-f2c2923a-ecce-465f-a1b1-135731baa245.png)

5. 지연 로딩
    - 지연로딩을 사용하면, 엔티티와 연관관계에 있는 데이터를 사용하는 시점에 불러올 수 있습니다.
    - 이 때의 이점은, DB가 객체를 불러올때, 연관관걔의 데이터를 가지고 오지않아 크기를 줄임으로써 부담을 줄이는 장점이 있습니다.
<br><br>
    
#### 🤔 JPA에서 N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.

N+1 문제가 발생하는 이유는, JPA는 JPQL을 생성하여 실행하게 되는데, JPQL은 엔티티 객체와 필드 이름을 갖고 쿼리를 만들기 때문에 객체의 연관관계 매핑에 의해서 관계가 맺어진 다른 객체들이 함께 조회되기 때문에 발생합니다.

즉시로딩의 경우, 모든객체를 불러오기에 당연히 N+1 문제가 발생하고, 지연로딩의 경우에도, 객체를 조회하고, 반복문으로 연관된 관계의 매핑을 조회할때 N+1 문제가 발생합니다.

지연로딩으로 한번 한번의 쿼리문으로 조회되어 불러온 객체가 있지만, 지연로딩의 경우, 연관된 매핑관계에있는 객체의 정보는 불러오지 않기 때문에, 해당 객체의 정보로 조건문을 사용하여 쿼리문을 별도로 생성하여 값을 불러와 데이터의 개수만큼의 N개의 쿼리문이 추가로 발생되어집니다.

```java
@Transactional
@Test
public void test_N1_문제_발생_지연로딩설정_loop으로_조회하는_경우() throws JsonProcessingException {
  savePostWithComments(4, 2);
  List<Post> posts = postRepository.findAll(); //(1) N+1 발생하지 않는다

  List<Comment> commentList;
  for (Post post : posts) {
    commentList = post.getCommentList();
    log.info("post author: {}", commentList.size()); //(2) N+1 발생한다
  }
}
```

```java
Hibernate: select post0_.post_id as post_id1_1_, post0_.create_dt as create_d2_1_, post0_.updated_dt as updated_3_1_, post0_.author as author4_1_, post0_.content as content5_1_, post0_.like_count as like_cou6_1_, post0_.title as title7_1_ from post post0_

Hibernate: select commentlis0_.post_id as post_id6_0_0_, commentlis0_.comment_id as comment_1_0_0_, commentlis0_.comment_id as comment_1_0_1_, commentlis0_.create_dt as create_d2_0_1_, commentlis0_.updated_dt as updated_3_0_1_, commentlis0_.author as author4_0_1_, commentlis0_.content as content5_0_1_, commentlis0_.post_id as post_id6_0_1_ from comment commentlis0_ where commentlis0_.post_id=?

Hibernate: select commentlis0_.post_id as post_id6_0_0_, commentlis0_.comment_id as comment_1_0_0_, commentlis0_.comment_id as comment_1_0_1_, commentlis0_.create_dt as create_d2_0_1_, commentlis0_.updated_dt as updated_3_0_1_, commentlis0_.author as author4_0_1_, commentlis0_.content as content5_0_1_, commentlis0_.post_id as post_id6_0_1_ from comment commentlis0_ where commentlis0_.post_id=?

Hibernate: select commentlis0_.post_id as post_id6_0_0_, commentlis0_.comment_id as comment_1_0_0_, commentlis0_.comment_id as comment_1_0_1_, commentlis0_.create_dt as create_d2_0_1_, commentlis0_.updated_dt as updated_3_0_1_, commentlis0_.author as author4_0_1_, commentlis0_.content as content5_0_1_, commentlis0_.post_id as post_id6_0_1_ from comment commentlis0_ where commentlis0_.post_id=?

Hibernate: select commentlis0_.post_id as post_id6_0_0_, commentlis0_.comment_id as comment_1_0_0_, commentlis0_.comment_id as comment_1_0_1_, commentlis0_.create_dt as create_d2_0_1_, commentlis0_.updated_dt as updated_3_0_1_, commentlis0_.author as author4_0_1_, commentlis0_.content as content5_0_1_, commentlis0_.post_id as post_id6_0_1_ from comment commentlis0_ where commentlis0_.post_id=?
```

Comment 정보를 조회하면, Post에 대한 조회는 이미 끝난 상태라서 JOIN으로 쿼리가 생성이 안 됩니다.

단지 Post에 대한 정보 ID로 조회할 수밖에 없어서 `where comment.postId=?` 형식으로 JPQL 쿼리를 생성합니다.          
이로 인해 매번 조회 쿼리가 생성이 되어 N 번 실행하는 이슈가 발생합니다.
<br><br>

#### 🤔 N+1 해결 방법

지연로딩시, N+1 문제의 해결방법으로는,

패치 조인(fetch join), EntityGraph, Batch Size 지정 + 즉시 로딩 3가지가 있습니다.

1. fetch join
    - JPQL에 fetch join 키워드를 사용해서 join 대상을 함께 조회할 수 있습니다.
    - 지연로딩을 이용해서 객체를 조회 시, 함께불러오길 원하는 연관관계의 객체를 join해서 같이 불러오는 방식 입니다.

    ```java
    @Repository
      public interface PostRepository extends JpaRepository<Post, Long> {
           @Query("select p from Post p left join fetch p.commentList")
           List<Post> findAllWithFetchJoin();
      }
    ```

2. EntityGraph
    - @EntityGraph JPQL에서 fetch join을 하게 되면 하드코딩해야하는 단점이 있습니다. 이를 보완하기 위해 엔티티그래프 어노테이션을 사용할 수 있습니다.

    ```java
    @EntityGraph(attributePaths = {"articles"}, type = EntityGraphType.FETCH)
       @Query("select distinct u from User u left join u.articles")
       List<User> findAllEntityGraph();
    ```

3. Batch Size 지정 + 즉시 로딩
    - JPQL 페치 조인 대신 Batch 크기를 지정하는 방법도 있습니다. @BatchSize 어노테이션에 size를 지정하고 fetch 타입은 즉시로 설정합니다.

    ```java
    @Table(name = "post")
       public class Post extends DateAudit {
       ...(생략)...
    
       @JsonIgnore //JSON 변환시 무한 루프 방지용
       @BatchSize(size = 2) //batch size를 지정한다
       @OneToMany(mappedBy = "post", fetch = FetchType.EAGER) //즉시로딩으로 변경한다
            private List<Comment> commentList = Lists.newArrayList();
      }
    ```
<br><br>

#### 🤔 JPA Paging N+1 문제 해결 방법

- Pagination에서의 문제 발생 distinct를 쓰는 이유는 연관관계에 대해서 fetch join으로 가져온다고 했을 때, 중복된 데이터가 많기 때문에 중복 데이터를 처리하기 위함인데, Paging 처리는 쿼리를 날릴 때 진행되기 때문에 JPA에게 pagination 요청을 하여도 distinct때와 마찬가지로 중복된 데이터가 있을 수 있으니 limit offset을 걸지 않고 인메모리에 다 가져오게 됩니다. 이렇게 되면 paging을 하는 의미가 사라지게 됩니다.
- Paging 해결방법 - ~ToOne ~ToOne 관계에 있는 경우에는 fetch join을 걸어도 Pagination이 원하는대로 제공됩니다.

```java
@EntityGraph(attributePaths = {"user"}, type = EntityGraphType.FETCH)
@Query("select a from Article a left join a.user")
Page<Article> findAllPage(Pageable pageable);
```

- Paging 해결방법 - Batch Size 사용자가 임의로 연관관계에 대해 데이터의 사이즈를 알때 사용할 수 있는 방법으로 지연로딩하는 객체에 대해서 Batch성 loading하는 것입니다. 기존의 지연로딩은 객체를 조회할 때 그때그때 쿼리문을 날려서 N+1이 발생한 반면 객체를 조회하는 시점에 쿼리를 하나만 날리는게 아니라 해당하는 Article에 대해서 쿼리를 batch size개를 날리게 되는 것입니다. 즉, 지연 로딩으로 생길 N+1 문제를 batch size만큼 가져와 미연에 방지하는거라고 볼 수 있습니다.
- Paging 해결방법 - @Fetch(FetchMode.SUBSELECT) BatchSize와 동일한 동작을 하지만, size를 개발자가 임의로 정하는 것이 아닌 스프링에서 자동으로 설정해줍니다. 일반적으로 모든 batchsize를 가져오기 때문에, 성능적인 테스트가 필요합니다.
- MultipleBagFetchException 해결책 - fetch join 두개 이상의 fetch join을 설정할 경우 메모리에 너무 많은 값이 들어와 MultipleBagFetchException을 발생합니다. 이 경우에는 Set자료구조를 사용해 해결할 수 있습니다. 하지만 Pagination에는 사용할 수 없습니다.

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
---
