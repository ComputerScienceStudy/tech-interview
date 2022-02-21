# Tech Interview
## [Java](https://github.com/ComputerScienceStudy/tech-interview/blob/main/KHY/Content/Java.md)
<details>
<summary>목차</summary>

- JVM 동작 과정/원리
- GC(Garbage Collector)의 종류와 동작 과정/원리
- Java 언어 기초
    - 정적 타입 언어와 동적 타입 언어의 차이
    - Java 코드의 컴파일 과정
    - 각 변수 타입이 몇 byte인지, primitive type과 reference type 인지
    - overriding vs overloading 개념과 활용
    - 접근자 종류와 기능
    - final 키워드
    - Generic의 개념
    - ThreadLocal이 무엇이고 언제 활용되는지
    - static이란 무엇인가요?
      - java의 non-static 멤버와 static 멤버의 차이 
      - java의 main 메서드가 static인 이유
    - Wrapper Class란 무엇인가요?
    - Lombok
- 객체지향
    - 객체지향에 대해서 설명해주세요. 
    - SOLID(객체지향 5대원칙)에 대해서 설명해주세요.
- 오류처리
    - Checked Exception과 Unchecked Exception에 대해 설명해주세요. 스프링 트랜잭션 추상화에서 rollback 대상은 무엇일까요?
    - 자바의 동시성 이슈(공유자원 접근)에 대해 설명해주세요. 
    - 자바에서 null을 안전하게 다루는 방법에 대해 설명해주세요.
</details>
    
## [Spring Framework](https://github.com/ComputerScienceStudy/tech-interview/blob/main/KHY/Content/Spring.md)
<details>
<summary>목차</summary>

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
</details>


## [Database, Web, Network](https://github.com/ComputerScienceStudy/tech-interview/blob/main/KHY/Content/DB%20Web%20Network.md)
<details>
<summary>목차</summary>

### Database
- SQL
- RDBMS와 NoSQL
    - RDBMS
        - 2차원의 행과 열로 데이터의 관계를 관리하는 데이터베이스 
        - 장점: 스키마에 맞추어 데이터를 관리하기 때문에 데이터의 정합성을 보장할 수 있다.
        - 단점: 시스템이 커질 수록 쿼리가 복잡해지고 성능이 저하되며, 수평적 확장이 어렵다.
    - NoSQL
        - RDBMS가 비대해짐에 따라 관계가 복잡해져, 이를 극복하기 위해 등장하게 된 데이터베이스
        - 장점: NOSQL은 스키마 없이 Key-Value 형태로 데이터를 관리하여 좀 더 자유롭게 데이터를 관리할 수 있다.
        - 단점: 중복된 데이터가 추가 가능하여, 이에 대한 관리가 필요하다.
- JPA
    - ORM이란?
    - JPA를 사용할 때의 이점
    - Lock이란? JPA에서 이것들을 어떻게 처리하는지?
        - DB 락은 여러 개의 트랜잭션들이 하나의 데이터로 동시에 접근하려고 할 때 이를 제어해주는 도구이다.
            - 공유락(LS, Shared Lock): 트랜잭션이 읽기를 할 때 사용하는 락, 데이터를 읽을 수 있지만 쓸 수 없음
            - 베타락(LX, Exclusive Lock): 트랜잭션이 읽고 쓰기를 할 때 사용하는 락, 데이터를 읽고 쓸 수 있음
- 트랜잭션(Transaction)이란?
    - 트랜잭션이란 데이터베이스 작업의 단위로써 하나 이상의 쿼리를 처리할 때 동일한 Connection 객체를 공유하여 에러가 발생한 경우 모든 과정을 되돌리기 위한 방법입니다.
    - 트랜잭션의 ACID란?
        - 원자성(Atomicity): 트랜잭션에 포함된 작업은 전부 수행되거나 전부 수행되지 않아야 한다.
        - 일관성(Consistency): 트랜잭션을 수행하기 전이나 후나 데이터베이스는 항상 일관된 상태를 유지해야 한다.
        - 고립성(Isolation): 수행 중인 트랜잭션에 다른 트랜잭션이 끼어들어 변경중인 데이터 값을 훼손하지 않아야한다.
        - 지속성(Durability): 수행을 성공적으로 완료한 트랜잭션은 변경한 데이터를 영구히 저장해야 한다.   
- 데이터 정합성

