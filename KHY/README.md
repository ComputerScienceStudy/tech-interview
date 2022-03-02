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
- Bean에 대해 설명해보세요.
  - Spring Bean이란 무엇인가요?
  - 스프링 Bean의 생성 과정을 설명해주세요.
  - 스프링 Bean의 Scope에 대해서 설명해주세요.
  - Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.
- MVC 패턴이란?
- 프론트 컨트롤러 패턴이란 무엇인가요?
- Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.
- Filter와 Interceptor 차이
  - Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?
- AOP(Aspect Oriented Programming)란 무엇일까요?
- Spring에서 예외처리하는 방법에 대해서 설명해주세요.
- Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.
- DTO를 사용하는 이유
</details>


## [Database, Web, Network](https://github.com/ComputerScienceStudy/tech-interview/blob/main/KHY/Content/DB%20Web%20Network.md)
<details>
<summary>목차</summary>

### Database
- RDBMS vs NOSQL에 대해서 설명해주세요.
- 인덱스
  - 데이터베이스에서  index를 만들면 내부적으로 어떤동작이 이루어지는지 설명해주시고 장단점에 대해 설명해주세요.
  - 데이터베이스에서 index를 만들면 성능이 빨라지게 되는 이유를 설명해주세요.
  - hash index를 사용했을 때의 단점과 이유를 설명하세요.
  - 인덱스에 왜 해쉬 보다 B Tree를 쓰는가?
- 트랜잭션
  - 트랜잭션에 대해서 설명해주세요.
  - ACID에 대해서 설명해주세요.
  - 트랜잭션 격리 수준(Transaction Isolation Levels)에 대해서 설명해주세요.
  - DBMS는 어떻게 트랜잭션을 관리할까요?
  - 잠금 타임아웃과 교착 상태가 발생하는 이유에 대해서 설명해주세요.
  - 트랜잭션 Rollback은 어떤 경우에 하나요?
- 정규화
  - Nomalization 이 무엇인가요? 
  - Denormalization은 무엇이고, 언제 시행하게 되는지 설명해주세요.
- Elastic Search
  - Elastic Search에 대해서 간단히 설명해주세요. 
  - Elastic Search의 인덱스구조와 RDBMS의 인덱스 구조의 차이에 대해 설명해주세요. 
  - Elastic Search의 키워드 검색과 RDBMS의 LIKE 검색의 차이에 대해 설명해주세요.
- JPA
  - ORM이란?
  - JPA, Hibernate 그리고 Spring Data JPA 각각에 대해서 설명해주세요.
  - JPA를 사용할 때의 이점에 대해서 설명해주세요.
  - JPA에서 N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.
  - 데이터 정합성에 대해서 설명해주세요. JPA에서 이것들을 어떻게 처리하는가요?
  - DB Lock에 대해서 설명해주세요. JPA에서 이것들을 어떻게 처리하는가요?
- SQL
  - A라는 테이블이 존재할 때, 새로운 속성(Column)을 추가한다고 할때, 모든 행(row)에 Default값을 넣어주고 싶을때, 어떤 쿼리문을 작성해야할까요?

### Web
- 쿠키와 세션
  - 쿠키와 세션의 필요성
  - 동작방식
  - 쿠키와 세션은 언제 사용하나요?
- 세션 기반 인증 방식과 토큰 기반 인증 방식의 차이
  - 동작방식
  - 장단점
- JWT 
  - JWT에 대해서 간단히 설명해주세요.
  - JWT를 사용한 이유와 장점은 무엇인가요?
  - JWT 단점은 무엇인가요?
- 웹 서버와 WAS의 차이점
- 웹 공격 패턴과 방어 방법
  - SQL Injection에 대해서 간단히 설명해주세요.
- Restful의 개념
  - Restful이란 무엇이며, 이것에 대해서 아는대로 설명해보세요.
  - 본인이 프로젝트를 진행할때 Restful API를 지키기위해 한 노력은 무엇인가요?
- Challenge
  - 웹 사이트를 제작했는데 고해상도 이미지를 많이 사용하여 페이지 로딩 속도가 느립니다. 최적화 하는 방법에 대해서 모두 설명하세요.
  - 브라운이 새로운 검색 엔진을 개발하려고 합니다. 어떻게 설계 및 개발 것인지 아는 지식을 모두 동원하여 설명하세요.

### Network
- 웹 브라우저에서 URI에 구글닷컴을 쳤을 때 발생하는 일들을 아는 대로 설명해주세요.<br>
  DNS 서버, HTTP 프로토콜(80포트), HTTPS 프로토콜(443포트), DOM, IP, PORT 등등의 용어를 사용해서
- 사용자가 웹브라우저를 통해 서버에 이미지를 요청해서 사용자에게 보여주기까지 과정을 설명하세요.
- OSI 7계층
  - OSI 7계층이 무엇인지 그 존재 이유에 대해서 설명해보세요.
  - TCP/IP 4계층에 대해 설명해보세요.
  - 웹 서버 소프트웨어(Apache, Nginx)는 OSI 7계층 중 어디서 작동하는지 설명해보세요.
  - 웹 서버 소프트웨어(Apache, Nginx)의 서버 간 라우팅 기능은 OSI 7계층 중 어디서 작동하는지 설명해보세요.
- DNS란?
- HTTP
  - HTTP의 역할
  - HTTP와 HTTPS의 차이를 설명하세요.
  - HTTPS에 대해서 설명하고 SSL Handshake에 대해서 설명해보세요.
  - HTTP 프로토콜의 특징
  - HTTP 1.1 VS 2.0 VS 3.0
  - HTTP 응답코드
  - HTTP Method - PUT과 PATCH의 차이
- TCP와 UDP
  - TCP와 UDP의 차이점에 대해서 설명해보세요.
  - 3 way hand shake에 대해서 설명하세요.
</details>

### [Cheet Sheet](https://sunzero.notion.site/39419328056f4c08a5168ef4e24e6da6)
