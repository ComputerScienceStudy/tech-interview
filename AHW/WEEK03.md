# [3주차 면접 스터디] DB 정리

### 목차

#### DB
- [RDBMS vs NoSQL](https://github.com/ComputerScienceStudy/tech-interview/blob/main/AHW/WEEK03.md#rdbms-vs-nosql%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%84%A4%EB%AA%85%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94)

- [인덱스(Index)](https://github.com/ComputerScienceStudy/tech-interview/blob/main/AHW/WEEK03.md#%EC%9D%B8%EB%8D%B1%EC%8A%A4)

- [트랜젝션](https://github.com/ComputerScienceStudy/tech-interview/blob/main/AHW/WEEK03.md#%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98)

- [JPA](https://github.com/ComputerScienceStudy/tech-interview/blob/main/AHW/WEEK03.md#jpajava-persistence-api)

- [정규화(Normalization) vs 비정규화(Denormalization)](https://github.com/ComputerScienceStudy/tech-interview/blob/main/AHW/WEEK03.md#%EC%A0%95%EA%B7%9C%ED%99%94%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%84%A4%EB%AA%85%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94)

- [SQL](https://github.com/ComputerScienceStudy/tech-interview/blob/main/AHW/WEEK03.md#sql)

#### WEB
- [쿠키(Cookie)와 세션(Session)](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#%EC%BF%A0%ED%82%A4cookie%EC%99%80-%EC%84%B8%EC%85%98session)

- [세션 기반 인증방식 vs 토큰 기반 인증방식](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#%EC%84%B8%EC%85%98-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D%EB%B0%A9%EC%8B%9D-vs-%ED%86%A0%ED%81%B0-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D%EB%B0%A9%EC%8B%9D)

- [JWT](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#jwtjson-web-token)

- [Web Server와 WAS](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#%EC%9B%B9-%EC%84%9C%EB%B2%84%EC%99%80-was%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)

- [SQL Injection](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#%EC%9B%B9-%EA%B3%B5%EA%B2%A9-%ED%8C%A8%ED%84%B4-%EB%B0%8F-%EB%B0%A9%EC%96%B4-%EB%B0%A9%EB%B2%95)

- [RESTful 개념](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#restful%EC%9D%98-%EA%B0%9C%EB%85%90)

#### NETWORK
- [OSI 7계층 vs TCP/IP 4계층](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#osi-7%EA%B3%84%EC%B8%B5)

- [DNS란?](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#dns%EB%9E%80)

- [HTTP와 HTTPS](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#dns%EB%9E%80)

- [TCP vs UDP](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#tcp%EC%99%80-udp)

- [웹 브라우저 요청 흐름](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#%EC%9B%B9-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%97%90%EC%84%9C-uri%EC%97%90-googlecom%EC%9D%84-%EC%B3%A4%EC%9D%84-%EB%95%8C-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-%EC%9D%BC%EB%93%A4%EC%9D%84-%EC%84%A4%EB%AA%85%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94)

- [서버가 웹브라우저를 통해 이미지를 요청받아 출력하는 과정](https://github.com/ComputerScienceStudy/tech-interview/edit/main/AHW/WEEK03.md#%EC%82%AC%EC%9A%A9%EC%9E%90%EA%B0%80-%EC%9B%B9%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EB%A5%BC-%ED%86%B5%ED%95%B4-%EC%84%9C%EB%B2%84%EC%97%90-%EC%9D%B4%EB%AF%B8%EC%A7%80%EB%A5%BC-%EC%9A%94%EC%B2%AD%ED%95%B4%EC%84%9C-%EC%82%AC%EC%9A%A9%EC%9E%90%EC%97%90%EA%B2%8C-%EB%B3%B4%EC%97%AC%EC%A3%BC%EA%B8%B0%EA%B9%8C%EC%A7%80-%EA%B3%BC%EC%A0%95%EC%9D%84-%EC%84%A4%EB%AA%85%ED%95%98%EC%84%B8%EC%9A%94)

---
## DB
----

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

  - 조건 검색 Where절의 효율성
    - 테이블을 만들고 안에 데이터가 쌓이게 되면 테이블의 레코드는 내부적으로 순서가 없이 뒤죽박죽으로 저장됩니다.
    - 인덱스 테이블은 데이터들이 정렬되어 저장되어 있기 때문에 해당 조건 (Where)에 맞는 데이터들을 빠르게 찾아낼 수 있습니다.
  - 정렬 Order by절의 효율성
    - Order by는 정렬과 동시에 1차적으로 메모리에서 정렬이 이루어지고 메모리보다 큰 작업이 필요하다면 디스크 I/O도 추가적으로 발생되는 작업입니다.
    - 인덱스를 사용하면, 이미 정렬이 되어 있기 때문에 Order by에 의한 Sort 과정을 피하고 가져오기만 하면 됩니다.
  - MIN, MAX 처리에 대한 효율성
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

---
## WEB
---

### 쿠키(Cookie)와 세션(Session)
**- 쿠키(Cookie)**
  - 클라이언트(브라우저) 로컬에 저장되는 키와 값이 들어있는 파일입니다
  - 사용자 인증이 유효한 시간을 명시할 수 있으며, 유효 시간이 정해지면 브라우저가 종료되어도 인증이 유지된다
  - 클라이언트의 상태 정보를 로컬에 저장했다가 참조합니다.
  - 즉, 자동완성이나, 팝업 일주일간 보지 않기 등 사용자의 편의를 위하는 것이지만 지워져도 되고, 조작되거나 가로채이더라도 큰 지장이 없는 수준의 정보들을 저장하는데 사용됩니다.

**- 세션(Session)**
  - 웹 브라우저를 통해 서버에 접속한 이후부터 브라우저를 종료할 때까지 인증상태를 유지합니다.
  - 사용자나 다른 누군가에게 노출되면 안되는 중요한 정보들은 세션으로 서버안에서 다뤄집니다.
  - 사용자에 대한 정보를 서버에 두기 때문에 쿠키보다 보안에 좋지만, 사용자가 많아질수록 서버 메모리를 많이 차지하게 됩니다.
    - 즉, 동접자 수가 많은 웹 사이트인 경우 서버에 과부하를 주게 되므로 성능 저하의 요인이 됩니다.

  <details>
   <summary>💡 세션 ID란?</summary>
   클라이언트가 Request를 보내면, 해당 서버의 엔진이 클라이언트에게 부여하는 유일한 ID 
  </details>

<br>

**1. 쿠키와 세션의 필요성**
   - HTTP 프로토콜의 특징이자 약점을 보완하기 위해서 사용됩니다.
   - HTTP 프로토콜의 약점은 모든 요청 간 의존관계가 없기 때문에, 현재 접속한 사용자가 이전에 접속했던 사용자와 같은 사용자인지 아닌지 알 수 있는 방법이 없다는 것.
   - 따라서, 통신할 때마다 새로 연결하기 때문에 클라이언트는 매 요청마다 인증을 해야 한다는 단점이 있습니다.
   - 즉, **이전 요청과 현재 요청이 같은 사용자의 요청인지 알기 위해 상태를 유지**하는 데에 쿠키와 세션이 필요합니다.

<br>

**2. 동작방식**
   1. 쿠키(Cookie)
      ![img_2.png](img_2.png)
      1. 클라이언트가 서버에 페이지를 요청
      2. 서버에서 쿠키를 생성
      3. HTTP 헤더(Set-Cookie)에 쿠키를 포함시켜 응답 `Set-Cookie: user=hwon0720`
      4. 전달받은 쿠키는 웹브라우저에서 관리하고 있다가, 다음 요청 때 쿠키를 HTTP 헤더에 넣어서 전송 `cookie: user=hwon0720`
      5. 서버에서는 쿠키 정보를 읽어 이전 상태 정보를 확인한 후 응답

   2. 세션(Session)
      ![img_3.png](img_3.png)
      1. 클라이언트가 서버에 접속 시(login), 서버로부터 Session ID를 발급 받음 
      2. 서버가 응답할 때 HTTP 헤더(Set-Cookie)에 Session ID를 포함해서 전송하고, 쿠키에 Session ID(JSESSIONID)를 저장합니다.
         `Set−Cookie: JSESSIONID=xslei13f`
      3. 웹브라우저(클라이언트)는 이후 웹브라우저를 닫기까지 다음 요청 때 부여된 Session ID가 담겨있는 쿠키를 HTTP 헤더에 넣어서 전송
         `Cookie: JSESSONID=xslei13f`
      4. 서버는 세션 ID를 확인하고, 해당 세션에 관련된 정보를 확인한 후 응답

<br>

**3. 쿠키와 세션은 언제 사용하나요?**
   1. 쿠키(Cookie)
      1. 방문 사이트에서 로그인 시, 아이디 & 비밀번호 저장 or 로그인 상태 유지
      2. 쇼핑몰의 장바구니 기능
      3. 팝업 "일주일 간 다시 보지 않기"
      4. 최근 검색한 상품들 광고에서 추천

   2. 세션(Session)
      1. 로그인 정보 유지
         - 화면이 이동해도 로그인이 풀리지 않고 로그아웃하기 전까지 유지

<details>
<summary>💡 쿠키와 세션 비교하기</summary>

|구분|쿠키|세션|
|---|---|---|
|저장위치|**클라이언트**|**서버**|
|저장형식|text|Object|
|리소스|클라이언트의 리소스|서버의 리소스|
|용량제한|20개/도메인, 4KB/쿠키|제한 없음|
|만료시점|쿠키 저장 시 설정 가능|브라우저 종료 시|
|속도|**세션보다 빠름**|느림(서버의 처리가 필요하기 때문)|
|보안성|낮음|**쿠키보다 높음**|
- 리소스
  - `세션`은 서버에 저장되고 서버자원을 사용하기 때문에, 사용자가 많을 경우 소모되는 자원이 상당해서 서버의 메모리를 많이 차지하고 속도가 느려질 수 있습니다.
  - 따라서, `세션`이 `쿠키`에 비해 보안도가 높은 편임에도 불구하고, `쿠키`를 사용하는 일이 많습니다.
- 보안성
  - `쿠키`는 클라이언트 로컬에 저장되기 때문에 변질되거나 request에서 스니핑(엿보기)을 당할 우려가 있어서 보안에 취약하지만,
  - `세션`은 쿠키를 이용해서 session id만 저장하고 이를 구분해서 서버에서 처리하기 때문에 비교적 보안성이 좋습니다.

</details>

<br>

출처

[1](https://github.com/WeareSoft/tech-interview/blob/master/contents/network.md#%EC%BF%A0%ED%82%A4%EC%99%80-%EC%84%B8%EC%85%98)

[1, 2](https://interconnection.tistory.com/74)

[2](https://devuna.tistory.com/23)

---

### 세션 기반 인증방식 vs 토큰 기반 인증방식
1. **세션 기반 인증방식**
- 동작방식
  - 세션(Session)과 쿠키(Cookie) 사용
  - 서버 측에서 유저들의 정보를 관리
  - 클라이언트의 상태를 유지하는 `Stateful` 구조

  ![image](https://user-images.githubusercontent.com/90819869/155197033-f417536d-d161-4193-af8f-bdc25b8c60cd.png)
    1. 서버가 클라이언트(브라우저)에게 웹사이트를 제공합니다.
    2. 클라이언트가 웹사이트에 로그인합니다.
    3. 성공 시, 서버가 유지 세션을 만들고, 세션을 식별하기 위한 sessionId를 기준으로 **정보를 서버 메모리 상에 저장**한 후 클라이언트에게 sessionId를 전송합니다.
    4. 클라이언트는 모든 request에 cookie(sessionId)를 함께 전송합니다.
    5. 서버는 브라우저가 보낸 sessionId를 키로 서버 메모리에서 사용자의 session 정보를 식별하고 유효하다면, 원하는 응답을 제공해줍니다.

- 장점
  + 구현이 명확하다는 장점이 있다.
  + 서버에서 로그인 상태 확인이 편하다.
  + 상대적으로 안전하다.
    + 서버측에서 세션을 관리하기 때문에, 클라이언트 변조에 영향받거나 데이터가 손상될 우려가 없다.

- 단점
  - 유저들의 세션에 대한 정보를 서버 메모리에 저장하기 때문에, 메모리 사용량 증가에 대한 부담이 있다.
  - 멀티 디바이스 환경에서 로그인 시 신경써줘야할 부분들이 생긴다.
    - 사용자가 늘어나게 되면 더 많은 트래픽을 처리하기 위해 여러 프로세스를 돌리거나 컴퓨터를 추가하는 등 서버를 확장해야 한다.
  - 중앙 세션 관리 시스템(서버)에 장애가 발생할 경우, 시스템 전체의 문제가 된다.

<br>

2. **토큰 기반 인증방식**
- 동작방식
  - JWT 사용
  - 인증받은 사용자들에게 토큰을 발급하고, 서버에 요청을 할 때 헤더에 토큰을 함께 보내도록 하여 유효성 검사를 한다
  - 상태를 유지하지 않는 `Stateless` 구조

  ![image](https://user-images.githubusercontent.com/90819869/155197195-d50973fd-5f04-4717-8c22-3eed2d59928b.png)
    1. 서버가 클라이언트에게 웹사이트를 제공합니다.
    2. 클라이언트(유저)가 웹사이트에 로그인합니다.
    3. 서버에 세션을 이용해서 정보를 기록하는 대신, Token을 생성하여 발급합니다.
    4. **클라이언트가 발급된 Token을 저장** 후, 요청을 할 때 저장된 Token을 Header에 포함시켜 전송합니다.
    5. 서버는 요청 시 매번 전달받은 Header의 Token 정보를 검증(Verification)한 뒤, 해당 유저에 권한을 인가합니다.

- 장점
  + 클라이언트에 저장되기 때문에 서버의 메모리에 부담이 되지않으며 Scale 에 있어 대비책을 고려할 필요가 없다
  + 멀티 디바이스 환경에 대한 부담이 없다.

- 단점
  - 상대적으로 데이터가 손상될 위험이 크다.
  - Token 은 일반적으로 Session ID 보다 길다.
  - XSS 공격에 취약할 수 있어 가능한 민감한 정보는 포함시키지 않을 필요가 있다.

<details>
<summary>💡 크로스 사이트 스크립팅(Cross Site Scripting, XSS) 공격이란?</summary>

- 공격자가 상대방의 브라우저에 스크립트가 실행되도록 해 사용자의 세션을 가로채거나, 웹사이트를 변조하거나, 악의적 콘텐츠를 삽입하거나, 피싱 공격을 진행하는 것입니다.

</details>

<details>
<summary>💡 Refresh Token이란?</summary>

- 토큰 기반 인증의 단점을 보완하기 위한 방식으로, access 토큰이 만료되었을때 Refresh 토큰으로 서버에 새로운 access 토큰을 발급받을 수 있습니다.
  - 서버 데이터베이스에 Refresh Token이 저장되어 있을때 클라이언트가 블랙리스트에 포함되어 있다면, access 토큰을 발급해주는 것을 막을 수 있다.
  - Refresh Token으로 access 토큰이 만료되면 알아서 갱신한다.

</details>

<br>

출처

[1,2](https://jins-dev.tistory.com/entry/Session-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D%EA%B3%BC-Token-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D)
[1,2](https://mangkyu.tistory.com/55)
[1,2](https://velog.io/@jifrozen/%EC%84%B8%EC%85%98-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D-vs-%ED%86%A0%ED%81%B0-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9DJwt)

---

### JWT(JSON Web Token)
1. JWT 사용 이유 및 장단점 
   - 사용 이유
     - 기존의 Session과 Token을 기반으로 한 인증 방식은, 인증 과정에서 DB를 거쳐야만 합니다.
     - 하지만 JWT의 경우, 사용자 인증에 필요한 정보를 토큰 자체에 담고 있어서, 별도 저장소에 정보를 저장해둘 필요가 없습니다.
     - 토큰에 대한 기본 정보, 전달할 정보(예: 로그인 시스템에서의 유저 정보), 토큰이 검증됐음을 증명해주는 `signature`(토큰을 인코딩하거나 유효성 검증을 할 때 사용하는 고유한 암호화 코드) 등을 포함

   - 장점
     - 별도의 인증 저장소가 필요 없음
     - 쿠키를 전달하지 않아도 되므로, 쿠키를 사용함으로써 발생하는 취약점 해결
     - 트래픽에 대한 부담이 낮음
     - REST 서비스로 제공 가능 

   - 단점
     - 자가수용적(Self-contained)
       - 토큰 자체에 정보를 담고 있다는 점이 양날의 검이 될 수 있음
     - 토큰 길이
       - 토큰의 페이로드(Payload)에 3종류의 클레임을 저장하기 때문에, 정보가 많아질수록 토큰의 길이가 늘어나 네트워크에 부하를 줄 수 있음
     - Payload 인코딩
       - Payload를 탈취하여 디코딩하면 데이터를 볼 수 있음
       - JWE로 암호화하거나 Payload에 중요 데이터를 넣지 않아야 함
     - Stateless
       - 상태를 저장하지 않기 때문에 한번 만들어지면 제어가 불가능 (=토큰 임의 삭제 불가능)
       - 토큰을 임의로 삭제하는 것이 불가능하므로 토큰 만료 시간을 꼭 넣어줘야 함

<details>
<summary>💡 언제 사용되나요?</summary>

- **로그인**
  - 서버가 유저의 세션을 유지할 필요 없이, 유저가 보낸 토큰만 확인하면 되기 때문에, 서버의 자원을 아낄 수 있습니다.
- **정보교류**
  - 정보가 sign이 되어 있기 때문에 정보의 출처나 내용이 변경되지는 않았는지 검증할 수 있습니다.

</details>

<br>

출처

[1. JWT 사용 이유 및 장단점](https://gorokke.tistory.com/181)

---

### 웹 서버와 WAS의 차이점
1. **웹 서버(Web Server)**
   - 웹 브라우저 클라이언트로부터 HTTP 요청을 받아 **정적인 컨텐츠**(.html .jpeg .css 등)를 제공하는 컴퓨터 프로그램
   - Apache Server, Nginx 등
   ![image](https://user-images.githubusercontent.com/90819869/155197629-06da5aa3-7418-466d-9379-78eb0ca90eb9.png)

<br>

2. **WAS(Web Application Server)**
   - DB 조회나 다양한 로직 처리를 요구하는 **동적인 컨텐츠**를 제공하기 위해 만들어진 Application Server
   ![image](https://user-images.githubusercontent.com/90819869/155197657-213808df-5341-4445-91b4-9faf26c841ea.png)

<details>
<summary>💡 Web Server와 WAS를 구분하는 이유가 뭔가요?</summary>

- **Web Server가 필요한 이유**
  - Web Server를 통해 정적인 파일들을 Application Server까지 가지 않고, 앞에서 빠르게 처리해줄 수 있습니다.
  - 따라서, Web Server에서 정적 컨텐츠만 처리하도록 기능을 분배하여 서버의 부담을 줄일 수 있게 됩니다.
- **WAS가 필요한 이유**
  - 웹 페이지의 정적 컨텐츠와 동적 컨텐츠에 대한 유저의 요청을 Web Server가 제공하는 데에는 한계가 있습니다.
  - 따라서, WAS를 통해 요청에 맞는 데이터를 DB에서 가져와서 비즈니스 로직에 맞게 그때 그때 결과를 만들어서 제공함으로써 자원을 효율적으로 사용할 수 있게 됩니다.
- **정리**
  - 즉, 자원 이용의 효율성 및 장애 극복, 배포 및 유지보수의 편의성 을 위해 Web Server와 WAS를 분리하여 사용해주는 게 좋습니다.
    - Web Server를 WAS 앞에 두고 필요한 WAS들을 Web Server에 플러그인 형태로 설정하면 더욱 효율적인 분산 처리가 가능

</details>

<br>

출처

[1, 2. 웹 서버 vs WAS](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html)

---

### 웹 공격 패턴 및 방어 방법
1. **SQL Injection에 대해서 간단히 설명해주세요.**
- 코드 인젝션의 한 기법으로, 클라이언트의 입력값을 조작하여 서버의 데이터베이스를 공격할 수 있는 공격 방식
- 즉, 악의적인 사용자가 보안상의 취약점을 이용해, 임의의 SQL문을 주입하고 실행되게 하여 서버의 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위

<br>

출처

[1. SQL Injection 공격 및 방어 1](https://noirstar.tistory.com/264)

[1. SQL Injection 공격 및 방어 2](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=dktmrorl&logNo=222048311115)

---

### RESTful의 개념
1. **RESTful이란 무엇이며, 이것에 대해서 아는대로 설명해보세요.**
   - REST 아키텍처를 따르는 시스템을 지칭하는 용어입니다.
   - 목적
     1. 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
     2. 성능 향상보다는, 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높여주는 것

<details>
<summary>💡 REST란?</summary>

- HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 `CRUD Operation`을 적용하는 것
- CRUD Operation
  - Create: 생성(POST)
  - Read : 조회(GET)
  - Update : 수정(PUT)
  - Delete : 삭제(DELETE)
  - HEAD: header 정보 조회(HEAD)

</details>

<br>

출처

[1. RESTful이란?](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)

[2. REST API 설계 기본 규칙](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)

---

### Challenge
- 웹 사이트를 제작했는데 고해상도 이미지를 많이 사용하여 페이지 로딩 속도가 느립니다. 최적화 하는 방법에 대해서 모두 설명하세요.
- 브라운이 새로운 검색 엔진을 개발하려고 합니다. 어떻게 설계 및 개발 것인지 아는 지식을 모두 동원하여 설명하세요.

---
## NETWORK
---

### 웹 브라우저에서 URI에 `google.com`을 쳤을 때 발생하는 일들을 설명해주세요.
(DNS 서버, HTTP 프로토콜(80포트), HTTPS 프로토콜(443포트), DOM, IP, PORT 등의 용어 언급 필요)
- 웹 브라우저 요청 흐름
  1. DNS 서버를 조회해서 **IP와 PORT번호 조회**
  2. **HTTP 요청 메세지 생성**
     
     ![image](https://user-images.githubusercontent.com/90819869/155197845-d7793b5b-b60e-47a4-923d-b457d22ad2c2.png)
  3. HTTP 메세지를 SOCKET 라이브러리를 통해 OS계층인 **TCP/IP계층에 전달**
     - 이때 3-way handshake를 통해 서버와 연결을 확인하고 데이터를 전달한다
  4. TCP/IP 계층에서는 이전의 웹 브라우저에서 전달 받은 데이터를 기반으로 **TCP/IP 패킷 생성**
  5. 네트워크 인터페이스 계층을 거쳐 **서버로 전송**
  6. 서버는 전달 받은 데이터를 분석하고, **HTTP 응답 메세지 생성**
     
     ![image](https://user-images.githubusercontent.com/90819869/155197973-c7081287-a9c8-45a2-a17c-281df9e468d1.png)
  7. 서버도 위와 같은 방식으로 응답 패킷을 만들어서 **클라이언트에게 패킷 전달**
  8. 클라이언트는 응답 패킷을 분석하고, **웹 브라우저가 렌더링해서 화면에 출력**

<br>

[📚 참고자료](https://sic-dev.tistory.com/89)

---

### 사용자가 웹브라우저를 통해 서버에 이미지를 요청해서 사용자에게 보여주기까지 과정을 설명하세요.

![image](https://user-images.githubusercontent.com/90819869/155198005-07e23ba5-95ce-4e55-84b0-d00e0bb2f936.png)

- 예: 구글 홈페이지의 구글 로고 이미지
  1. 웹 브라우저가 https://www.google.com/images/google.png 로 이미지를 요청 해야한다는 것을 인지한다.
  2. 웹 브라우저는 URL을 이용해 서버의 ip를 추출한다.
  3. DNS 서버에 요청을 하게 되고 이 때 ip를 찾기위한 이름 해결 과정은 UDP 통신으로 이루어 진다.
  4. 이미지를 요청하기 위한 HTTP 메세지를 만든다.
  5. 메세지는 get메서드이고 /google.png를 요청하는 메세지이다.
  6. **웹브라우저는 서버와 TCP 3 Ways Handshaking 방식으로 커넥션을 맺는다.**
  7. **웹브라우저는 서버에 HTTP 요청을 보낸다.**
  8. 서버는 메세지를 받고 HTTP 메세지를 해석한다.
  9. get이라는 메서드이고 `/google.png`라는 파일을 요청 했다는 것을 인지한다.
  10. 서버는 해당 리소스가 있는지 찾는다.
  11. **서버는 클라이언트와 TCP 3 Ways Handshaking 방식으로 커넥션을 맺는다.**
  12. **서버는 클라이언트에 HTTP 응답을 보낸다.**

<br>

[📚 참고자료](https://krksap.tistory.com/1148)

---

### OSI 7계층
1. **OSI 7계층이 무엇인지 그 존재 이유에 대해서 설명해보세요.**
  - 네트워크에서 통신이 일어나는 과정을 7단계로 나눈 것
  - 상호 이질적인 네트워크간의 연결에서 호환성의 결여를 막기 위해 개발된 모형
  - OSI 7계층이 있음으로써, 통신이 일어나는 과정을 단계별로 파악할 수 있습니다.
  - 문제 발생 시, 효율적으로 해결이 가능합니다.
    - 7단계 중 특정한 곳에 이상이 생기면 다른 단계의 장비 및 소프트웨어를 건드리지 않고도 이상이 생긴 단계만 고칠 수 있습니다.

  ![image](https://user-images.githubusercontent.com/90819869/155205397-f3a0dd33-b0a0-4f19-ad87-237627e32620.png)
  1. 1계층 - 물리계층(Physical Layer)
      - 전기 데이터의 전송만을 담당 (통신 케이블, 리피터, 허브 등)
  2. 2계층 - 데이터 링크계층(DataLink Layer)
      - 정보의 오류와 흐름을 관리 (브리지, 스위치, 이더넷 등)
  3. 3계층 - 네트워크 계층(Network Layer)
      - 경로를 선택하고 주소를 정하고 경로에 따라 패킷을 전달 (라우터)
      - 라우팅, 흐름 제어, 세그멘테이션, 오류 제어, 인터네트워킹 등을 수행
      - `라우팅` : 데이터를 목적지까지 가장 안전하고 빠르게 전달 (중요 기능)
  4. 4계층 - 전송 계층(Transport Layer)
      - 데이터를 받으면 해당 데이터를 하나로 합쳐서 5계층으로 전달 (예: TCP)
      - 양 끝단(End to end)의 사용자들이 신뢰성있는 데이터를 주고 받을 수 있도록 하는 역할
      - `연결 기반(connection oriented)` : 전송 계층이 패킷들의 전송이 유효한지 확인하고 전송 실패한 패킷들을 다시 전송
  5. 5계층 -세션 계층(Session Layer) 
      - 데이터가 통신하기 위한 논리적인 연결(세션)을 담당
      - TCP/IP 세션을 생성 및 제거
      - 양 끝단의 응용 프로세스가 통신을 관리하기 위한 방법을 제공 (동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(Full Duplex) 등)
  6. 6계층 - 표현 계층(Presentation Layer)
      - 데이터 표현이 상이한 응용 프로세스의 독립성을 제공하고, 암호화
      - 코드 간의 번역 담당, MIME 인코딩이나 암호화 등을 수행
  7. 7계층 - 응용 계층(Application Layer)
      - 최종 목적지로서, 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행 (HTTP, FTP, SMTP, POP3, IMAP, Telnet 등의 프로토콜)

<br>

2. **TCP/IP 4계층에 대해 설명해보세요.**
  - OSI 참조 모델을 기반으로 상업적이고 실무적으로 이용될 수 있도록 단순화된 모형
  
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

<br>

3. **웹 서버 소프트웨어(Apache, Nginx)는 OSI 7계층 중 어디서 작동하는지 설명해보세요.**

4. **웹 서버 소프트웨어(Apache, Nginx)의 서버 간 라우팅 기능은 OSI 7계층 중 어디서 작동하는지 설명해보세요.**


출처

[1. OSI 7계층](https://pinelover.tistory.com/180)

[2. TCP/IP 4계층](https://togll.tistory.com/39)

---

### DNS란?
- `www.example.com` 과 같이 사람이 읽을 수 있는 이름을 `192.0.2.1`과 같은 숫자 IP 주소로 변환하여 컴퓨터가 서로 통신할 수 있도록 한다. 
- 인터넷의 DNS 시스템은 이름과 숫자 간의 매핑을 관리하여, 마치 **전화번호부**와 같은 기능을 한다.
- DNS 서버는 이름에 대한 요청을 IP 주소로 변환하여 최종 사용자가 도메인 이름을 웹 브라우저에 입력할 때 해당 사용자를 어떤 서버에 연결할 것인지를 제어한다. = `쿼리`
- **동작원리**

  ![image](https://user-images.githubusercontent.com/90819869/155198775-78f87882-58b0-4cfb-a122-dc5408c9f9ce.png)
  1. 웹 브라우저에 `www.example.com`을 입력하면, Local DNS에게 `"www.naver.com"`이라는 hostname에 대한 IP 주소를 요청한다.
    - Local DNS에 없으면 다른 DNS name 서버 정보(Root DNS 정보)를 받는다.
  2. Root DNS 서버에 `"www.example.com"`에 대해 요청한다.
  3. Root DNS 서버로 부터 "com 도메인"을 관리하는 TLD (Top-Level Domain) 이름 서버 정보를 전달 받는다.
  4. TLD에 `"www.example.com"`에 대해 요청한다.
  5. TLD에서 "name.com" 관리하는 DNS 정보를 전달한다.
  6. "example.com" 도메인을 관리하는 DNS 서버에 `"www.example.com"` 호스트네임에 대한 IP 주소를 요청한다.
  7. Local DNS 서버에게 `www.example.com`에 대한 IP 주소(예:222.122.195.6)를 응답 받는다.
  8. Local DNS는 `www.example.com`에 대한 IP 주소를 캐싱을 하고 IP 주소 정보를 전달한다.

<br>

출처

[1. DNS란?](https://ijbgo.tistory.com/27)

---

### HTTP
1. **HTTP의 역할**
- 하이퍼텍스트를 교환하기 위한 통신 규약으로, 인터넷에서 데이터를 주고기 위한 프로토콜
- 이 규약을 따름으로써, 모든 프로그램이 이 규약에 맞춰 개발되고 **서로 정보를 교환할 수 있습니다**.

<br>

2. **HTTP 프로토콜의 특징**
- Connectionless (비 연결 지향)
    - 클라이언트가 서버에 요청(Request)을 했을 때,그 요청에 맞는 응답(Response)을 보낸 후 연결을 끊는 처리방식
- Stateless (상태정보 유지 안함)
    - 연결을 끊는 순간 클라이언트와 서버의 통신은 끝나며 상태 정보를 유지하지 않는 서버 처리방식
- `80`번 포트 사용

<br>

3. **HTTPS에 대해서 설명하고 SSL Handshake에 대해서 설명해보세요.**
- HTTPS란?
    - 웹 통신 프로토콜인 HTTP의 보안이 강화된 버전의 프로토콜
    - 소켓 통신에서 일반 텍스트를 이용하는 대신, 웹 상에서 정보를 암호화하는 **SSL**이나 **TLS**(SSL에서 발전한 것) 프로토콜을 통해 세션 데이터를 암호화합니다.
        - 두 프로토콜을 통해 HTTPS는 기밀성(사생활 보호), 데이터 무결성, ID 및 디지털 인증서를 사용한 인증을 제공할 수 있게 됩니다.
    - `대칭키 암호화`와 `비대칭키 암호화`를 사용합니다.
        - 대칭키 암호화 : 클라이언트와 서버가 동일한 키를 사용해 암호화/복호화를 진행. 키가 노출되면 매우 위험하지만 연산 속도가 빠름
        - 비대칭키 암호화 : 1개의 쌍으로 구성된 공개키와 개인키를 사용해 암호화/복호화를 진행. 키가 노출되어도 비교적 안전하지만 연산 속도가 느림
    - `443`번 포트 사용

- SSL Handshake
    - 송신자와 수신자가 암호화된 데이터를 교환하기 위한 일련의 협상과정
        - 통신을 하는 브라우저와 웹 서버가 서로 암호화 통신을 시작할 수 있도록 신분을 확인하고, 필요한 정보를 클라이언트와 서버가 주고 받는 과정입니다.

    ![image](https://user-images.githubusercontent.com/90819869/155216519-58ced17d-884e-477a-9f8c-06b25767bd50.png)
    1. `클라이언트`가 서버에 접속 시도 (Client Hello)
    2. `서버`는 공개키가 담긴 SSL 인증서 등의 정보를 클라이언트에게 제공 (Server Hello)
    3. `클라이언트`(브라우저)는 서버의 SSL 인증서가 믿을만한지 확인
    4. `클라이언트`(브라우저)는 자신이 생성한 난수와 서버의 난수를 사용하여 premaster secret(암호화된 세션키) 생성
    5. `서버`는 사이트의 비밀키로, 브라우저가 보낸 premaster secret값을 복호화
    6. `서버`와 `클라이언트`는 SSL handshake를 종료, HTTPS 통신 시작

<details>
<summary>💡 cipher suite가 무엇인가요?</summary>

- 보안의 궁극적 목표를 달성하기 위해 사용하는 방식을 패키지의 형태로 묶어놓은 것을 의미합니다.
- 여기서 보안의 목표란 다음과 같습니다.
    - 안전한 키 교환
    - 전달 대상 인증
    - 암호화 알고리즘
    - 메시지 무결성 확인 알고리즘

</details>

<br>

4. **HTTP와 HTTPS의 차이를 설명하세요.**
- HTTP
    - 암호화가 되지 않은 평문 데이터를 전송하는 프로토콜
    - HTTP로 비밀번호나 주민등록번호 같이 보안이 필요한 정보들을 주고 받을 때, 제 3자가 정보를 조회할 수 있습니다.
    - 비연결형으로 웹 페이지를 보는 중 인터넷 연결이 끊겼다가 다시 연결되어도 페이지를 계속 볼 수 있습니다.
- HTTPS
    - 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 **HTTP에 데이터 암호화가 추가된 프로토콜**
    - 단, HTTP보다 비교적 속도가 느립니다.
    - 소켓(데이터를 주고 받는 경로) 자체에서 인증을 하기 때문에 인터넷 연결이 끊기면 소켓도 끊어져서 다시 HTTPS 인증하는 시간이 소요됩니다.

<br>

5. **HTTP 1.1 VS 2.0 VS 3.0**
- HTTP 1.1
    - Connection Keep-Alive (기존 연결에 대해서 handshake 생략가능)
    - 파이프라이닝 기법 도입 (이전 요청에 대한 응답이 완전히 전송되기 전에 다음 전송을 가능하게 하여 레이턴시를 낮춤) → HOLB(Head Of Line Blocking) 문제 발생
    - 언어, 인코딩 타입등을 포함한 컨텐츠 전송
    - 동일 IP 주소에 다른 도메인을 호스트하는 기능 가능 (HOST header)
    - 문제점 : HOLB, 무거운 Header 구조, RTT(Round Trip Time)

<details>
<summary>💡 HTTP 1.1 문제점의 원인?</summary>

1. HOLB
- HTTP 1.1에서 사용되는 `파이프라이닝`이라는 기술은 하나의 커넥션에서 한 번에 순차적인 여러 요청을 연속적으로 하고 그 순서에 맞춰 응답을 받는 방식으로 지연 시간을 줄이는 방법이다.
- 순차적으로 데이터를 요청하고 받아야 하다 보니 먼저 받은 요청이 끝나지 않으면 그 뒤에 있는 요청의 처리가 아무리 빨리 끝나도 먼저 온 요청이 끝날 때까지 기다려야 하는 문제가 발생했는데, 이를 HOL(Head Of Line) Blocking이라고 한다.
  
2. 무거운 Header
- 사용자가 방문한 웹페이지는 다수의 http 요청이 발생하게 되는데, 이 경우 매 요청 시마다 중복된 헤더값, domain에 설정된 cookie 정보들을 Header에 포함하여 전송하기 때문에 Header가 전송값보다 커지는 경우도 발생한다.

3. RTT
- RTT란 클라이언트가 보낸 요청을 서버가 처리한 후 다시 클라이언트로 응답해주는 사이클이다.
- TCP는 연결을 생성하기 위해 기본적으로 1 RTT가 필요하고, 여기에 TLS를 사용한 암호화까지 하려고 한다면 TLS의 자체 핸드쉐이크까지 더해져 총 3 RTT가 필요하다.
- TCP상에서 동작하는 HTTP의 특성상, Handshake 가 반복적으로 일어나고 또한 불필요한 RTT증가와 네트워크 지연을 초래하여 성능을 저하 시키게 된다.

</details>

- HTTP 2.0
    - Multiplexed Streams : 한 커넥션으로 동시에 여러 개의 메세지를 주고 받을 있으며, 응답은 순서에 상관없이 stream으로 주고 받습니다.
        - 하나의 스트림에서 문제가 발생한다고 해도 다른 스트림은 지킬 수 있게 되어 이런 문제에서 자유로울 수 있습니다.
    - Server Push : 클라이언트가 요청하지 않은 리소스를 Push 해주는 방법으로 클라이언트의 요청을 최소화 해서 성능 향상 → 성능 향상
    - Header Compression : Header의 중복값이 존재하는 경우, HPACK 압축방식을 이용하여 Header 정보를 압축 → HTTP 1.1의 무거운 Header 문제 개선
    - 단, 여전히 TCP를 이용하기 때문에 RTT로 인한 지연시간 및 HOLB 문제는 해결 X

<details>
<summary>💡 HPACK 압축 방식?</summary>

- Header에 중복값이 존재하는 경우 Static/Dynamic Header Table 개념을 사용하여 중복 Header를 검출하고 중복된 Header는 index값만 전송하고 중복되지 않은 Header정보의 값은 Huffman Encoding 기법으로 인코딩 처리 하여 전송하는 방식

</details>

<details>
<summary>💡 SPDY란?</summary>

![image](https://user-images.githubusercontent.com/90819869/155224672-98532538-b6cc-4d83-9a86-efb6fdac4d82.png)
  
- Latency 관점에서 HTTP를 고속화한 프로토콜
- PDY는 HTTP를 대치하는 프로토콜이 아니고 HTTP를 통한 전송을 재 정의하는 형태로 구현 되었다.
- SPDY는 실제로 HTTP/1.1에 비해 상당한 성능 향상과 효율성을 보여줬고 이는 HTTP/2 초안의 참고 규격이 되었다.

</details>

- HTTP 3.0
    - 기존의 HTTP/1, HTTP/2와는 다르게 **UDP 기반의 프로토콜**인 QUIC 을 사용하여 통신하는 프로토콜
    - TCP를 사용하지 않기 때문에 통신을 시작할 때 3 Way Handshake 과정 생략 → RTT 문제 개선 = 지연시간 단축
        - 연결 설정에 필요한 정보와 함께 데이터도 보내버리기 때문에 첫 연결 설정에 1 RTT만 소요 (기존 HTTP는 총 3 RTT 소요)
    - 클라이언트의 IP가 바뀌어도 연결이 유지됨
        - TCP의 경우 소스의 IP 주소와 포트, 연결 대상의 IP 주소와 포트로 연결을 식별하기 때문에 클라이언트의 IP가 바뀌는 상황이 발생하면 연결이 끊어져 버린다. 연결이 끊어졌으니 다시 연결을 생성하기 위해 결국 Handshake 과정을 다시 거쳐야한다는 것이고, 이 과정에서 다시 레이턴시가 발생한다.

<details>
<summary>💡 QUIC(Quick UDP Internet Connections)란?</summary>

![image](https://user-images.githubusercontent.com/90819869/155224804-72470786-4079-4e74-a813-3285bdd26bdc.png)
  
- UDP를 기반으로 TCP + TLS + HTTP 의 기능을 모두 구현하는 프로토콜
- HTTP/3의 기반 기술

</details>

<br>

6. **HTTP 응답코드**
- 상태 코드는 3자리 숫자로 만들어져 있으며, 첫번째 자리는 1에서 5까지 제공됩니다. 첫번째 자리가 4와 5인 경우는 정상적인 상황이 아니기 때문에 사이트 관리자가 즉시 알아야 하는 정보입니다.
    - 1xx(정보) : 요청을 받았으며 프로세스를 계속 진행합니다.
    - 2xx(성공) : 요청을 성공적으로 받았으며 인식했고 수용하였습니다.
    - 3xx(리다이렉션) : 요청 완료를 위해 추가 작업 조치가 필요합니다.
    - 4xx(클라이언트 오류) : 요청의 문법이 잘못되었거나 요청을 처리할 수 없습니다.
    - 5xx(서버 오류) : 서버가 명백히 유효한 요청에 대한 충족을 실패했습니다.

<br>

7. **HTTP Method - PUT과 PATCH의 차이**
- PUT
    - 리소스의 모든 것을 업데이트 합니다.
- PATCH
    - 리소스의 일부를 업데이트 합니다.
- 예를 들어, 한 사용자에 대해 여러 정보를 객체로 수집하여 서버로 보내는 경우
    - `PUT`은 보내지지 않은 정보에 대해서는 *null값으로 업데이트*하지만
    - `PATCH`는 *기존 데이터를 유지하는 방식*으로 대응한다.

<br>

출처

[1. HTTP의 역할](https://velog.io/@surim014/HTTP%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)

[2. HTTP 프로토콜의 특징](https://github.com/WeareSoft/tech-interview/blob/master/contents/network.md#%EC%BF%A0%ED%82%A4%EC%99%80-%EC%84%B8%EC%85%98)

[3. HTTPS란?](https://github.com/WeareSoft/tech-interview/blob/master/contents/network.md#http%EC%99%80-https)

[3. SSL Handshake란?](https://brunch.co.kr/@sangjinkang/38)

[4. HTTP vs HTTPS](https://mangkyu.tistory.com/98)

[5. HTTP 1.1 vs 2.0 vs 3.0](https://velog.io/@ziyoonee/HTTP1-%EB%B6%80%ED%84%B0-HTTP3-%EA%B9%8C%EC%A7%80-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0#http11)

[6. HTTP 응답코드](https://www.whatap.io/ko/blog/40/)

[7. PUT vs PATCH](https://velog.io/@dulcis-hortus/PUT%EA%B3%BC-PATCH%EC%9D%98-%EC%B0%A8%EC%9D%B4)

---

### TCP와 UDP
1. **TCP와 UDP의 차이점에 대해서 설명해보세요.**
- TCP
    - 신뢰적이고, 연결형 서비스를 제공하는 프로토콜
    - 주로 신뢰성이 요구되는 애플리케이션(DNS나 IPTV등)에서 사용
    
    ![image](https://user-images.githubusercontent.com/90819869/155228033-1a6d627f-2350-48a9-b88f-20ee4deda052.png)


- UDP
    - 비신뢰적이고, 비연결형 서비스를 제공하는 프로토콜
    - 간단한 데이터를 빠른 속도로 전송하고자 하는 애플리케이션(HTTP 등)에서 사용

    ![image](https://user-images.githubusercontent.com/90819869/155228060-b4364ded-5e8b-46ef-b23e-64207f8b0ca4.png)

| TCP(Transfer Control Protocol) | UDP(User Datagram Protocol) |
|--|--|
| 연결이 성공해야 통신 가능(연결형 프로토콜)	| 비연결형 프로토콜(연결 없이 통신이 가능) |
| 데이터의 경계를 구분하지 않음(Byte-Stream Service) |	데이터의 경계를 구분함(Datagram Service) |
| 신뢰성 있는 데이터 전송(데이터의 재전송 존재) |	비신뢰성 있는 데이터 전송(데이터의 재전송 없음) |
| 일 대 일(Unicast) 통신 |	일 대 일, 일 대 다(Broadcast), 다 대 다(Multicast) 통신 |

<br>

2. **3 way hand shake에 대해서 설명하세요.**
- TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 연결을 설정(Connection Establish) 하는 과정

  ![image](https://user-images.githubusercontent.com/90819869/155229115-5b50d1e6-59a3-4470-8f80-d4f14ff3b72c.png)
    1. 먼저 open()을 실행한 클라이언트가 연결 요청 메시지`SYN(Synchronize Sequence Numbers)`를 보내고 SYN_SENT 상태로 대기한다.
    2. 서버는 SYN_RCVD 상태로 바꾸고 SYN과 응답 ACK(Acknowledgment)를 보낸다.
    3. SYN과 응답 ACK을 받은 클라이언트는 ESTABLISHED 상태로 변경하고 서버에게 응답 ACK를 보낸다.
    4. ACK를 받은 서버는 ESTABLISHED 상태로 변경한다.
<br>

출처

[1. TCP vs UDP](https://velog.io/@hidaehyunlee/TCP-%EC%99%80-UDP-%EC%9D%98-%EC%B0%A8%EC%9D%B4#31-tcp%EC%9D%98-%ED%8A%B9%EC%A7%95)

[2. 3-way handshake](https://gmlwjd9405.github.io/2018/09/19/tcp-connection.html)
