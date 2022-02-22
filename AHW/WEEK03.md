# [3주차 면접 스터디] DB 정리

### 목차

[RDBMS vs NoSQL](https://github.com/ComputerScienceStudy/tech-interview/blob/main/AHW/WEEK03.md#rdbms-vs-nosql%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%84%A4%EB%AA%85%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94)

[인덱스(Index)](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#%EC%9D%B8%EB%8D%B1%EC%8A%A4)

[트랜젝션](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98)

[JPA](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#jpajava-persistence-api)

[정규화(Normalization) vs 비정규화(Denormalization)](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#%EC%A0%95%EA%B7%9C%ED%99%94%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%84%A4%EB%AA%85%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94)

[SQL](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#sql)

---

### RDBMS vs NOSQL에 대해서 설명해주세요.

1. **RDBMS**
  - 관계형 데이터베이스 관리 시스템
    - 테이블 간 관계를 맺고 모여있는 집합체
  - 모든 데이터를 2차원 테이블 형태로 표현 (`Column: 속성(Attribute)` 과 `Row: 값(value)`)
  - `외래 키(foreign key)`를 이용해 테이블 간 Join이 가능

  ![image](https://user-images.githubusercontent.com/90819869/155027771-68a55b57-6da7-45ea-a434-c8398cd17ace.png)

  - 장점
    - 정해진 스키마에 따라 데이터를 저장하므로, 작업의 완전성을 보장
    - 데이터의 분류, 정렬, 탐색 속도, 업데이트가 비교적 빠름
  - 단점
    - 테이블 간 관계를 맺고 있어서 시스템이 커질 경우, Join문이 많은 복잡한 쿼리 생성
    - `Scale-up`만을 지원하므로, 이로 인한 비용이 증가 (성능 향상을 위한 장비)
    - 반드시 스키마 규격에 맞춰 데이터를 다뤄야 하므로, 스키마가 변경될 경우 수정이 번거롭고 처리가 어려움

<br>

2. **NoSQL**
  - 분산된 환경에 데이터를 JSON 또는 XML 파일의 형태로 저장하는데이터베이스
  - 데이터·테이블 간 관계를 정의하지 않음
    - 정해진 스키마가 없어, 보다 자유롭게 데이터를 저장
  - `key 값`만 가지고도 데이터에 대한 입·출력 가능
    - 하나의 ”ID:123”을 기준으로 한 모든 정보를 하나의 json/xml 파일에 저장 가능

      ![image](https://user-images.githubusercontent.com/90819869/155027930-b1425d91-0339-4169-bdab-b0af88d135a6.png)

  - 장점
    - RDBMS로는 관리할 수 없는 복잡하고 용량이 큰 데이터 관리가 가능
      - 비정형 데이터(이미지, IoT 데이터)
      - 다양한 형태의 DB 구성(Document, Graph, Key value, wide column 등)
    - 여러대의 서버에 나누어서 데이터를 저장할 수 있기 때문에, `Scale-up`이 빠르고 저렴

      ![image](https://user-images.githubusercontent.com/90819869/155027947-8882fa96-f470-4157-b490-64bc697d3d57.png)

  - 단점
    - 데이터 중복이 발생할 수 있고, 중복된 데이터가 변경될 경우 모든 컬렉션에서 수정 필요
    - 오픈소스 기술이기 때문에 정형화된 스탠다드가 없음
    - 최신 기술이기 때문에, 사용하기가 RDBMS에 비해 어려움
<details>
<summary>💡 RDBMS와 NoSQL은 언제 사용해야 될까요?</summary>

-  RDBMS
    - 데이터 구조가 확실하고 변경될 여지가 없는 경우
    - 명확한 스키마가 중요한 경우
    - 데이터 변경/확장이 잦은 시스템 (중복된 데이터가 없어 변경이 용이하기 때문)

-  NoSQL
    - Big Data 저장/활용 시
    - 반정형 or 비정형 데이터 저장/활용 시
    - High-Availability(HA) 서비스 사용 시 (몇 개의 서버가 다운돼도, 다른 서버에 데이터 복재가 존재하므로 비상시에도 사라지지 않음)
</details>

<br>

**출처**

[1](https://khj93.tistory.com/entry/Database-RDBMS%EC%99%80-NOSQL-%EC%B0%A8%EC%9D%B4%EC%A0%90)

[2](https://universitytomorrow.com/26)

[3](https://beelee.tistory.com/35)

[4](https://www.educba.com/rdbms-vs-nosql/)

---

### 인덱스

- = 책의 목차와 같은 기능
- 데이터들이 정렬되어 있다는 특징 덕분에, 조건 검색 영역에서 용이
- Select문, 특히 조건 검색 Where절에서 발생하는 속도 저하 문제 해결책 중 하나

<details>
<summary>💡 index를 사용하면 좋은 경우</summary>
  
  1. 규모가 큰 테이블
  2. 삽입(INSERT), 수정(UPDATE), 삭제(DELETE) 작업이 자주 발생하지 않는 컬럼
  3. WHERE나 ORDER BY, JOIN 등이 자주 사용되는 컬럼
  4. 데이터의 중복도가 낮은 컬럼

</details>

<br>

1. **데이터베이스에서 index를 만들면 내부적으로 어떤 동작이 이루어지는지 설명해주시고 장단점에 대해 설명해주세요.**
  - **index 동작 과정** (검색 속도 향상 원인)
  1. 특정 컬럼에 인덱스 생성 시, 해당 컬럼의 데이터들을 정렬 후 별도의 메모리 공간에 데이터의 물리적 주소와 함께 저장된다
  2. 쿼리문에 ‘인덱스 생성 컬럼을 Where 조건으로 거는 등’의 작업을 하면 옵티마이저에서 판단하여 생성된 인덱스를 탄다
  3. 인덱스에 저장되어 있는 데이터의 물리적 주소로 가서 데이터를 가져온다

  ![image](https://user-images.githubusercontent.com/90819869/155029469-d6c5fe9f-4ecc-4a88-9698-c3875cd2bb73.png)

  - 장점
      - 테이블 조회 속도 및 그에 따른 성능 향상
      - Select 외에도 `Update`나 `Delete` 의 연산을 수행하려면 해당 대상을 조회해야 하기 때문에, 이와 관련된 성능 향상
  - 단점
      - 인덱스를 관리하기 위해 DB의 약 10%에 해당하는 저장공간 필요
      - 인덱스를 관리하기 위해 추가 작업 필요 (💡 index의 관리)
      - 인덱스를 잘못 사용할 경우 오히려 성능이 저하될 수 있음

<details>
<summary>💡 index의 관리</summary>

- INSERT: 새로운 데이터에 대한 인덱스를 추가
- DELETE: 삭제하는 데이터의 인덱스를 사용하지 않는다는 작업을 진행
- UPDATE: 기존의 인덱스를 사용하지 않음 처리하고, 갱신된 데이터에 대해 인덱스를 추가

</details>

<br>

2. **데이터베이스에서 index를 만들면 성능이 빨라지게 되는 이유를 설명해주세요.**
  a. 조건 검색 Where절의 효율성
      - 테이블을 만들고 안에 데이터가 쌓이게 되면 테이블의 레코드는 내부적으로 순서가 없이 뒤죽박죽으로 저장됩니다.
      - 인덱스 테이블은 데이터들이 정렬되어 저장되어 있기 때문에 해당 조건 (Where)에 맞는 데이터들을 빠르게 찾아낼 수 있습니다.
  b. 정렬 Order by절의 효율성
      - Order by는 정렬과 동시에 1차적으로 메모리에서 정렬이 이루어지고 메모리보다 큰 작업이 필요하다면 디스크 I/O도 추가적으로 발생되는 작업입니다.
      - 인덱스를 사용하면, 이미 정렬이 되어 있기 때문에 Order by에 의한 Sort 과정을 피하고 가져오기만 하면 됩니다.
  c. MIN, MAX 처리에 대한 효율성
      - 데이터가 정렬되어 있으므로, MIN값과 MAX값을 레코드의 시작값과 끝 값 한건씩만 가져오면 되기에 FULL TABE SCAN으로 테이블을 다 뒤져서 작업하는 것보다 훨씬 효율적으로 찾을 수 있습니다.

<br>

3. **hash index를 사용했을 때의 단점과 이유를 설명하세요.**
  - 데이터 정렬화가 되지 않는다
      - 데이터베이스에선 부등호(<, >) 연산이 자주 사용되는데, 해시 테이블은 위와 같이 등호(=) 연산에 최적화 되어있어 내부 데이터들이 정렬되어 있지 않다. 따라서, 특정 기준보다 크거나 작은 값을 빠른 시간 내에 찾을 수가 없다.

<details>
<summary>💡 Hash Table이란?</summary>

- key와 value를 한 쌍으로 데이터를 저장하는 자료구조
    - 해시 테이블 이용 시, 인덱스는 **(key, value) = (컬럼의 값, 데이터의 위치)**로 구현
    - key값을 이용해 대응되는 value값을 구하는 방식
- 해시 충돌이라는 변수가 존재하나, 평균적으로 **O(1)**의 매우 빠른 시간만에 원하는 데이터를 탐색할 수 있는 구조
- 동급비교(=)에서 효과적
- 정렬할 필요가 없으므로, 삽입/삭제가 빠름
- 메모리기반의 테이블에 주로 사용

</details>

<br>

4. **인덱스에 왜 해쉬 보다 B Tree를 쓰는가?**
  - 특정 데이터 값을 찾을 때, Hash보다 시간 복잡도에 대한 이점을 가진다 (💡 왜 B-Tree가 Hash보다 시간복잡도에서 유리한가요?)

  - B-Tree 인덱스는 항상 정렬된 상태를 유지하기 때문에, 기준값보다 크거나 작은 요소들을 항상 탐색할 수 있다

<details>
<summary>💡 왜 B-Tree가 Hash보다 시간복잡도에서 유리한가요?</summary>

- Hash는 탐색 시간이 가장 빠르지만, 이는 온전히 ‘단 하나의 데이터를 탐색하는 시간’에 국한된다. 예를 들어, 1,2,3,4,5가 저장되어 있는 해시 테이블에서 3이라는 데이터를 찾을 때에만 O(1)의 시간 복잡도를 가진다는 것이다.
- B-Tree는 아래 사진처럼 노드 하나에 여러 데이터가 저장될 수 있다. 각 노드 내 데이터들은 Hash와 달리 항상 정렬된 상태이다.
![image](https://user-images.githubusercontent.com/90819869/155030603-63afb521-5fba-4eba-af16-33160be2a042.png)
- 이처럼, B-Tree는 항상 좌, 우 자식노드 개수의 밸런스를 유지하므로 최악의 경우에도 무조건 탐색 시간이 O(logN)을 가지게 된다.

<br>

</details>

<details>
<summary>💡 B+Tree란?</summary>

기존의 B-Tree는 어느 한 데이터의 검색은 효율적이지만, 모든 데이터를 한 번 순회하는 데에는 트리의 모든 노드를 방문해야 하므로 비효율적이다. 이러한 B-Tree의 단점을 개선시킨 자료구조가 B+Tree이다.

- leaf node에만 데이터를 저장하고, leaf node가 아닌 node에서는 자식 포인터만 저장한다.
- leaf node끼리는 Linked list로 연결되어있다.
- B+Tree에서는 반드시 leaf node에만 데이터가 저장되기 때문에 중간 node에서 key를 올바르게 찾아가기 위해서 key가 중복될 수 있다.

</details>

<br>

**출처**

[1](https://mangkyu.tistory.com/96)

[2](https://coding-factory.tistory.com/746)

[3](https://rebro.kr/167)

[4](https://helloinyong.tistory.com/296)

[4](https://jungwoong.tistory.com/34)

[추가 인덱스 개념](https://ssoonidev.tistory.com/12)

---

### 트랜잭션

- 데이터베이스를 대상으로 수행하는 일련의 연산(CRUD)들로 이뤄진 하나의 작업 단위를 의미
  - 예를 들어, 고객이 온라인 주문을 시도했다고 상상해 보자.
  - **`Read`**: 먼저 데이터베이스에서 해당 고객의 정보가 이미 존재하는지 확인해야 한다.
  - **`Update`**: 만약 존재한다면 해당 고객의 주문 이력 정보를 수정해주고,
  - **`Create`**: 그렇지 않다면 해당 고객의 정보를 새로 생성해줘야 한다. 그러고 나서 해당 고객에 연결된 주문의 정보를 새로 생성해주면 이 과정은 끝이 난다.
  - 이러한 연산들은 `'온라인 주문 처리'`라는 하나의 논리적 기능을 수행하기 위한 것들임을 알 수 있고, 따라서 개발자는 이러한 연산들을 묶어서 하나의 트랜잭션으로 정의하게 된다.
- 트랜잭션의 5가지 상태

  ![image](https://user-images.githubusercontent.com/90819869/155031742-2ac25660-eb39-46e6-b44c-a17fb3c88234.png)


<br>

1. **트랜잭션을 사용할 때의 장점은 무엇인가요?**
  - 하나의 트랜잭션으로 정의되는 일련의 연산들은 하나라도 실패하면 전부 다 실패한 것과 같이 처리된다. 따라서 중간 연산까지만 수행이 되어 데이터들의 상태가 모순이 생기는 일은 발생하지 않는다.
  - 즉, 트랜잭션을 정의하는 본질적인 목적은, **모순이 없고 신뢰할 수 있는 안전한 데이터들을 구축하는 것**이다.

<br>

2. **트랜잭션의 특성에 대해 설명해주세요(ACID)**
  - Atomicity(원자성)
    - 트랜잭션의 연산들은 전체가 처리되거나 처리되지 않아야 한다(All or Nothing).
      - 일부 연산만 성공하는 것은 불가능하며, 하나라도 실패하는 경우에는 전부 다 실패한 것처럼 처리한다.
      - 예: 내 통장에서 돈이 빠져나갔다면 반드시 친구에게 송금도 완료가 되었어야 한다.
  -  Consistency(일관성)
    - 트랜잭션 실행이 성공적으로 이뤄지면 언제나 모순 없이 일관성 있는 데이터 상태를 유지해야 한다.
      - 예: 송금이 완료된 후에도 내 통장과 친구 통장의 잔고 합은 반드시 동일해야 한다.
  - Isolation(고립성)
    - 트랜잭션 실행 중에는 또 다른 트랜잭션이 접근할 수 없다.
      - 예: 어떤 트랜잭션이 내 통장에 대한 연산을 수행하고 있다면, 이 트랜잭션이 완료될 때까지 다른 트랜잭션은 내 통장에 대한 참조가 불가능하다.
  - Durability(지속성)
    - 완료된 트랜잭션의 결과는 영구적으로 데이터베이스에 저장된다.
    - 시스템에 어떠한 문제가 생기더라도 복구가 가능하도록 해야 한다.

<br>

3. **트랜잭션 격리 수준(Transaction Isolation Levels)에 대해서 설명해주세요.**

<br>

4. **잠금 타임아웃과 교착 상태가 발생하는 이유에 대해서 설명해주세요.**
  - 잠금 타임아웃
      - 작업 중인 트랜잭션에 다른 트랜잭션이 접근하여 작업을 시도할 때, 작업 중인 트랜잭션이 commit/rollback할 때까지 대기 시간이 발생하는데,  이 시간이 길어지는 경우 발생하게 됩니다.
  - 교착 상태
      - 프로세스가 자원을 얻지 못해 다음 처리를 하지 못하는 상태로, 시스템적으로 **한정된 자원**을 여러 곳에서 사용하려고 할 때 발생합니다.

<br>

5. **트랜잭션 Rollback은 어떤 경우에 하나요?**
  - 트랜잭션의 연산들을 수행하는 과정에서 오류가 발생하여 데이터베이스의 일관성이 깨졌을 때, 해당 트랜잭션의 모든 연산들을 취소함으로써 원자성을 확보해야 되는 경우
  - 이후 트랜잭션을 다시 시작할 수도 있고, 아예 종료할 수도 있다.

<details>
<summary>💡 Commit 연산과 Rollback 연산</summary>

1. **Commit 연산**

    ![image](https://user-images.githubusercontent.com/90819869/155031258-e97d9c52-d720-45e4-98af-45015c8065f3.png)

    - 트랜잭션이 성공적으로 수행되었을 선언(작업 완료)
    - commit 연산이 실행된 후에야 트랜잭션의 수행 결과가 데이터베이스에 반영되어 데이터베이스가 일관된 상태를 지속적으로 유지
    - commit 연산의 실행을 통해 트랜잭션의 수행이 성공적으로 완료되었음을 선언하고 결과를 최종 데이터베이스에 반영

2. **Rollback 연산**

    ![image](https://user-images.githubusercontent.com/90819869/155031283-6f5f8ceb-2a34-4f3d-8dea-0f046a3f3ecd.png)

    - 트랜잭션이 수행을 실패했음을 선언(작업 취소)
    - rollback 연산이 실행되면 트랜잭션이 지금까지 실행한 연산의 결과가 취소되고 트랜잭션이 수행되기 전의 상태로 다시 돌아감
    - 트랜잭션이 수행되는 도중 일부 연산이 처리되지 못한 상황에서는, rollback 연산을 실행하여 트랜잭션의 수행이 실패했음을 선언하고, 모순되지 않도록 데이터베이스를 트랜잭션 수행 전의 일관된 상태로 되돌려야 함

</details>

<br>

**출처**

[1, 2](https://it-eldorado.tistory.com/65)

[4](https://velog.io/@mooh2jj/%EA%B5%90%EC%B0%A9%EC%83%81%ED%83%9CDeadlock%EC%9D%B4%EB%9E%80)

[5](https://brunch.co.kr/@skeks463/27)

---

### JPA(Java Persistence API)

1. **ORM이란?**
  - 객체와 DB의 테이블이 매핑을 이루는 것. 즉, 객체가 테이블이 되도록 매핑 시켜주는 것
  - JPA, Hibernate, Mybatis 등

<br>

2. **JPA, Hibernate 그리고 Spring Data JPA 각각에 대해서 설명해주세요.**
  - **JPA**
    - 자바 ORM 기술에 대한 표준 명세로, `JAVA`에서 제공하는 API
    - Java 클래스와 RDBMS 간의 다리 역할

<details>
<summary>💡 장/단점</summary>

- **장점**
  1. 개발이 편리함
    - 기본적인 CRUD용 SQL을 직접 작성할 필요 X
  2. 데이터베이스에 독립적 개발 가능
    - JPA는 데이터베이스에 종속적이지 않으므로, 데이터베이스가 변경되더라도 해당 데이터베이스에 맞는 쿼리를 생성
  3. 유지보수가 쉬움
    - 테이블 변경 시 JPA의 엔티티만 수정 가능

- **단점**
  1. 학습이 어려움
  2. 특정 데이터베이스의 함수를 사용하지 못함
  3. 테이블은 객체지향 설계가 필요

</details>

  - **Hibernate**
    - JPA 구현체의 한 종류
    - JPA가 DB와 자바 객체를 매핑하기 위한 인터페이스(API)를 제공하면, Hibernate는 이 인터페이스를 구현한 것
  - **Spring Data JPA**
    - JPA를 쉽게 사용하기 위해 스프링에서 제공하고 있는 프레임워크
    - Spring Data JPA의 `Repository`의 구현에서 JPA를 사용

  | 구분 | 예시 |
  | --- | --- |
  | JPA | Java의 Interface |
  | Hibernate | Interface를 구현한 Class |
  | Spring Data JPA | JPA에게 Repository라는 인터페이스 제공 |

<br>

3. **데이터 정합성에 대해서 설명해주세요. JPA에서 이것들을 어떻게 처리하는가요?**
  - 데이터 값이 서로 모순이 없이 일관되게 일치한다는 의미
  - 예를 들어, 중복 데이터를 많이 사용하면 데이터 값이 서로 달라지는 경우가 발생하는데, 이를 ‘정합성이 깨졌다(=데이터가 일치하지 않는다)’라고 합니다.
  - JPA에서는 ‘Entity’라는 Java 객체(Java Bean)의 값이 변경되면 데이터베이스에 반영되는데, 이를 통해 데이터 정합성이 유지되는 건 아닐지...? 🤔

<br>

4. **DB Lock에 대해서 설명해주세요. JPA에서 이것들을 어떻게 처리하는가요?**
  - 트랜잭션 처리의 순차성을 보장하기 위한 방법
    - 하나의 트랜잭션이 완벽하게 끝날 때까지 다른 요청을 막음으로써, 여러 유저가 동시에 접근하더라도 1명씩 요청이 처리되도록 한다. (예: 수강신청)
  - **종류**
    - **공유(Shared or Read) Lock**
      - 데이터를 읽을 때 사용
      - 공유 Lock은 공유 Lock 끼리는 동시에 접근이 가능해서, 여러 사용사가 동시에 하나의 데이터를 읽는 것이 가능
      - 베타 Lock의 접근은 불가능
    - **베타(Exclusive or Write) Lock**
      - 데이터를 변경할 때 사용 (트랜잭션 완료 시까지 유지)
      - Lock이 해제될 때까지 다른 트랜잭션(읽기 포함)은 해당 리소스에 접근할 수 없음
      - 다른 트랜잭션이 수행되고 있는 데이터에 접근하여 Lock을 걸 수 없음
  - **Lock 설정 레벨**
      - **데이터베이스**
        - 전체 데이터베이스를 기준으로 Lock
        - DB 전체에 영향이 있는 DB 업데이트와 같은 작업에서만 사용
      - 파일 (실제 데이터[테이블, row 등]가 쓰여지는 물리적인 저장소)
        - 데이터베이스 파일을 기준으로 Lock
        - 파일 전체 백업 시 사용
      - **테이블 = DDL Lock**
        - 테이블 기준으로 Lock
        - 전체 테이블의 대한 데이터 변경이 있을 경우 사용
        - DDL(create, alter, drop 등) 구문과 함께 사용
      - 페이지와 블럭
        - 파일을 구성하는 페이지와 블록을 기준으로 Lock
      - 컬럼(Column)
        - 컬럼을 기준으로 Lock
      - **행(Row)**
        - 1개의 행(Row)를 기준으로 Lock
        - 가장 일반적으로 사용

<br>

5. **JPA는 로그 기법에 대해 어떻게 처리하는가?**

<br>

6. **JPA는 트랜잭션 Lock에 대해 어떻게 처리하는가?**

<br>

**출처**

[1, 2](https://velog.io/@adam2/JPA%EB%8A%94-%EB%8F%84%EB%8D%B0%EC%B2%B4-%EB%AD%98%EA%B9%8C-orm-%EC%98%81%EC%86%8D%EC%84%B1-hibernate-spring-data-jpa)

[2](https://suhwan.dev/2019/02/24/jpa-vs-hibernate-vs-spring-data-jpa/)

[3](https://donglnemo.tistory.com/171)

[3](https://dejavuhyo.github.io/posts/difference-jdbc-mybatis-jpa-spring-data-jpa/#3-jpajava-persistent-api)

[4](https://centbin-dev.tistory.com/40)

[4](https://sabarada.tistory.com/121)

---

### QueryDSL을 사용하는 이유와 JPQL과 차이점에 대해서 설명해주세요.

[QueryDSL](https://tecoble.techcourse.co.kr/post/2021-08-08-basic-querydsl/)

[JPQL](https://victorydntmd.tistory.com/205?category=795879)

[JPQL vs QueryDSL 간단 비교](https://devkingdom.tistory.com/242)

---

### 정규화에 대해서 설명해주세요

1. **정규화(Nomalization)가 무엇인가요? 비정규화(Denormalization)는 무엇이고, 언제 시행하게 되는지 설명해주세요.**
  - **정규화(Normalization)**
    - 이상현상이 존재하는 테이블을 분해하여 여러 개의 테이블을 생성하는 과정
    - 이 과정을 통해, 데이터를 보다 효율적으로 저장하고, 테이블 간 데이터 중복을 방지할 수 있고, 중복된 데이터를 허용하지 않음으로써 무결성을 유지하고, DB의 저장 용량을 줄일 수 있습니다.
    - 테이블이 분해되는 정도에 따라 정규화 단계가 나눠진다.

      1. **제 1 정규화**
          - 테이블의 모든 컬럼이 원자값(하나의 값)을 갖도록 분해

          ![image](https://user-images.githubusercontent.com/90819869/155033203-8322a410-9069-456d-92bf-770d9ebeab30.png)

      2. **제 2 정규화**
          - 제1 정규형을 만족하고, 완전 함수 종속(기본키의 부분집합이 결정자가 되어선 안됨을 의미)을 만족하도록 분해

          ![image](https://user-images.githubusercontent.com/90819869/155033220-6a4cfdd9-b210-4f0e-ad0b-df89a2273a8a.png)

          - 기본키(학생번호, 강좌이름) 중 강좌이름이 강의실을 결정하는 결정자이므로, 별도의 테이블로 분해한다

          ![image](https://user-images.githubusercontent.com/90819869/155033237-e63c9a2b-f540-4d2f-bafa-dbdd84c006f6.png)

      3. **제 3 정규화**
          - 제2 정규형을 만족하고, 이행적 종속(A→B, B→C = A→C)을 없애도록 분해
          - 각 속성들을 독립적으로 만드는 것이 아니라, 서로 참조가 가능하도록 분해

          ![image](https://user-images.githubusercontent.com/90819869/155033261-a24c0ab4-9e08-4922-8ffa-b5f03d787a1e.png)

          - 예를 들어, 이행적 종속을 따를 경우 학생번호→수강료가 되어버려서 강좌 변경 시에도 수강료가 변경되지 않는다. 이를 방지하기 위해, (학생번호, 강좌이름)과 (강좌이름, 수강료) 테이블로 분해한다

          ![image](https://user-images.githubusercontent.com/90819869/155033279-51601cbf-4b3b-40af-8d41-935613d0dd07.png)

      4. **BCNF 정규화**
          - 제 3 정규형을 만족하고, 모든 결정자가 후보키가 되도록 분해

          ![image](https://user-images.githubusercontent.com/90819869/155033306-f9bc71a8-818d-440f-a54b-459e3fba0cc9.png)

          - 기본키(학생번호, 특강이름)는 교수를 결정하는데, 교수 또한 특강이름을 결정하는 결정자이다.
          - 문제는, 교수가 결정자이지만 후보키는 아니라는 점이다. 따라서, 모든 결정자가 후보키가 될 수 있도록 분해한다.

          ![image](https://user-images.githubusercontent.com/90819869/155033324-102af95e-0b8e-4d07-86b3-0a4e6a378461.png)

<br>

  - **비정규화(Denomalization)**
    - 하나 이상의 테이블에 데이터를 중복해 배치하는 최적화 기법
      - 시스템의 성능 향상, 개발 및 운영의 편의성 등을 위해 정규화된 데이터 모델을 통합, 중복, 분리하는 과정으로, **의도적으로 정규화 원칙을 위배하는 것**

<details>
<summary>💡 언제 사용되나요?</summary>

- 디스크 I/O 량이 많아서 조회 시 성능이 저하될 때
- 테이블끼리의 경로가 너무 멀어 조인으로 인한 성능 저하가 예상될 때
- 칼럼을 계산하여 조회할 때 성능이 저하될 것이 예상될 때
- (일반적으로) 조회에 대한 처리 성능이 중요하다고 판단될 때

</details>

<br>

**출처**

[1_a](https://mangkyu.tistory.com/28)

[1_a](https://mangkyu.tistory.com/110)

[1_b](https://owlyr.tistory.com/20#113a77b2-e481-43f8-a1b3-b31f767e9803)

[1_b](https://velog.io/@bsjp400/Database-DB-%EC%A0%95%EA%B7%9C%ED%99%94-%EB%B9%84%EC%A0%95%EA%B7%9C%ED%99%94%EB%9E%80)

---

### Elastic Search

1. **Elastic Search에 대해서 간단히 설명해주세요.**

<br>

2. **Elastic Search의 인덱스구조와 RDBMS의 인덱스 구조의 차이에 대해 설명해주세요.**
  1. 색인과 역색인

<br>

3. **Elastic Search의 키워드 검색과 RDBMS의 LIKE 검색의 차이에 대해 설명해주세요.**

<br>

**출처**

[1](https://choseongho93.tistory.com/231)

[1, 2](https://jaemunbro.medium.com/elastic-search-%EA%B8%B0%EC%B4%88-%EC%8A%A4%ED%84%B0%EB%94%94-ff01870094f0)

[2](https://stackoverflow.com/questions/34539476/what-is-the-difference-between-an-elastic-search-index-and-an-index-in-a-relatio)

[3](https://velog.io/@jakeseo_me/%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-2-DB%EB%A7%8C-%EC%9E%88%EC%9C%BC%EB%A9%B4-%EB%90%98%EB%8A%94%EB%8D%B0-%EC%99%9C-%EA%B5%B3%EC%9D%B4-%EA%B2%80%EC%83%89%EC%97%94%EC%A7%84)

[3](https://12teamtoday.tistory.com/35)

---

### SQL

1. **A라는 테이블이 존재할 때, 새로운 속성(Column)을 추가한다고 할때, 모든 행(row)에 Default값을 넣어주고 싶을때, 어떤 쿼리문을 작성해야할까요?**

  ```sql
  # 구문
  ALTER TABLE {TABLENAME} ADD {COLUMNNAME} {TYPE} {NULL|NOT NULL} CONSTRAINT {CONSTRAINT_NAME} DEFAULT {DEFAULT_VALUE} WITH VALUES

  # 적용
  ALTER TABLE A ADD col1 varchar(10) NULL --또는 NOT NULL
  CONSTRAINT df_col1 -- 이름을 생략하면 자동으로 생성
  DEFAULT 'default' -- default 값 지정 옵션
  WITH VALUES -- 기존에 입력된 데이터에 default 값을 업데이트 하고자 하는 경우
  ```

<br>

**출처**

[1](https://tipntech.tistory.com/16)
