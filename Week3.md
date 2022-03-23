# DB, Web, Network
## 목차
### [DB](https://github.com/ComputerScienceStudy/tech-interview/edit/main/Week3.md#db-1)
- RDBMS vs NOSQL에 대해서 설명해주세요.
- 인덱스
    - 데이터베이스에서 index를 만들면 내부적으로 어떤동작이 이루어지는지 설명해주시고, 장단점에 대해 설명해주세요.
    - 데이터베이스에서 index를 만들면 성능이 빨라지게 되는 이유를 설명해주세요.
    - hash index를 사용했을 때의 단점과 이유를 설명하세요.
    - 인덱스에 왜 해쉬 보다 B Tree를 쓰는가?
- 트랜잭션이 무엇인가요
    - 트랜잭션에 대해서 설명해주세요.
    - 트랜잭션을 사용할 때의 장점은 무엇인가요
    - 트랜잭션의 특성에 대해 설명해주세요(ACID)
    - 트랜잭션 격리 수준(Transaction Isolation Levels)에 대해서 설명해주세요.
    - 잠금 타임아웃과 교착 상태가 발생하는 이유에 대해서 설명해주세요.
    - 트랜잭션 Rollback은 어떤 경우에 하나요?
- JPA
    - ORM이란?
    - JPA, Hibernate 그리고 Spring Data JPA 각각에 대해서 설명해주세요.
    - 데이터 정합성에 대해서 설명해주세요. JPA에서 이것들을 어떻게 처리하는가요?
    - DB Lock에 대해서 설명해주세요. JPA에서 이것들을 어떻게 처리하는가요?
- QueryDSL을 사용하는 이유와 JPQL과 차이점에 대해서 설명해주세요.
- 정규화에 대해서 설명해주세요
    - Nomalization 이 무엇인가요? Denormalization은 무엇이고, 언제 시행하게 되는지 설명해주세요.
- Elastic Search
    - Elastic Search에 대해서 간단히 설명해주세요.
    - Elastic Search의 인덱스구조와 RDBMS의 인덱스 구조의 차이에 대해 설명해주세요.
    - Elastic Search의 키워드 검색과 RDBMS의 LIKE 검색의 차이에 대해 설명해주세요.
- SQL
    - A라는 테이블이 존재할 때, 새로운 속성(Column)을 추가한다고 할때, 모든 행(row)에 Default값을 넣어주고 싶을때, 어떤 쿼리문을 작성해야할까요
<br><br>

## [WEB](https://github.com/ComputerScienceStudy/tech-interview/edit/main/Week3.md#web-1)

- 쿠키와 세션
    - 쿠키와 세션의 필요성
    - 동작방식
    - 쿠키와 세션은 언제 사용하나요?
- 세션 기반 인증 방식과 토큰 기반 인증 방식의 차이
    - 동작 방식
    - 장단점
- JWT
    - JWT를 사용한 이유와 장, 단점은 무엇인가요?
- 웹 서버와 WAS의 차이점
- 웹 공격 패턴과 방어 방법
    - SQL Injection에 대해서 간단히 설명해주세요.
- RESTful의 개념
    - RESTful이란 무엇이며, 이것에 대해서 아는대로 설명해보세요.
    - 본인이 프로젝트를 진행할때 Restful API를 지키기위해 한 노력은 무엇인가요?

## [Network](https://github.com/ComputerScienceStudy/tech-interview/edit/main/Week3.md#netwwork)

- 웹 브라우저에서 URI에 구글닷컴을 쳤을 때 발생하는 일들을 아는 대로 설명해주세요.
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

<br><br>

---
## DB

### RDBMS vs NOSQL에 대해서 설명해주세요.

---

**핵심답변**

RDBMS는 모든 데이터를 정해진 스키마에 따라 행과 열을 갖춘 2차원 테이블 형태로 구성하며 속성(Attribute)과 값(Value)을 이용하여 데이터를 정의, 저장, 관리합니다. 각 속성과 값을 가진 테이블은 외래 키(foreign key)를 이용해 서로 관계를 맺습니다. 일반적으로 SQL이라는 언어를 활용합니다. 

NoSQL은 SQL언어를 사용하지 않는 데이터베이스 관리 시스템입니다. 정해진 스키마가 없이, 혹은 느슨한 형태의 스키마를 사용하며 테이블 간 관계도 정의하지 않습니다. 따라서 Key 값을 가지고 데이터에 대한 입,출력을 수행합니다. 다양한 형태의 NOSQL 데이터베이스가 있고, 대표적으로 key-value store, document db, graph db 등이 있습니다.
<br><br>

****🤔 테이블 간의 관계는 무엇이 있고, 외래키는 무엇인가요?****