[](https://mangkyu.tistory.com/93)

### Web
- 쿠키(Cookie)와 세션(Session)
    - 동작방식
    - 차이점
    - 장단점
- 토큰 기반 인증 방식이란?
    - 동작 방식
    - 장단점
- JWT란?
    - 구조 (3부분)
    - 장단점
[](https://imbf.github.io/interview/2020/12/16/NAVER-Interview-Preparation-8.html)

### Network
- OSI 7 Layer란?
    - ISO(국제표준화기구)에서 네트워크 통신 과정을 7단계로 정의한 국제통신표준규약
    ![image](https://user-images.githubusercontent.com/90819869/154872518-a4c2bd73-5fdd-4953-8894-4f0dcef6232e.png)
    1) 물리 : 전송하는데 필요한 기능 제공 (통신 케이블, 허브)
    2) 데이터링크 : 송/수신 확인, MAC Address로 통신 (브릿지, 스위치)
    3) 네트워크 : IP를 기반으로 데이터(패킷) 전송 경로 결정 (라우팅)
    4) 전송 : TCP/UDP 포트 정보를 참조해 데이터의 전송
    5) 세션 : 통신 시스템 사용자 간의 연결을 유지 및 설정
    6) 표현 : 세션 계층 간의 주고받는 인터페이스를 일관성 있게 제공
    7) 응용 : 사용자가 네트워크에 접근할 수 있도록 서비스를 제공
- 프로토콜이란?
    - 컴퓨터 간 데이터 통신을 원활히 하기 위해 규정한 약속, 신호 송신의 순서(handshaking)나 데이 터표현법, 오류 검출법 등을 정한 것
- HTTP / HTTPS 차이?
    - HTTP 프로토콜이란?
        - 하이퍼텍스트를 전송하는 규약
        - 하이퍼텍스트 : 한 문서에서 다른 문서로 즉시 접근할 수 있는 텍스트
        - 비연결성 프로토콜, REQUEST에 대한 RESPONSE만 전달되고 연결 유지 X
    - HTTPS 프로토콜이란?
        - HTTP + SSL, HTTP로 통신하는 소켓을 SSL(Secure Socket Layer) or TLS(Transport Layer Security)라는 프로토콜로 대체한 것 (새로운 별개의 프로토콜이 아니라 연결 방식이 달라진 것)
        - HTTP는 TCP와 직접 통신하지만, HTTPS에서는 SSL과 통신하고 SSL이 TCP와 통신하는 방식
        - SSL을 사용하기 때문에 암호화와 증명서, 안전성 보호를 이용할 수 있음
        - 공통키 암호화 방식과 공개키 암호화 방식을 혼합한 하이브리드 암호 시스템 사용, 공통키를 공개 키 암호화 방식으로 교환하고 이후 통신은 공통키 암호를 사용하는 방식
- DNS란?
    - DNS란 Host의 Domain Name을 Host의 IP로 변환해주는 서비스를 말합니다. DNS 서버들은 계층구조로 구현된 분산 데이터베이스로 주요 구성 요소로써 Root, Top Level Domain(TLD), Authoritative, Local DNS Server가 존재합니다.
    - DNS 서비스 과정 (캐싱 x)
    1. Host가 gaia.cs.umass.edu의 IP주소를 Local DNS서버에게 요청을 보낸다.
    2. Local DNS서버는 루트 DNS 서버에게 Domain Name을 보내고 루트 DNS 서버는 edu를 인식한 후 TLD 서버의 주소를 넘겨준다.
    3. Local DNS서버는 TLD서버에게 Domain Name을 보내고 TLD 서버는 unmass.edu를 인식한 후 Authoritative 서버의 주소를 넘겨준다.
    4. Local DNS서버는 Authoritative 서버에게 Domain Name을 보내고 gaia.cs.umass.edu에 해당하는 Ip주소를 얻어온다.
    5. 변환된 Ip 주소를 Host에게 넘겨주고 Host는 이 IP를 사용해서 어플리케이션 간에 통신 한다.
- TCP와 UDP의 차이?
    - UDP는 비신뢰적이고 비연결형 서비스를 제공하는 프로토콜이며, 주로 DNS나, IPTV등에서 사용
    - TCP는 신뢰적이고 연결형 서비스를 제공하는 프로토콜이며, HTTP 등에서 사용
- REST와 RESTful의 개념
    - Restful API에서의 URL과 일반적인 HTTP에서의 URL의 차이는?
        - 일반적인 HTTP URL : 기능에 중점을 두어 설계, 예) 회원 정보 호출 - ‘/getUser’
        - Restful API : 자원에 중점을 두고 설계, 예) ‘/user’ 하위에 기능에 대한 구분을 추가, POST, GET, DELETE, PUT 등의 HTTP 메서드를 사용
- HTTP REQUEST - GET과 POST의 차이점
    - GET : 서버에 데이터를 전달할 때 URL Query를 사용해야 하므로 보안에 취약함 / 데이터를 받는 용도로 적합
    - POST : 데이터를 Header에 넣어서 전송하므로 헤더를 열어보지 않으면 확인할 수 없음 / DB 내용을 갱신하거나 서버로 데이터를 전송할 때 적합
    - SSL을 이용한 HTTPS 프로토콜로 데이터 전송을 암호화하면 보안성을 보완할 수 있음, URL 뒤에 붙는 쿼리스트링 내용 모두 암호화되어 전송되기 때문에 보안성을 강화함

[](https://hyonee.tistory.com/136)

</details>
