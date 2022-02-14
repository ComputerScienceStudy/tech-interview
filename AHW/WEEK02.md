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

- 프론트 컨트롤러 패턴이란 무엇인가요?
- Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.
- POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?
- spring IoC/DI의 동작원리
  - Spring DI/IoC는 어떻게 동작하나요?
  - IoC 컨테이너의 역할은 무엇이 있을까요?
- Spring IoC/DI(의존성 주입)의 방법에 대해 아는대로 설명해주세요.
  - 각 DI 주입 방식의 차이점과 이점에 대해서 설명해주세요.
  - 의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.
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