![image](https://user-images.githubusercontent.com/90819869/155289873-cc2c1c41-b0c4-490d-8264-698ce3648566.png)

테이블 간의 관계는 관계를 맺는 테이블의 수에 따라 다음과 같이 나눌 수 있습니다.

1. 일대일(one-to-one) 관계
2. 일대다(one-to-many) 관계
3. 다대다(many-to-many) 관계
<br><br>

🤔 **두 DB의 장단점을 간략하게 말해볼 수 있을까요?**

- RDBMS
    - 장점: 정해진 스키마에 따라 데이터가 저장되므로 데이터 구조가 명확하고, 각 관계를 따라 저장된 데이터는 중복 없음이 보장됩니다.
    - 단점: 테이블 간 관계로 얽혀 있어 시스템이 커진다면 쿼리가 복잡해질 수 있습니다. ~~또한 성능 향상을 위해 서버 자체의 성능을 Scale-up하는 방법 밖에 없기 때문에 비용이 기하급수적으로 늘어날 수 있습니다.~~ !피드백 반영사항: 샤딩(sharding)을 통해서 서버 부하를 줄이는 방법이 있는데, 샤딩은 Scale-out의 방법 중 하나이므로 적절하지 않은 설명입니다.

- NoSQL
    - 장점: 스키마가 없기 떄문에 데이터 구조가 자유롭습니다. 언제든지 데이터를 조정하거나 새로운 필드 추가가 가능합니다. 데이터 분산이 용이하기 때문에 대량의 데이터를 빠르게 처리해야 하는 요즘 상황에 적합할 수 있습니다. 성능 향상을 위해서도 Scale-Up과 Scale-Out 모두 가능합니다.
    - 단점: 데이터 중복 문제가 발생할 수 있고 스키마가 존재하지 않으므로 데이터 구조가 명확하지 않습니다.
<br><br>

🤔 **데이터베이스의 서버 확장에 대해 설명해주세요.**

데이터베이스 서버의 확장성은 수직적 확장(Scale-up)과 수평적 확장(Scale-out)으로 나누어집니다.

- 수직적 확장은 단순히 데이터베이스 서버의 성능을 향상시키는 것입니다.(ex. CPU 업그레이드)
- 수평적 확장은 더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산됨을 의미합니다.

수평적 확장은 NoSQL DB에서만 가능합니다.데이터 저장 방식으로 인해 Relational DB는 일반적으로 수직적 확장만 지원합니다.
<br><br>

🤔 **Nosql이 데이터가 많을 때 속도 측면에서 유리한 이유가 무엇인가요?**

RDBMS는 배열의 형식으로 데이터가 저장되기 때문에, 데이터를 찾기 위해 모든 데이터를 조회합니다.반면 Nosql의 경우 key-value 형식 HashMap 구조이기 때문에 Key값만 있다면 더 빠른 조회가 가능하다고 생각합니다.
<br><br>

🤔 **그렇다면 어떤 기준으로 DB를 선택할 수 있죠?**

RDBMS는 데이터 구조가 명확하고 명확한 스키마가 중요할 때 사용할 수 있습니다. 데이터 중복이 없음이 보장되므로 재무관련, 보안, 개인 건강정보 시스템과 같은 곳에서 선택할 만 합니다.

반면 NoSQL은 막대한 데이터를 저장해야 할 필요가 있고 작성 속도가 빨라야 하는 데이터 분석, 빠른 트로토타입 작업 등에서 사용할 수 있습니다.

둘은 대체될 수 있는 성질 이라기보다 각각 필요한 시점에 적절히 선택하여 사용할 수 있습니다. 때로는 상호 보완적으로도 사용할 수 있을 것입니다. 
<br><br>

---

### 인덱스

---

**핵심답변**

인덱스란, 추가적인 쓰기 작업과 저장 공간을 활용하여 데이터베이스 테이블의 검색 속도를 향상시키기 위한 자료 구조입니다.

즉, 데이터베이스의 목차라고 할 수 있습니다.
<br><br>

**🤔 데이터베이스에서 index를 만들면 내부적으로 어떤동작이 이루어지는지 설명해주시고, 장단점에 대해 설명해주세요.**

테이블에 인덱스를 설정해줬을 때, 인덱스 테이블이 생성되고 인덱스 테이블은 칼럼의 값과 해당 레코드가 저장된 주소를 키와 밸류로 갖게됩니다.

이렇게 생성된 테이블은 정렬화된 B TREE의 구조를 갖게 되고, 인덱스를 참조할 경우 이진탐색과 키의 범위를 바탕으로 해당 키의 밸류가 존재하는 노드를 찾아냅니다.

마지막으로, 인덱스에서 찾은 레코드 주소를 바탕으로 테이블에서 값을 조회합니다.

- 장점
    - 테이블을 조회하고 정렬하는 속도를 향상시킵니다.
    - 전반적인 시스템의 부하를 줄일 수 있습니다.
- 단점
    - 인덱스를 관리하기 위해 DB에 약 10퍼센트의 해당하는 저장공간이 필요합니다.
    - 인덱스를 잘못 사용할 경우 오히려 성능이 저하됩니다.
<br><br>

**🤔 INDEX를 사용하면 성능이 저하되는 경우에 대해 설명해주세요.**

- 업데이트 또는 삭제할 경우 데이터의 인덱스를 삭제하지 않고 사용하지 않음 처리를 하기 때문에 업데이트와 삭제가 많이 사용되는 컬럼일 경우 인덱스의 크기가 누적되어 성능이 저하될 수 있습니다.
- 테이블 풀 스캔의 시간 복잡도가 O(N)이고 인덱스 자료 구조인 B TREE의 시간 복잡도가 O(logN)이기 때문에, 일정 이상의 크기를 갖는 테이블이 아닐 경우에는 오히려 성능이 저하됩니다.
<br><br>

**🤔 데이터베이스에서 index를 만들면 성능이 빨라지게 되는 이유를 설명해주세요.**

인덱스는 데이터와 데이터의 위치를 포함한 자료구조이기에, 인덱스를 생성하면 데이터를 빠르게 조회할 수 있게 됩니다.

성능 향상의 대표적인 예로 인덱스의 정렬화된 B TREE 자료구조를 예로 가질 수 있습니다.

인덱스가 없을 경우 특정 데이터를 찾기 위해서는 테이블을 풀 스캔해야 하기 때문에 시간 복잡도 O(N)을 갖습니다.

반면에, B TREE의 자료구조를 갖는 인덱스는 이진탐색을 바탕으로 데이터 위치를 조회하기 때문에 시간 복잡도 O(logN)을 갖습니다.
<br><br>

**🤔 hash index를 사용했을 때의 단점과 이유를 설명하세요.**

해시 인덱스는 특정 기준보다 크거나 작은 값을 찾을 때 매우 비효율적이라는 단점이 존재합니다.

해시 테이블은 해시 함수를 통해 나온 해시 값을 이용하여 저장된 메모리 공간에 한번에 접근하기 때문에 등호 연산에는 굉장히 효율적입니다.

그러나,  DB에서는 등호 연산 뿐만아니라 부등호 연산도 자주 사용하는데 해시 테이블은 정렬되어있지 않습니다. 이런 특징 때문에 특정 기준보다 크거나 작은 값을 찾을 때는 연산의 성능이 굉장히 떨어지게 됩니다.
<br><br>

**🤔 인덱스에 왜 해쉬 보다 B Tree를 쓰는가?**

해시 테이블은 조회에서는 빠르지만, 정렬되어 있지 않기 때문에 부등호 연산에는 성능이 좋지 않습니다.

반면에, B TREE는 항상 정렬되어 있는 상태이며 데이터들간의 범위를 사용해서 자식노드를 가지기 때문에 인덱스에 매우 유리합니다.

![image](https://user-images.githubusercontent.com/90819869/155291677-cdc9a478-d786-4e49-b528-ecd300d59565.png)

<br><br>

---

### 트랜잭션이 무엇인가요?

---

### 핵심답변

트랜잭션은 일관성 있고 신뢰할 수 있는 방식으로 독립적이게 처리되는 작업 단위입니다.     
따라서 예상치 못한 에러가 발생해도 DB를 신뢰성 있는 상태로 만드는 작업 단위를 제공합니다.        
또한 DB에 동시에 접근하는 경우 프로그램 간 격리를 제공해 에러를 방지하는 역할도 합니다.     
이러한 트랜잭션은 다양한 데이터 항목들을 접근하고 갱신하는 프로그램의 수행의 단위가 됩니다.     
<br><br>

**🤔 트랜잭션의 특성에 대해 설명해주세요(ACID)**

ACID는 트랜잭션이 안전하게 수행된다는 것을 보장하기 위한 성질입니다.

- Atomicity(원자성) : 트랜잭션의 연산은 모든 연산이 완벽히 수행되어야 하며, 아니면, 전혀 어떠한 연산도 수행되지 않은 상태를 보장해야 합니다.
- Consistency(일관성) : 트랜잭션이 진행되는 동안에 데이터베이스가 변경되더라도 업데이트된 데이터베이스로 트랜잭션이 진행되는 것이 아닌 트랜잭션이 진행하기 전 참조한 데이터베이스로 진행되어야 합니다.
- Isolation(독립성) : 트랜잭션은 동시에 실행될 경우 다른 트랜잭션에 의해 영향을 받지 않고 독립적으로 실행되어야 합니다.
- Durability(지속성) : 트랜잭션이 성공적으로 완료되어 커밋되고 나면, 해당 트랜잭션에 의한 모든 변경은 향후에 어떤 소프트웨어나 하드웨어 장애가 발생되더라도 보존되어야 합니다.
<br><br>

**🤔 트랜잭션이 독립적으로 실행된다는 말은 무엇인가요?**

하나의 트랜잭션 실행 중에 다른 트랜잭션의 연산이 끼어들 수 없고, 수행중인 트랜잭션은 완전히 완료될 때까지 다른 트랜잭션에서 수행 결과를 참조할 수 없다는 것을 말합니다.
<br><br>

**🤔 트랜잭션 수행이 보존해야 할 일관성은 무엇이 있을까요?**

기본 키, 외래 키 제약과 같은 명시적인 무결성 제약 조건들뿐만 아니라, 자금 이체 예에서 두 계좌 잔고의 합은 이체 전후가 같아야 한다는 사항과 같은 비명시적인 일관성 조건들도 있습니다.
<br><br>

**🤔 트랜잭션 격리 수준(Transaction Isolation Levels)에 대해서 설명해주세요.**

트랜잭션 격리수준은 고립도와 성능의 트레이드 오프를 조절합니다.

- **READ UNCOMMITTED**: 다른 트랜잭션에서 커밋되지 않은 내용도 참조할 수 있습니다.
    - 따라서 오염된 읽기, 재현 불가한 읽기, 허상 읽기 문제가 발생할 가능성이 있습니다.
- **READ COMMITTED**: 다른 트랜잭션에서 커밋된 내용만 참조할 수 있습니다.
    - 이로써 오염된 값 읽기 문제는 해결되지만 재현 불가한 읽기, 허상 읽기 문제는 여전히 남습니다.
- **REPEATABLE READ**: 트랜잭션에 진입하기 이전에 커밋된 내용만 참조할 수 있습니다.
    - 오염된 값 읽기, 재현 불가한 읽기 문제는 해결되지만 허상 읽기는 여전히 남습니다.
- **SERIALIZABLE**: 트랜잭션에 진입하면 락을 걸어 다른 트랜잭션이 접근하지 못하게 합니다. 동시성 문제는 모두 해소되지만 성능이 매우 떨어집니다.

Dirty Read, Nonrepeatable Read와 같은 문제를 예방하려면 트랜잭션을 서로 완전히 격리 하면 되겠지만

그렇게 하면 트랜잭션을 한 줄로 세워놓고 하나씩 실행하는 꼴이라서 엄청난 성능 저하가 옵니다.

그래서, 성능을 감안하며, 요건을 충족하는 가장 낮은 수준의 트랜잭션 격리 수준을 선택하는게 좋습니다.
<br><br>

**🤔 잠금 타임아웃과 교착 상태가 발생하는 이유에 대해서 설명해주세요.**

잠금 타임아웃은 다음과 같은 상황에서 발생합니다.

트랜잭션A의 갱신과 트랜잭션B의 갱신이 충돌하는 경우, wait이 발생하고 지정 시간이 지나면 잠금 타임아웃이 발생합니다.

교착상태는 다음과 같은 상황에서 발생합니다.

트랜잭션A는 a에, 트랜잭션B는 b에 갱신을 한 상태일 떄,

트랜잭션 A가 b에 갱신을 하려 하고, 트랜잭션B는 a에 갱신을 하려고 하면 교탁 상태가 발생합니다.
<br><br>

**🤔 트랜잭션 Rollback은 어떤 경우에 하나요?**

하나의 트랜잭션 처리가 비정상적으로 종료되면 트랜잭션의 원자성을 위해 롤백을 사용합니다.

트랜잭션을 사용해 데이터를 추가하다 에러가 발생할 때, 트랜잭션을 롤백함으로써 해당 트랜잭션에서 작업한 모든 연산을 취소하여 실제 데이터베이스에 반영하지 않도록 합니다.

롤백하고 난 후에는 해당 트랜잭션을 재시작하거나 폐기해야 합니다.
<br><br>

---

### JPA

---

**🤔  ORM(Object Relational Mapping)이란?**

객체와 관계형 데이터베이스를 매핑해주는 것으로 쿼리문 작성 없이 객체를 데이터베이스에 직접 저장할 수 있게 도와주는 기술입니다.
<br><br>

**🤔 JPA, Hibernate 그리고 Spring Data JPA 각각에 대해서 설명해주세요.**

- JPA란 Java Persistance API의 약자로 JAVA ORM 표준 기술 명세입니다.자바에서 데이터를 DBMS에 영구히 기록할 수 있는 환경을 제공하는 API이자, 인터페이스입니다.
- Hibernate는 JPA의 구현체 중 하나입니다.JPA는 단순히 명세이기 때문에 구현이 없습니다. 따라서 인터페이스를 직접 구현한 라이브러리가 필요하며, Hibernate가 그 역할을 합니다. 내부적으로 JDBC API를 사용합니다.
- Spring Data JPA는 JPA를 편하게 쓸 수 있도록 만들어 놓은 모듈입니다. JPA를 한 단계 추상화시킨 Repository라는 인터페이스를 제공합니다.

![image](https://user-images.githubusercontent.com/90819869/155292257-13ca87a0-60a2-4484-8982-22d31a7a84e9.png)
<br><br>

**🤔 JPA가 클래스가 아닌 인터페이스를 사용하는 이유에 대해서 설명해주세요.**

상속을 통해, 코드를 재사용한다면, 부모클래스를 상속받은 자식클래스에서는 부모 클래스의 모든 메서드를 그대로 사용할 수 있기에, 캡슐화를 위반합니다.

또한, 원치 않은 메서드들도 상속됩니다. 원치 않은 메서드도 상속되면 의도치 않은 버그도 발생시킬 수 있습니다.

인터페이스를 사용하면, 함수의 특징만을 정의하고 함수의 내용이 없기에 결합도가 낮습니다.

클래스의 기본 틀을 제공하여 정의된 메서드를 통해서만 코드를 재사용할 수 있기에, 개발자들에게 정형화된 개발을 할 수 있게 해줄 수 있습니다.
<br><br>

**🤔 JPA를 사용할 때의 이점에 대해서 설명해주세요.**

JPA는 ORM기술이기 때문에 RDBMS에 연결하여 데이터를 직접 조작할 필요없이, 자바코드로 표현하여 객체 중심으로 개발할 수 있다는 장점이 있습니다.

그로인해 JPA에 익숙하다면 생산성이 높아진다는 장점을 가지고 있습니다.

정리하자면, 생산성, 유지보수성, DB접근 최소화로인한 성능 최적화(영속성 컨텍스트), 패러다임 불일치 해결, 데이터 접근 추상화와 벤더 독립성이 있습니다.
<br><br>

**🤔 JPA의 단점은 무엇인가요**

JPA는 자동으로 쿼리를 생성해주기 때문에, 통계처리와 같은 복잡한 쿼리보다 실시간 쿼리에 최적화 되어있씁니다.따라서, 미세하고 복잡한 쿼리문을 사용해야할 때는 Mybatis와 같은 Mapper방식을 사용하는 것이 더 효율적일 수 있습니다.
<br><br>

**🤔 JPA 영속성 컨텍스트의 이점(5가지)를 설명해주세요.**

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
    - 우선적으로 1차캐시에 저장하고, `commit()`시 쿼리문들을 DB에 보냅니다.
    - `flush()`는 1차캐시를 지우지 않고, 쿼리를 DB에 날려 DB와 싱크는 맞추는 역할을 하고
    - 쿼리를 보내고난 후 `commit()`을 하게 됩니다.
    - 트랜잭션의 커밋은 이 `flush()`와 `commit()` 2가지 일을 하게 됩니다.
        
    ![image](https://user-images.githubusercontent.com/90819869/155292560-ec8eb67f-4fad-44da-8f5f-e25540cb3584.png)
        
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
        
        ![image](https://user-images.githubusercontent.com/90819869/155292704-791763f8-a53e-444f-9c2d-f78833f9fdee.png)
        
5. 지연 로딩
    - 지연로딩을 사용하면, 엔티티와 연관관계에 있는 데이터를 사용하는 시점에 불러올 수 있습니다.
    - 이 때의 이점은, DB가 객체를 불러올때, 연관관걔의 데이터를 가지고 오지않아 크기를 줄임으로써 부담을 줄이는 장점이 있습니다.
<br><br>

**🤔 데이터 정합성에 대해서 설명해주세요. JPA에서 이것들을 어떻게 처리하는가요?**

데이터 정합성이란, 서로 모순이 없이 일관되게 일치한다는 의미입니다.

JPA에는 영속성 컨텍스트가 있는데, 이곳에서 1차 캐쉬에서 엔티티와 스냅샷을 비교하여 정합성을 유지합니다. 이러한 1차 캐쉬의 단위는 트랜잭션의 단위와 동일합니다.
<br><br>

**🤔 DB Lock에 대해서 설명해주세요. JPA에서 이것들을 어떻게 처리하는가요?**

Lock은 데이터 영속성과 트랜잭션 처리의 순차성을 보장하기 위한 방법입니다. 데이터 시스템은 여러곳에서 동시에 접근할 수 있는 구조이기 때문에 필연적으로 데이터의 변경 또는 충돌로 인한 오염의 가능성이 있습니다. Lock은 이러한 경우를 방지해줍니다.

- Shared Lock: Read Lock이라고도 하는 공유 락은 데이터를 읽을 때 사용합니다. 같은 Read Lock끼리는 동시 접근이 가능한데, 읽는 것 만으로는 이는 데이터 일관성과 무결성을 해치지 않기 때문입니다. 다만 Exclusive Lock의 접근은 제한됩니다.
- Exclusive Lock: Write Lock, 베타락이라고도 하는 Exclusive Lock은 데이터를 변경할 때 사용합니다. 트랜잭션이 완료될 때 까지 유지 됩니다. Exclusive Lock이 끝날 때 까지는 어떠한 접근도 허용되지 않습니다.
<br><br>

👉 JPA Lock

- **Optimistic Lock**: 데이터 갱신 시 경합이 일어나지 않을 것이라고 낙관적으로 보고 잠그는 기법입니다. 예컨대 회원 정보는 해당 회원에 의해서만 발생할 것이므로 동시 요청이 발생할 가능성이 낮습니다.
- **Pessimistic Loc**k: 동일 데이터를 동시에 수정할 가능성이 높다는 비관적 전제에서 잠그는 방식입니다. 예컨대 상품의 재고는 동시에 여러 사람이 주문할 가능성이 높습니다. 이럴 경우 비관적 잠금을 통해 예외를 발생시키지 않으면서 정합성을 유지하는 것이 중요합니다. 주로 Exclusive Lock을 이용합니다.
- **Implicit Lock**: 코드에 명시적으로 지정하지 않아도 잠금이 발생하는 Lock입니다. `@Version`이나 `@OptimisticLocking` 어노테이션이 있는 경우 자동적으로 충돌 감지를 위해 잠금이 실행됩니다. DB의 경우에는 업데이트, 삭제 쿼리 발행시 암시적인 Row Exclusive Lock이 실행됩니다.
- **Explicit Lock**: 프로그램을 통해 명시적으로 잠금을 실행합니다. JPA에서 엔티티를 조회할 떄 LockMode를 지정하거나, SELECT FOR UPDATE 쿼리를 통해 직접 지정할 수 있습니다.
<br><br>

**🤔 JPA는 로그 기법에 대해 어떻게 처리하는가?**

1. **표준 출력**: application.properties에 아래 코드를 추가합니다. 간단한 방식이지만 로깅 프레임 워크를 최적화하지 않고 모든 것을 표준 출력으로 직접 언로드하기 때문에 권장되는 방식은 아닙니다.

```sql
spring.jpa.show-sql=true
```

2. **로거를 통한 처리**: 속성 파일에서 로거를 구성해 SQL문을 기록하는 방식도 있습니다.

```sql
logging.level.org.hibernate.SQL=DEBUG
logging.level.org.hibernate.type.descriptor.sql.BasicBinder=TRACE
```

3. **JDBCTemplate 쿼리 로깅**: JdbcTemplate을 사용할 때 로깅을 구성하는 방식은 다음 속성이 필요합니다.

```sql
logging.level.org.springframework.jdbc.core.JdbcTemplate=DEBUG
logging.level.org.springframework.jdbc.core.StatementCreatorUtils=TRACE
```
<br><br>

**🤔 JPA에서 N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.**

- N+1 문제가 발생하는 이유는, JPA는 JPQL을 생성하여 실행하게 되는데, JPQL은 엔티티 객체와 필드 이름을 갖고 쿼리를 만들기 때문에 객체의 연관관계 매핑에 의해서 관계가 맺어진 다른 객체들이 함께 조회되기 때문에 발생합니다.
- 즉시로딩의 경우, 모든객체를 불러오기에 당연히 N+1 문제가 발생하고, 지연로딩의 경우에도, 객체를 조회하고, 반복문으로 연관된 관계의 매핑을 조회할때 N+1 문제가 발생합니다.
- 지연로딩으로 한번 한번의 쿼리문으로 조회되어 불러온 객체가 있지만, 지연로딩의 경우, 연관된 매핑관계에있는 객체의 정보는 불러오지 않기 때문에, 해당 객체의 정보로 조건문을 사용하여 쿼리문을 별도로 생성하여 값을 불러와 데이터의 개수만큼의 N개의 쿼리문이 추가로 발생되어집니다.

```sql
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

```sql
Hibernate: select post0_.post_id as post_id1_1_, post0_.create_dt as create_d2_1_, post0_.updated_dt as updated_3_1_, post0_.author as author4_1_, post0_.content as content5_1_, post0_.like_count as like_cou6_1_, post0_.title as title7_1_ from post post0_

Hibernate: select commentlis0_.post_id as post_id6_0_0_, commentlis0_.comment_id as comment_1_0_0_, commentlis0_.comment_id as comment_1_0_1_, commentlis0_.create_dt as create_d2_0_1_, commentlis0_.updated_dt as updated_3_0_1_, commentlis0_.author as author4_0_1_, commentlis0_.content as content5_0_1_, commentlis0_.post_id as post_id6_0_1_ from comment commentlis0_ where commentlis0_.post_id=?

Hibernate: select commentlis0_.post_id as post_id6_0_0_, commentlis0_.comment_id as comment_1_0_0_, commentlis0_.comment_id as comment_1_0_1_, commentlis0_.create_dt as create_d2_0_1_, commentlis0_.updated_dt as updated_3_0_1_, commentlis0_.author as author4_0_1_, commentlis0_.content as content5_0_1_, commentlis0_.post_id as post_id6_0_1_ from comment commentlis0_ where commentlis0_.post_id=?

Hibernate: select commentlis0_.post_id as post_id6_0_0_, commentlis0_.comment_id as comment_1_0_0_, commentlis0_.comment_id as comment_1_0_1_, commentlis0_.create_dt as create_d2_0_1_, commentlis0_.updated_dt as updated_3_0_1_, commentlis0_.author as author4_0_1_, commentlis0_.content as content5_0_1_, commentlis0_.post_id as post_id6_0_1_ from comment commentlis0_ where commentlis0_.post_id=?

Hibernate: select commentlis0_.post_id as post_id6_0_0_, commentlis0_.comment_id as comment_1_0_0_, commentlis0_.comment_id as comment_1_0_1_, commentlis0_.create_dt as create_d2_0_1_, commentlis0_.updated_dt as updated_3_0_1_, commentlis0_.author as author4_0_1_, commentlis0_.content as content5_0_1_, commentlis0_.post_id as post_id6_0_1_ from comment commentlis0_ where commentlis0_.post_id=?
```

- Comment 정보를 조회하면, Post에 대한 조회는 이미 끝난 상태라서 JOIN으로 쿼리가 생성이 안 됩니다.
- 단지 Post에 대한 정보 ID로 조회할 수밖에 없어서 `where comment.postId=?` 형식으로 JPQL 쿼리를 생성합니다. 이로 인해 매번 조회 쿼리가 생성이 되어 N 번 실행하는 이슈가 발생합니다.
<br><br>

**🤔 N+1 해결 방법**

지연로딩시, N+1 문제의 해결방법으로는,

패치 조인(fetch join), EntityGraph, Batch Size 지정 + 즉시 로딩 3가지가 있습니다.

1. **fetch join**
    - JPQL에 fetch join 키워드를 사용해서 join 대상을 함께 조회할 수 있습니다.
    - 지연로딩을 이용해서 객체를 조회 시, 함께불러오길 원하는 연관관계의 객체를 join해서 같이 불러오는 방식입니다.
    
    ```sql
    @Repository
      public interface PostRepository extends JpaRepository<Post, Long> {
           @Query("select p from Post p left join fetch p.commentList")
           List<Post> findAllWithFetchJoin();
      }
    ```
    
2. **EntityGraph**
    - `@EntityGraph` JPQL에서 fetch join을 하게 되면 하드코딩해야하는 단점이 있습니다.
    - 이를 보완하기 위해 `@EntityGraph` 어노테이션을 사용할 수 있습니다.
    
    ```sql
    @EntityGraph(attributePaths = {"articles"}, type = EntityGraphType.FETCH)
       @Query("select distinct u from User u left join u.articles")
       List<User> findAllEntityGraph();
    ```
    
3. **Batch Size 지정 + 즉시 로딩**
    - JPQL 페치 조인 대신 Batch 크기를 지정하는 방법도 있습니다.
    - `@BatchSize` 어노테이션에 size를 지정하고 fetch 타입은 즉시로 설정합니다.
    
    ```sql
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

**🤔 JPA Paging N+1 문제 해결 방법**

- Pagination에서의 문제 발생 distinct를 쓰는 이유는 연관관계에 대해서 fetch join으로 가져온다고 했을 때 중복된 데이터가 많기 때문에 중복 데이터를 처리하기 위함인데, Paging 처리는 쿼리를 날릴 때 진행되기 때문에 JPA에게 pagination 요청을 하여도 distinct때와 마찬가지로 중복된 데이터가 있을 수 있으니 limit offset을 걸지 않고 인메모리에 다 가져오게 됩니다. 이렇게 되면 paging을 하는 의미가 사라지게 됩니다.
- Paging 해결방법 : ~ToOne ~ToOne 관계에 있는 경우에는 fetch join을 걸어도 Pagination이 원하는대로 제공됩니다.

```sql
@EntityGraph(attributePaths = {"user"}, type = EntityGraphType.FETCH)
@Query("select a from Article a left join a.user")
Page<Article> findAllPage(Pageable pageable);
```

- Paging 해결방법 : Batch Size 사용자가 임의로 연관관계에 대해 데이터의 사이즈를 알때 사용할 수 있는 방법으로 지연로딩하는 객체에 대해서 Batch성 loading하는 것입니다. 기존의 지연로딩은 객체를 조회할 때 그때그때 쿼리문을 날려서 N+1이 발생한 반면 객체를 조회하는 시점에 쿼리를 하나만 날리는게 아니라 해당하는 Article에 대해서 쿼리를 batch size개를 날리게 되는 것입니다. 즉, 지연 로딩으로 생길 N+1 문제를 batch size만큼 가져와 미연에 방지하는거라고 볼 수 있습니다.
- Paging 해결방법 : @Fetch(FetchMode.SUBSELECT) BatchSize와 동일한 동작을 하지만, size를 개발자가 임의로 정하는 것이 아닌 스프링에서 자동으로 설정해줍니다. 일반적으로 모든 batchsize를 가져오기 때문에, 성능적인 테스트가 필요합니다.
- MultipleBagFetchException 해결책 - fetch join 두개 이상의 fetch join을 설정할 경우 메모리에 너무 많은 값이 들어와 MultipleBagFetchException을 발생합니다. 이 경우에는 Set자료구조를 사용해 해결할 수 있습니다. 하지만 Pagination에는 사용할 수 없습니다.

```sql
@OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
private Set<Article> articles = emptySet();

@OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
private Set<Question> questions = emptySet();
```

- MultipleBagFetchException 해결책 : batchsize
    - List 자료구조를 꼭 사용해야하는 경우에 사용할 수 있습니다.
    - 2개 이상의 Collection join을 사용하는데, Pagination을 사용해야해서 인메모리 OOM을 방지하고자 하는 경우에 사용할 수 있습니다.
    
    ```sql
    @BatchSize(size = 100)
    @OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
    private Set<Article> articles = emptySet();
    
    @BatchSize(size = 100)
    @OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
    private Set<Question> questions = emptySet();
    ```
    
    ```sql
    @BatchSize(size = 100)
    @OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
    private List<Article> articles = new ArrayList<>();
    
    @BatchSize(size = 100)
    @OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
    private List<Question> questions = new ArrayList<>();
    ```
    
    ```sql
    @Query("select distinct u from User u left join u.articles left join u.questions")
    Page<User> findAllPage2(Pageable pageable);
    ```
    

---

### QueryDSL을 사용하는 이유와 JPQL과 차이점에 대해서 설명해주세요.

---

Spring Data JPA가 기본적으로 제공하는 CRUD 메서드 및 쿼리 메서드 기능으로 부족한 기능을 보강하기 위해 사용하고,

JPQL을 사용할 경우 직접 작성한 쿼리 스트링이 런타임 시에 오타 혹은 문법적인 오류로 인한 서비스의 크리티컬한 문제를 방지하고자 QueryDSL을 사용합니다.

- 차이점
    
    JPQL의 경우 직접 쿼리 스트링을 입력해줘야하는 반면, QueryDSL은 자바 코드로 이뤄져있어 문법과 오타에 대한 에러를 개발단계에서 잡을 수 있습니다.
    
<br><br>

**🤔 QueryDSL 장점에 대해서 설명해주세요.**

- 문자가 아닌 코드로 쿼리를 작성함으로써, 컴파일 시점에 문법 오류를 쉽게 확인할 수 있습니다.
- 자동완성 등 IDE의 도움을 받을 수 있습니다.
- 동적인 쿼리 작성이 편리합니다.
- 쿼리 작성시 제약 조건등을 메서드 추출을 통해 재사용할 수 있습니다.
<br><br>

---

### 정규화에 대해서 설명해주세요

---

1. **정규화(Nomalization)가 무엇인가요? 비정규화(Denormalization)는 무엇이고, 언제 시행하게 되는지 설명해주세요.**
    1. **정규화(Normalization)**
        1. 이상현상이 존재하는 테이블을 분해하여 여러 개의 테이블을 생성하는 과정
        2. 장점
            - 데이터 저장에 대한 효율성
            - 테이블 간 데이터 중복 방지
                - 무결성 유지
                - DB의 저장 용량 확보
        3. 테이블이 분해되는 정도에 따라 정규화 단계가 나눠진다.
            1. **제 1 정규화**
                - 테이블의 모든 컬럼이 원자값(하나의 값)을 갖도록 분해
                
                ![image](https://user-images.githubusercontent.com/90819869/155305842-ee711ac0-1787-47e3-a1b4-4ade90c108dd.png)
                
            2. **제 2 정규화**
                - 제1 정규형을 만족하고, 완전 함수 종속(기본키의 부분집합이 결정자가 되어선 안됨을 의미)을 만족하도록 분해
                
                ![image](https://user-images.githubusercontent.com/90819869/155305874-36d842a3-fc75-4906-ad76-eb6e8a73d536.png)
                
                - 학생번호로 조회 시, 강의실이 복수값으로 나올 수 있습니다.
                - 즉, 기본키(학생번호, 강좌이름) 중 강좌이름이 강의실을 결정하는 결정자이므로 별도의 테이블로 분해해줌으로써 완전함수종속 조건 만족
                
                ![image](https://user-images.githubusercontent.com/90819869/155305902-b34a3c66-4eef-4089-b21f-8159e82feac9.png)
                
            3. **제 3 정규화**
                - 제2 정규형을 만족하고, 이행적 종속(A→B, B→C = A→C)을 없애도록 분해
                - 각 속성들을 독립적으로 만드는 것이 아니라, 서로 참조가 가능하도록 분해
                
                ![image](https://user-images.githubusercontent.com/90819869/155305934-a712135d-8e95-4d40-b06d-6e36ed86e4b5.png)
                
                - 예를 들어, 이행적 종속을 따를 경우 학생번호→수강료가 되어버려서 강좌 변경 시에도 수강료가 변경되지 않는다. 이를 방지하기 위해, (학생번호, 강좌이름)과 (강좌이름, 수강료) 테이블로 분해한다
                
                ![image](https://user-images.githubusercontent.com/90819869/155305951-9e58ca02-4350-4553-aba9-30c5e54c8c6e.png)
                
            4. **BCNF 정규화**
                - 제 3 정규형을 만족하고, 모든 결정자가 후보키가 되도록 분해
                
                ![image](https://user-images.githubusercontent.com/90819869/155305973-d3dd6714-9c05-4afb-b6f3-411be521d982.png)
                
                - 기본키(학생번호, 특강이름)는 교수를 결정하는데, 교수 또한 특강이름을 결정하는 결정자이다.
                - 문제는 교수가 결정자이지만 후보키는 아니라는 점이다. 따라서, 모든 결정자가 후보키가 될 수 있도록 분해한다.
                
                ![image](https://user-images.githubusercontent.com/90819869/155306016-6830549e-abad-43ee-a896-31f298f2a7ec.png)
                
    2. **비정규화(Denomalization)**
        1. 하나 이상의 테이블에 데이터를 중복해 배치하는 최적화 기법
            - 시스템의 성능 향상, 개발 및 운영의 편의성 등을 위해 정규화된 데이터 모델을 통합, 중복, 분리하는 과정입니다 = **의도적으로 정규화 원칙을 위배하는 것**
        
<details>
<summary>💡 언제 사용되나요?</summary>
  
- 디스크 I/O 량이 많아서 조회 시 성능이 저하될 때
- 테이블끼리의 경로가 너무 멀어 조인으로 인한 성능 저하가 예상될 때
- 칼럼을 계산하여 조회할 때 성능이 저하될 것이 예상될 때
- (일반적으로) 조회에 대한 처리 성능이 중요하다고 판단될 때

</details>  
<br><br>

### **🤔 잘 조직되지 않는 테이블에서 일어날 수 있는 이상들은 무엇인가요?**

- 삽입 이상
    - 관계에 데이터를 삽입할 때 의도와 상관없이 원하지 않는 값들도 함께 삽입되는 현상
- 삭제 이상
    - 관계에 데이터를 삭제할 때 의도와 상관없는 값들도 함께 삭제되는 현상
- 갱신 이상
    - 관계의 행에 있는 속성 값을 갱신할 때 일부 행의 데이터만 갱신되어 데이터에 모순이 생기는 현상
- 정규화를 거치면, 위의 이상들이 일어나지 않도록 할 수 있다. 또한, 현실적으로 과도한 정규화는 DB 질의 처리 속도를 떨어 뜨리기 때문에 제 3 정규화 또는 보이스 코드 정규화까지만 정규화를 진행하며, 필요에 따라 비정규화 작업을 하기도 한다.
<br><br>

---

### Elastic Search

---

- **Elastic Search에 대해서 간단히 설명해주세요.**
    
    Elastic Search는 Apache Lucene 기반의 Java 오픈소스 분산 검색 엔진입니다. 텍스트, 숫자, 위치 기반 정보, 정형 및 비정형 데이터 등 모든 유형의 데이터를 검색, 분석할 수 있습니다. 
    
    보통 단독으로 사용하기보다는 ELK 스택이라고 부르는 Logstash, Kibana, Beats를 추가적으로 사용합니다.
<br><br>
    
- **Elastic Search의 인덱스구조와 RDBMS의 인덱스 구조의 차이에 대해 설명해주세요.**
    
    Elastic Search는 Inverted-Index 구조로 데이터를 저장합니다. 이는 책의 색인을 생각해보면 쉬운데, 특정 단어가 출현하는 doc을 저장하는 것입니다. 이렇게 하면 전문(Full-text) 검색시에 RDBMS에 비해 뛰어난 성능을 보장합니다.
    
    반면 RDBMS에는 다양한 인덱스 구조가 있지만, 대표적으로 밸런스 트리의 일종인 B-Tree 방식이 있습니다. 밸런스 트리는 트리의 노드가 한 방향으로 쏠리지 않도록 노드 삽입 및 삭제 시 특정 규칙에 의해 재정렬되어 왼쪽과 오른쪽 자식이 균형을 유지하는 형태입니다. 
<br><br>
 
- **Elastic Search의 키워드 검색과 RDBMS의 LIKE 검색의 차이에 대해 설명해주세요.**
    
    **RDBMS**에서는 where like '%...%'의 형식으로 데이터 검색이 가능합니다. 와일드카드로 시작하지 않는 경우에만 인덱스를 사용하고 나머지 경우는 전체를 탐색하기 때문에 상대적으로 속도가 느립니다. 또한 단순 텍스트 매칭에 대한 검색만을 제공하고 특히 한글 검색의 경우 빈약한 편입니다. 비정형 데이터의 색인과 검색도 불가능합니다.
    
    반면 **ES**의 키워드 검색은 document를 저장할 때 수행하는 알고리즘과 동일한 알고리즘으로 키워드를 분리합니다. 그 중에서 랭킹알고리즘을 통해서 가장 유사한 순서대로 결과를 나타냅니다. 텍스트를 여러 단어로 변형하거나 텍스트 특질을 이용한 동의어, 유의어를 활용한 검색도 가능합니다. 또한 비정형 데이터 검색 및 색인이 가능하고, 형태소 분석을 통한 자연어 처리를 할 수 있습니다. 더불어 역인덱싱 지원으로 매우 빠르게 검색할 수 있습니다.
<br><br>
  
🤔  **역인덱싱에 대해서 설명해주세요.**
    
역인덱싱은 대용량 텍스트의 효율적인 검색을 위해 고안된 방법으로, 문서를 유의미한 단어로 분리하여 정렬된 목록을 작성한 후에, 각 단어가 어느 문서에 있는지 표시하여 작성하는 작업입니다. 이 방법은 단어들이 이미 정렬되어 있기 때문에 검색 및 탐색의 속도가 매우 빠릅니다. 이 때 문서를 유의미한 단어로 분리하기 위해 형태소 분석 과정을 거칩니다.
    
<br><br>

---

### SQL

---

- **A라는 테이블이 존재할 때, 새로운 속성(Column)을 추가하고, 모든 행(row)에 Default값을 넣어주고 싶을다면, 어떤 쿼리문을 작성해야할까요?**

`alter table ~add 문`을 사용할 수 있습니다.

```sql
Alter table A add 컬럼명 자료형 default 초깃값;
```
<br><br>

---
## Web

### 쿠키와 세션
---

**핵심답변**

- 쿠키
    - 쿠키는 클라이언트의 로컬에 Key-Value쌍이 String 형태로 저장되는 데이터 파일입니다. 브라우저가 종료된 후에도 상태가 유지됩니다. 클라이언트의 상태 정보(이름, 값, 만료 날짜 및 시간, 경로정보)를 포함하고 있습니다.

- 세션
    - 세션은 일정 시간 같은 클라이언트로부터 들어오는 일련의 요청을 하나의 상태로 보고, 그 상태를 유지하는 기술입니다. 브라우저가 종료되기 전까지 상태가 유지됩니다. 상태 유지 수단으로 쿠키를 사용하지만, 사용자 정보를 클라이언트 로컬이 아닌 서버측에서 관리합니다.
<br>

- **쿠키와 세션의 필요성**
    
    HTTP 프로토콜의 경우 “Connectionless, Stateless”한 특성이 있어 요청간에 의존관계가 없습니다. 또한  매 통신마다 새로 연결해야 하기 때문에 현재의 클라이언트가 이전 접속자와 같은지를 알 수 있는 방법이 없습니다. 이 점을 보완하는 데 쿠키와 세션이 사용됩니다. 
    
- 동작방식
    - **쿠키 동작방식**
        1. 클라이언트가 페이지를 요청합니다.
        2. 서버에서 쿠키를 생성하고 HTTP 헤더에 쿠키를 포함 시켜 응답합니다.
        3. 브라우저가 종료되어도 쿠키 만료 기간이 있다면 클라이언트에서 보관하고 있습니다.
        4. 같은 요청을 할 경우 HTTP 헤더에 쿠키를 함께 보냅니다.
        5. 서버에서 쿠키를 읽어 이전 상태 정보를 변경할 필요가 있을 때, 쿠키를 업데이트 하여 변경된 쿠키를 HTTP 헤더에 포함시켜 응답합니다.
    - **세션 동작방식**
        1. 클라이언트가 서버에 접속 시 세션 ID를 발급 받습니다.
        2. 클라이언트는 세션 ID에 대해 쿠키를 사용해서 저장하고 가지고 있습니다.
        3. 클라이언트는 서버에 요청할 때, 이 쿠키의 세션 ID를 같이 서버에 전달해서 요청합니다.
        4. 서버는 세션 ID를 전달받아서 별다른 작업없이 세션 ID로 세션에 있는 클라이언트 정보를 가져와서 사용합니다.
        5. 클라이언트 정보를 가지고 서버 요청을 처리하여 클라이언트에게 응답합니다.
<br>

- **쿠키와 세션은 언제 사용하나요?**
    - 쿠키: 클라이언트 로컬에 저장되므로 보안에 취약해 로그인같은 인증에는 잘 쓰이지 않습니다. 단순한 **아이디의 저장**이나, **쇼핑몰의 장바구니 담아두기** 같은 기능에 사용합니다.
    - 세션: 보안상 중요한 작업인 **로그인 기능**에 사용됩니다.
<br><br>

---
### 세션 기반 인증 방식과 토큰 기반 인증 방식의 차이
---

- 동작 방식
    - 세션 기반 인증
        
        ![image](https://user-images.githubusercontent.com/90819869/155297256-c837465a-7138-45ba-bdd2-829444f77386.png)
        
        1. 사용자가 로그인하면 서버에서 검증합니다.
        2. 인증된 사용자라면 서버에 로그인한 유저의 정보가 저장되고, Session ID를 발급해 응답합니다.
        3. Session ID는 쿠키에 실려 사용자의 브라우저에 저장됩니다.
        4. 사용자가 다음 요청을 할 때, Session ID가 헤더에 담겨 전송됩니다.
        5. 서버는 쿠키 내부의 Session ID를 이용해 유저 정보를 가져와 확인하고, 이 작업의 반복으로 로그인이 유지됩니다.
    
    - 토큰 기반 인증
        
        ![image](https://user-images.githubusercontent.com/90819869/155297287-80c05220-17ff-4359-9f2a-94c3ee2f1dd1.png)
        
        1. 사용자가 로그인하면 서버는 해당 정보를 검증하고, 인증되면 토큰을 발급합니다.
        2. 클라이언트는 토큰을 저장해두고, 서버에 요청시마다 토큰을 HTTP요청 헤더에 담아 서버에 함께 전달합니다.
        3. 서버는 토큰을 검증하고, 요청에 응답합니다.

- 장단점
    - 세션 기반 인증
        - 장점: 클라이언트에게 요청시 Session ID만 전송하기 때문에 사이즈가 작습니다. 서버에서 정보를 관리하므로 조금 더 안전합니다.
        - 단점: 중앙 세션 관리 시스템이 없으면 시스템 확장이 어렵고, 중앙 세션 시스템에 장애가 발생하면 시스템 전체에 문제가 생길 수 있습니다. 또한 메모리에 세션 정보를 저장해 나가다보면 메모리 성능 저하를 일으킬 수 있습니다.
    
    - 토큰 기반 인증
        - 장점: 토큰이 클라이언트에 저장되기 때문에 서버는 완전히  Stateless합니다. 쿠키 사용에 따른 보안 취약점이 사라지고, 토큰에 선택적인 권한을 부여해 발급할 수 있습니다. 예컨대 OAuth 방식은 Google, Facebook같은 소셜 계정을 통한 로그인 기능 구현이 가능해 직접적인 운영과 관리 부담이 적습니다.
        - 단점: 토큰의 길이가 긴 경우 인증 요청이 많아질수록 네트워크 부하가 늘어납니다. 대표적인 토큰 인증 방식인 JWT의 경우 Payload 자체는 암호화되지 않기 때문에 담을 수 있는 정보가 제한적입니다. 토큰을 탈취당하면 유효기간이 지나기 전에는 대처가 어렵습니다.
<br><br>

---
### JWT
---

- **JWT를 사용한 이유와 장, 단점은 무엇인가요?**
    - 사용 이유:
        
        기존의 세션 인증 방식이나 토큰 인증 방식은, 인증 과정에서  DB를 거쳐야 합니다. 하지만 JWT의 경우 사용자 인증에 필요한 정보(자가수용적 Self-Contained 정보, 토큰 정보, 전달해야 하는 정보, 토큰 검증에 대한 Signature 등)를 토큰 자체에 담고 있어서, 별도의 저장소에 정보를 저장할 필요가 없습니다. 
        
        또한 JSON 객체를 사용하기 때문에 인코딩 시 XML보다 간결하고 사이즈가 작습니다. 또한 JSON Parser는 보통 대부분의 프로그래밍 언어에서 객체와 직접 Mapping되기 때문에 자연스럽고 쉽게 인증 방식을 사용할 수 있습니다.
        
    - 장점:
        - 웹표준(RFC 7519)으로, 서비스 도입 및 향후 디버깅과 관리가 용이한 측면이 있습니다. 사용자 인증에 필요한 정보를 담고 있어 별도의 저장소가 필요 없습니다. 트래픽에 대한 부담도 낮으며,  REST 서비스로 제공이 가능합니다.
    - 단점:
        - 토큰의 Payload에 정보를 담기 때문에 정보가 많아질수록 토큰의 길이가 늘어나 네트워크에 부하를 발생시킬 수 있습니다. 또한 Payload를 탈취하여 디코딩하면 데이터를 볼 수 있기 때문에 중요한 정보는 담지 말거나, 혹은 JWE라는 별도의 암호화를 거쳐야 합니다. Stateless한 특성상 한번 만들어지면 임의 삭제가 불가능하고 토큰 만료시간을 별도로 지정해주어야 합니다.
<br><br>

---

### 웹 서버와 WAS의 차이점

---

**핵심답변**

어떤 타입의 컨텐츠를 제공하는지의 차이입니다. `웹서버`는 **정적인 컨텐츠**를 제공하는 서버입니다. `WAS`는 DB 조회나, 어떤 로직을 처리해야 하는 **동적 컨텐츠**를 제공합니다.

대표적인 WAS로는 아파치 톰켓, 웹로직, 제이보스 등이 있습니다.
<br><br>

**🤔 Web Server와 WAS를 구분하는 이유가 뭔가요?**

- **Web Server가 필요한 이유**
    - Web Server를 통해 정적인 파일들을 Application Server까지 가지 않고, 앞에서 빠르게 처리해줄 수 있습니다.
    - 따라서, Web Server에서 정적 컨텐츠만 처리하도록 기능을 분배하여 서버의 부담을 줄일 수 있게 됩니다.

- **WAS가 필요한 이유**
    - 웹 페이지의 정적 컨텐츠와 동적 컨텐츠에 대한 유저의 요청을 Web Server가 제공하는 데에는 한계가 있습니다.
    - 따라서, WAS를 통해 요청에 맞는 데이터를 DB에서 가져와서 비즈니스 로직에 맞게 그때 그때 결과를 만들어서 제공함으로써 자원을 효율적으로 사용할 수 있게 됩니다.

- **정리**
    - 즉, 자원 이용의 효율성 및 장애 극복, 배포 및 유지보수의 편의성 을 위해 Web Server와 WAS를 분리하여 사용해주는 게 좋습니다.
        - Web Server를 WAS 앞에 두고 필요한 WAS들을 Web Server에 플러그인 형태로 설정하면 더욱 효율적인 분산 처리가 가능
<br><br>

---
### 웹 공격 패턴과 방어 방법
---

- **SQL Injection에 대해서 간단히 설명해주세요.**

**핵심답변**

클라이언트의 입력값을 조작하여 임의의 SQL문을 삽입해 서버의 데이터베이스를 공격할 수 있는 공격 방식입니다.
<br><br>

**🤔 SQL Injections의 대응방법은 무엇이 있나요**

1. 입력값에 대한 검증
2. Prepared Statement 구문사용
3. 웹 방화벽 사용
<br><br>

**🤔 크로스 사이트 스크립팅 -XSS**

공격자가 상대방 브라우저에 스크립트가 실행되도록 해 사용자의 세션을 가로채거나, 웹사이트를 변조하거나, 악의적 컨텐츠를 삽입하거나, 피싱 공격을 진행하는 것을 말합니다.

XSS공격은 기본적으로 <script>태그를 사용하기 때문에 XSS 공격을 차단하기 위해 태그 문자(<,>)등 위험한 문자 입력 시 문자 참조로 필터링하고, 서버에서 브라우저로 전송 시 문자를 인코딩하는 것으로 방지할 수 있습니다.

![image](https://user-images.githubusercontent.com/90819869/155297736-8b1cd1fd-2d1e-4f0d-8a77-ba9ca7b0582c.png)
<br><br>

---
### RESTful의 개념
---
  
- **RESTful이란 무엇이며, 이것에 대해서 아는대로 설명해보세요.**
    
    REST 아키텍쳐를 따르는 시스템으로, 아래 원칙을 지켜 설계하는 것을 의미합니다.
    
    1. HTTP URI를 통해 자원(Resource)을 명시하고
    2. HTTP Method(POST, GET, PUT, DELETE)를 통해
    3. 해당 자원(URI)에 대한  CRUD Operation을 적용합니다.
    
- **본인이 프로젝트를 진행할때 Restful API를 지키기위해 한 노력은 무엇인가요?**
    - 초기에는 단순히 GET과 POST만 활용했으나,  리팩토링 후 다른 HTTP Method의 적극적인 활용을 통해 어떤 CRUD 기능을 수행하는 지 알 수 있도록 변경했습니다.
    - 리소스의 집합인 Collection에는 단수가 아닌 복수를 사용했습니다.
    
        ex) • [GET] /user → • [GET] /users
    
    - Collection으로 시작해서 Identifier로 끝냈습니다.
        
        ex) • GET /shops/{shopId}/category/{categoryId}/price → • GET /shops/{shopId}
        
    - URL에는 동사보다 명사를 사용했습니다.
        
        ex) • [POST] /updateuser/{userId} → • [PUT] /user/{userId}
        
    - 또한, URI 설계시 아래의 기준으로 변경했습니다.
        - /관련 DB Columns/관련 Field값
            - ex) sign up → POST /users/2
        - /는 계층관계를 나타냄, 큰 범위/작은 범위
            - ex) /tils/idx/like/idx
        - /리소스명/리소스 ID/관계가 있는 다른 리소스명
            - ex) my til delete → /users/userid/tils/idx
<br><br>

---
## Netwwork

### 웹 브라우저에서 URI에 구글닷컴을 쳤을 때 발생하는 일들을 아는 대로 설명해주세요.
---
  
**핵심답변**

![image](https://user-images.githubusercontent.com/90819869/155298164-5d761734-3fb2-4bcd-a64a-efe86d3ef7dd.png)
1. 사용자가 URL주소를 입력하면, 도메인 네임을 DNS서버에서 검색합니다.
2. DNS서버에서 해당 도메인 네임에 해당하는 IP주소를 찾아 사용자가 입력한 URL 정보와 함께 전달합니다.
3. 웹 페이지 URL 정보와 IP 주소는 HTTP 프로토콜을 사용하여 HTTP 요청 메세지를 생성합니다.
4. HTTP 요청 메시지를 TCP 프로토콜을 사용하여 인터넷을 거쳐 해당 IP 주소의 컴퓨터로 전송합니다.
5. 도착한 HTTP 요청 메세지는 HTTP 프로토콜을 사용하여 웹페이지 URL 정보로 변환됩니다.
6. 웹 서버는 도착한 웹 페이지 URL 정보에 해당하는 데이터를 검색합니다.
7. 웹 서버에서는 다시 HTTP 프로토콜을 사용하여 HTTP 응답 메시지를 생성하고, 이를 다시 TCP 프로토콜을 이용해 인터넷을 거쳐 원래 컴퓨터로 전송됩니다.
8. 도착한 HTTP 응답메시지는 HTTP 프로토콜을 사용해 웹 페이지 데이터로 변홥니다.
9. 변환된 웹 페이지 데이터는 웹 브라우저에 의해 출력되어 사용자가 볼 수 있도록 합니다.
<br><br>
  
---
### 사용자가 웹브라우저를 통해 서버에 이미지를 요청해서 사용자에게 보여주기까지 과정을 설명하세요.
---
  
**핵심답변**

![image](https://user-images.githubusercontent.com/90819869/155301536-37f835e1-092b-49f4-984d-d7ee28cc844c.png)

1. 웹 브라우저가 https://www.google.com/images/google.png로 **이미지를 요청**해야 한다는 것을 인지합니다.
2. 웹 브라우저는 DNS 서버에서 URL을 이용해 **IP를 추출**합니다.
3. 웹 브라우저와 서버간의 **TCP 커넥션을 맺습니다**.(3 way handshaking)
4. 이미지 요청하기 위한 GET 메서드로 **HTTP 요청 메세지를 만듭니다**.
5. 웹 브라우저는 **서버에 HTTP 요청**을 보냅니다.
6. 서버는 메세지를 받고 HTTP 메세지를 확인하고, 해당 Resource가 존재한다면 200코드와 함께 **응답**해줍니다.
7. 웹 브라우저는 응답받은 메세지를 해석하여 사용자에게 보여줍니다.
<br><br>

---
### OSI 7계층
---
  
- **OSI 7계층이 무엇인지 그 존재 이유에 대해서 설명해보세요.**
    
    - 네트워크에서 통신이 일어나는 과정을 7단계로 나눈 것
    - 상호 이질적인 네트워크간의 연결에서 호환성의 결여를 막기 위해 개발된 모형
    - OSI 7계층이 있음으로써, 통신이 일어나는 과정을 단계별로 파악할 수 있습니다.
    - 문제 발생 시, 효율적으로 해결이 가능합니다.
        - 7단계 중 특정한 곳에 이상이 생기면 다른 단계의 장비 및 소프트웨어를 건드리지 않고도 이상이 생긴 단계만 고칠 수 있습니다.
    
    ![image](https://user-images.githubusercontent.com/90819869/155301851-3ed5e6f9-2ba0-4235-ab92-526e92844ab8.png)
    
    1. 1계층 - 물리계층(Physical Layer)
        - 전기 데이터의 전송만을 담당 (통신 케이블, 리피터, 허브 등)
    2. 2계층 - 데이터 링크계층(DataLink Layer)
        - 정보의 오류와 흐름을 관리 (브리지, 스위치, 이더넷 등)
    3. 3계층 - 네트워크 계층(Network Layer)
        - 경로를 선택하고 주소를 정하고 경로에 따라 패킷을 전달 (라우터)
        - 라우팅, 흐름 제어, 세그멘테이션, 오류 제어, 인터네트워킹 등을 수행
        - `라우팅` : 데이터를 목적지까지 가장 안전하고 빠르게 전달 (중요 기능)
    4. 4계층 - 전송 계층(Transport Layer)
        - 데이터를 받으면 해당 데이터를 하나로 합쳐서 5계층으로 전달 (예: TCP)
        - 양 끝단(End to end)의 사용자들이 신뢰성있는 데이터를 주고 받을 수 있도록 하는 역할
        - `연결 기반(connection oriented)` : 전송 계층이 패킷들의 전송이 유효한지 확인하고 전송 실패한 패킷들을 다시 전송
    5. 5계층 -세션 계층(Session Layer)
        - 데이터가 통신하기 위한 논리적인 연결(세션)을 담당
        - TCP/IP 세션을 생성 및 제거
        - 양 끝단의 응용 프로세스가 통신을 관리하기 위한 방법을 제공 (동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(Full Duplex) 등)
    6. 6계층 - 표현 계층(Presentation Layer)
        - 데이터 표현이 상이한 응용 프로세스의 독립성을 제공하고, 암호화
        - 코드 간의 번역 담당, MIME 인코딩이나 암호화 등을 수행
    7. 7계층 - 응용 계층(Application Layer)
        - 최종 목적지로서, 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행 (HTTP, FTP, SMTP, POP3, IMAP, Telnet 등의 프로토콜)

- **TCP/IP 4계층에 대해 설명해보세요.**

    - OSI 참조 모델을 기반으로 상업적이고 실무적으로 이용될 수 있도록 단순화된 모형
    
    | TCP/IP 4계층 | 역할 | 데이터 단위 | 전송주소 | 예시 | 장비 |
    | --- | --- | --- | --- | --- | --- |
    | L4
    응용 계층 | 응용프로그램 간 데이타 송수신 | Data/Message | - | 파일 전송, 이메일, FTP, HTTP, SSH, Telnet, DNS, SMTP 등 | - |
    | L3
    전송 계층 | 호스트 간 자료 송수신 | Segment | Port | TCP, UDP, RTP, RTCP 등 | 게이트웨이 |
    | L2
    인터넷 계층 | 데이타 전송을 위한 논리적 주소 지정 및 경로 지정 | Packet | IP | IP, ARP, ICMP, RARP, OSPF | 라우터 |
    | L1
    네트워크 연결 계층 | 실제 데이타인 프레임을 송수신 | Frame | MAC | Ethernet, PPP, Token Ring 등 | 브리지, 스위치 |
    
    1. L1 - 네트워크 연결 계층(Network Access Layer/Network Interface Layer)
        - 물리적으로 데이터가 네트워크를 통해 어떻게 전송되는지를 정의
        - MAC, LAN, 패킷망 등에 사용되는 것 (예: Ethernet, PPP, Token Ring 등)
    2. L2 - 인터넷 계층(Internet Layer)
        - 통신 노드 간의 IP패킷을 전송하는 기능과 라우팅 기능(경로 설정)을 담당
        - IP, ARP, RARP 등
    3. L3 - 전송 계층(Transport Layer)
        - 통신 노드 간 연결을 제어하고, 신뢰성 있는 데이터 전송을 담당
        - TCP, UDP 등
    4. L4 - 응용 계층(Application Layer)
        - TCP/UDP 기반의 응용 프로그램 구현 및 응용 프로그램 간 데이터 송수신을 담당
        - FTP, HTTP, SSH 등

- **웹 서버 소프트웨어(Apache, Nginx)는 OSI 7계층 중 어디서 작동하는지 설명해보세요.**

    - `응용계층(Application Layer)`에서 작동됩니다.
    - 웹 서버 소프트웨어는 HTTP 프로토콜을 이용하여 HTML, CSS, Javascript, image와 같은 정적인 정보들을 웹 브라우저에 전송합니다.  
    - HTTP 프로토콜은 OSI 7 계층인 Application Layer에 위치한 프로토콜로서, 브라우저(클라이언트)와 서버 사이에 정보를 주고 받기 위한 프로토콜로 사용됩니다.
        

- **웹 서버 소프트웨어(Apache, Nginx)의 서버 간 라우팅 기능은 OSI 7계층 중 어디서 작동하는지 설명해보세요.**

    - 서버간 라우팅 기능은 3계층인 `네트워크 계층(Network Layer)`에서 진행합니다.
    - 네트워크 계층에서 가장 중요한 기능이 데이터를 목적지까지 가장 안전하고 빠르게 전달하는 **라우팅 기능**입니다.
<br><br>

---
### DNS란?
---  
  
- 예를 들어, `www.example.com`과 같이 사람이 읽을 수 있는 이름을 `192.0.2.1`과 같은 숫자 IP 주소로 변환하여 컴퓨터가 서로 통신할 수 있도록 한다.
- 인터넷의 DNS 시스템은 이름과 숫자 간의 매핑을 관리하여, 마치 **전화번호부**와 같은 기능을 한다.
- DNS 서버는 **이름에 대한 요청을 IP 주소로 변환**하여 최종 사용자가 도메인 이름을 웹 브라우저에 입력할 때 해당 사용자를 어떤 서버에 연결할 것인지를 제어한다. = `쿼리`
- **동작원리**
    
    ![image](https://user-images.githubusercontent.com/90819869/155302736-fb5a8917-052f-4130-92f2-3769a569e95a.png)
    
    1. 웹 브라우저에 `www.naver.com`을 입력하면, Local DNS에게 `"www.naver.com"`이라는 hostname에 대한 IP 주소를 요청한다.
        - Local DNS에 없으면 다른 DNS name 서버 정보(Root DNS 정보)를 받는다.
    2. Root DNS 서버에 `"www.naver.com"`에 대해 요청한다.
    3. Root DNS 서버로 부터 "com 도메인"을 관리하는 TLD (Top-Level Domain) 이름 서버 정보를 전달 받는다.
    4. TLD에 `"www.naver.com"`에 대해 요청한다.
    5. TLD에서 "name.com" 관리하는 DNS 정보를 전달한다.
    6. "example.com" 도메인을 관리하는 DNS 서버에 `"www.naver.com"` 호스트네임에 대한 IP 주소를 요청한다.
    7. Local DNS 서버에게 `www.naver.com`에 대한 IP 주소(예:222.122.195.6)를 응답 받는다.
    8. Local DNS는 `www.naver.com`에 대한 IP 주소를 캐싱을 하고 IP 주소 정보를 전달한다.
<br><br>

---
### HTTP
---
  
- **HTTP의 역할은 무엇인가요?**

World Wide Web에서 하이퍼텍스트 문서를 교환하기 위하여 사용되는 통신규약입니다.
<br><br>

- **HTTP와 HTTPS의 차이를 설명하세요.**

`HTTP`는 따로 암호화 과정을 거치지 않기 때문에 중간에 패킷을 가로챌 수 있고, 수정할 수 있습니다. 따라서 **보안이 취약**합니다.

이를 **보완**하기 위해 나온 것이 `HTTPS`입니다. 중간에 암호화 계층을 거쳐서 **패킷을 암호화**합니다.
<br><br>

- **HTTPS에 대해서 설명하고 SSL Handshake에 대해서 설명해보세요.**

`HTTPS`는 HTTP 통신을 하는 소켓 부분을 SSL이나 TSL이라는 프로토콜로 대체한 것입니다.

HTTPS는 제3자 인증, 공개키 암호화, 비밀키 암호화를 사용합니다.

제3자 인증은 믿을 수 있는 인증기관에 등록된 인증서만 신뢰하는 것이고,

**공개키 암호화**는 비밀키를 공유하기 위해 사용합니다.

**비밀키 암호화**는 통신하는 데이터를 암호화하는데 사용합니다.
<br>
  
`SSL Handshake` 과정은 다음과 같습니다.

1. 클라이언트는 TCP 3way handshake를 수행한 이후 Client Hello를 전송합니다.
2. 서버는 인증서를 보냅니다.
3. 클라이언트는 받은 인증서를 신뢰하기 위해서 등록된 인증기관인지 확인합니다.
    
    이 인증서는 인증기관의 개인키로 암호화되어있고, 공개키로 검증할 수 있습니다.
    
    클라이언트는 클라이언트에 내장된 공개키를 이용해서 통신에 사용할 비밀키를 암호화해서 서버에 보냅니다.
    
4. 서버는 이를 개인키로 확인하고 이후 통신은 공유된 비밀키로 암호화되어 통신합니다.
5. 클라이언트와 서버는 헨드쉐이크 단계를 서로에게 알린다.
<br><br>

- **HTTP 프로토콜의 특징**

1. 비연결을 지향합니다. (Connectionless)
클라이언트가 request를 서버에 보내고, 서버가 클라이언트에 요청에 맞는 response를 보내면 바로 연결을 끊습니다.

2. 상태정보 유지를 하지 않습니다. (Stateless)
연결을 끊는 순간 클라이언트와 서버의 통신은 끝나며 상태 정보를 유지하지 않습니다.
<br><br>

- **HTTP 1.1 VS 2.0**

`HTTP/1.1`는 Connection당 하나의 요청을 처리 하도록 설계 되어 있습니다.

그래서 동시전송이 불가능하고 요청과 응답이 순차적으로 이루어 지게 됩니다.

그렇다 보니 HTTP문서 안에 포함된 다수의 리소스 (CSS, JS, Images)를 처리하려면 요청할 리소스 개수에 비례해서 Latency(대기 시간)는 길어지게 됩니다.

<br>
  
**HTTP/1.1 단점**으로는 다음과 같습니다.
- HOL(Head Of Line) Blocking 현상이 발생합니다.
- 매 요청별로 connection을 만들기 때문에, TCP상에서 동작하는 HTTP의 특성상 3-way handshake가 반복적으로 일어나고 불필요한 RTT증가와 네트워크 지연을 초래하여 성능을 저하시키게 됩니다. 
- Header 구조가 무겁습니다.
    HTTP/1.1의 헤더에는 많은 메타정보들이 저장되어져 있습니다.  
    
    사용자가 방문한 웹페이지는 다수의 HTTP요청이 발생하게 되는데, 이 경우 매 요청시 마다 중복된 헤더값을 전송하게 됩니다.
<br>

**`HTTP/2.0` 장점**은 다음과 같습니다.

- 한 커넥션으로 동시에 여러개의 메세지를 주고 받을 있으며, 응답은 순서에 상관없이 stream으로 주고 받습니다.
    
    HTTP/1.1의 Connection Keep-Alive, Pipelining의 개선이라 보면 됩니다.
    
- 리소스간의 우선순위를 설정하여, 브라우저 렌더링이 늦어지는 문제를 해결합니다.
    
    예를 들어, 클라이언트가 요청한 HTML문서 안에 CSS파일 1개와 Image파일 2개가 존재하고, 이를 클라이언트가 각각 요청하고 난 후 Image파일보다 CSS파일의 수신이 늦어지는 경우 브라우저의 렌더링이 늦어지는 문제가 발생합니다.
    
    HTTP/2의 경우 리소스간 우선순위를 설정하여 이런 문제를 해결하고 있습니다.
    
- 서버는 클라이언트의 요청에 대해 요청하지도 않은 리소스를 마음대로 보내줄 수도 있습니다.
    
    클라이언트가 HTML문서를 요청했고 해당 HTML에 여러개의 리소스(CSS, Image)가 포함되어 있는 경우, HTTP/1.1에서 클라이언트는 요청한 HTML문서를 수신한 후 HTML문서를 해석하면서 필요한 리소스를 재요청합니다.
    
    HTTP/2에선 Server Push를 이용하면 클라이언트가 요청하지도 않은 (HTML문서에 포함된 리소스) 리소스를 Push 해주는 방법으로 클라이언트의 요청을 최소화 해서 성능 향상을 이끌어 냅니다.
    
    이를 PUSH_PROMISE 라고 부르며 PUSH_PROMISE를 통해서 서버가 전송한 리소스에 대해선 클라이언트는 요청을 하지 않습니다.
<br><br>

- **HTTP 응답코드**

    - 클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능을 합니다.

|구분|설명|
|--|--|
|1xx (Informational)|요청이 수신되어 처리중|
|2xx (Successful)|요청 정상 처리|
|3xx (Redirection)|요청을 완료하려면 추가 행동이 필요|
|4xx (Client Error)|클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음|
|5xx (Server Error)|서버 오류, 서버가 정상 요청을 처리하지 못함|

<br><br>

✔️ **자주 사용하는 HTTP 응답 코드**

- 200 OK - 요청 성공
- 201 Created - 요청에 따른 새로운 리소스 생성 성공
- 204 No Content - 요청은 성공했지만 딱히 보내줄 내용이 없음
- 400 Bad Request - 잘못된 요청
- 401 Unauthorized - 비인증 요청
- 403 Forbidden - 비승인 요청
- 404 Not Found - 존재하지 않는 리소스에 대한 요청
- 500 Internal Server Error - 서버 에러
- 503 Service Unavailable - 서비스가 이용 불가능함
<br><br>

- **HTTP Method - PUT과 PATCH의 차이**

- `PUT`: 리소스의 전체를 클라이언트가 서버에게 보내는 리소스로 업데이트 하는데 사용합니다. (해당 리소스가 없으면 생성합니다.)
- `PATCH`: 리소스의 부분적으로 수정하는데 사용합니다. 의미론적으로 UPDATE와 더 가깝다고 할 수 있습니다.
<br><br>

---
### TCP와 UDP
---
  
- **TCP와 UDP의 차이점에 대해서 설명해보세요.**

`TCP`는 연결 지향형 프로토콜이고 UDP는 데이터를 데이터그램 단위로 전송하는 프로토콜입니다.

TCP는 가상 회선을 만들어 신뢰성을 보장하도록 (흐름 제어, 혼잡 제어, 오류 제어)하는 프로토콜로

따로 신뢰성을 보장하기 위한 절차가 없는 UDP에 비해 속도가 느린 편입니다.

그래서 TCP는 그래서 파일 전송과 같은 신뢰성이 중요한 서비스에 사용되고,
  
<br>
  
`UDP`는 스트리밍, RTP와 같이 연속성이 더 중요한 서비스에 사용됩니다.

하지만 UDP도 신뢰성을 UDP 자체에서 보장하지 않는 것 뿐이지, 개발자가 직접 신뢰성을 보장하도록 할 수 있습니다.

그래서 HTTP/3은 QUIC이라는 프로토콜을 기반으로 하는데, QUIC은 UDP를 기반으로 합니다.

즉, UDP 자체는 신뢰성을 보장하지 않지만, 추가적인 정의를 통해 신뢰성을 보장받을 수 있습니다.
<br><br>

**🤔 3 way hand shake에 대해서 설명하세요.**

TCP 3way handshake는 가상회선을 수립하는 단계입니다.

클라이언트는 서버에 요청을 전송할 수 있는지, 서버는 클라이언트에게 응답을 전송할 수 있는지 확인하는 과정입니다.

SYN, ACK 패킷을 주고받으며, 임의의 난수로 SYN 플래그를 전송하고, ACK 플래그에는 1을 더한값을 전송합니다.

정확한 순서는 SYN(n) → ACK(n + 1), SYN(m) → ACK(m + 1) 순으로 일어납니다.
<br><br>

**🤔 왜 임의의 난수로 지정하나요?**

Connection을 맺을 때 사용하는 포트는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용됩니다.

따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용하는 가능성이 존재합니다. 

서버 측에서는 패킷의 SYN을 보고 패킷을 구분하게 되는데, 난수가 아닌 순처적인 Number가 전송된다면 이전의 Connection으로부터 오는 패킷으로 인식할 수 있습니다. 

이런 문제가 발생할 가능성을 줄이기 위해서 난수로 설정합니다.
<br><br>

**🤔 4 way hand shake에 대해서 설명하세요.**

TCP의 연결을 해제(Connection Termination)하는 과정입니다.

클라이언트는 서버에게 연결 해제를 통지하고, 서버가 이를 확인하고 클라이언트에게 이를 받았음을 전송해주고, 최종적으로 연결이 해제됩니다. 

단, 서버에서 소켓이 닫혔다고 통지해도 클라이언트 측에서는 일정시간 대기하는데, 혹시나 패킷이 나중에 도착할 수 있기 때문입니다.
<br><br>

**🤔 TCP의 연결 설정 과정(3단계)과 연결 종료 과정(4단계)이 단계가 차이나는 이유는 무엇인가요?**

Client가 데이터 전송을 마쳤다고 하더라도 Server는 아직 보낼 데이터가 남아있을 수 있기 때문에 일단 FIN에 대한 ACK만 보내고, 데이터를 모두 전송한 후에 자신도 FIN 메시지를 보내기 때문입니다.
