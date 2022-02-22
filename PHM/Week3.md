# [3주차] DB/Web/Network

## (1) DB

### 1. RDBMS(SQL) vs NOSQL에 대해서 설명해주세요
#### 핵심답변
RDBMS는 관계형 데이터베이스를 말하며, 행과 열로된 테이블 구조를 가집니다.        
고정된 테이블을 먼저 구성하고, 테이블에 맞춰 데이터를 쌓는 정형화된 방식입니다. <br>

NoSQL은 비 관계형 DB로, 관계형데이터베이스보다는 유연한 스키마를 제공합니다.        
키(key)와 값(value)의 형식으로 데이터가 저장되며 테이블 구조대신 도큐먼트(document) 형식을 가지는 동적 스키마를 제공합니다.     

sql DB는 특정 유형의 데이터만 넣을 수 있지만, Nosql은 정해진게 없어 자유로운 데이터 저장이 가능합니다.        

<br>

##### 🤔 그럼 NoSQL은 테이블 구조가 없나요?
아니요, Nosql에서 테이블에 매핑되는게 Collection이며, 행에 매핑되는게 document입니다.

<br><br>

##### 🤔 각각 어느 상황에서 사용하면 좋을까요?
RDBMS(sql)는 테이블을 나누어 조인하는 방식이기때문에, 복잡한 쿼리문이 필요하거나 높은 부하가 예상될때 유용합니다.        

Nosql은 데이터가 지속적으로 추가되고 변경되어 먼저 데이터 구조를 정하기 힘들때나, 데이터가 너무 많을때 속도 측면에서 유리합니다.

<br><br>

##### 🤔 Nosql이 데이터가 많을 때 속도 측면에서 유리하다고 생각한 이유가 무엇인가요?
RDBMS는 배열의 형식으로 데이터가 저장되기 때문에, 데이터를 찾가위해 모든 데이터를 조회합니다.     
반면 Nosql의 경우 key-value 형식 HashMap 구조이기 때문에 Key값만 있다면 더 빠른 조회가 가능하다고 생각합니다.

<br><br>

### 2. 인덱스에 대해서 아는데로 설명해주세요
#### 핵심답변
인덱스란 데이터베이스 테이블에 대한 검색 속도를 높이기위한 자료구조입니다.       
테이블에 인덱스를 설정해주면, 인덱스 테이블이 생성되고, key-rowid를 가집니다.        
key는 컬럽의 값, rowid는 논리적인 주소값을 가집니다.      

인덱스는 오직 조회에서만 사용되면, 테이블 데이터의 수정이 일어나면, 
인덱스 테이블은 수정(update)되지 않고 삭제되었다가 생성되기 때문에, 속도가 매우 느려집니다.

<br><br>

##### 🤔 데이터베이스에서 index를 만들면 내부적으로 어떤동작이 이루어지는지 설명해주시고 장단점에 대해 설명해주세요.
인덱스를 생성하면, 인덱스 테이블에선, 지정해준 컬럼의 값을 key로 가지고 key의 범위에 따라 자식 노드를 가집니다.     
각 노드의 키의 값은 다음 노드의 주소를 가르켜, 데이터를 조회할 때 데이터 범위에 따라 노드를 찾아가게됩니다.      

<br>

![image](https://user-images.githubusercontent.com/42319300/154984629-701cdeb4-3396-4aa6-bce6-22e352020f0e.png)


<br><br>

##### 🤔 인덱스에 왜 해쉬 보다 B Tree를 쓰는가?
해쉬테이블은 조회에서 빠르지만, 정렬이 되어있지않아 등호나 부등호와 같은 sql 조건절을 사용할 때 좋지않습니다.       
반면, B Tree는 항상 정렬되어있는 상태이며, 데이터들간의 범위를 사용해서 자식노드를 가지기때문에 인덱스에 매우 유리합니다.

<br>

![image](https://user-images.githubusercontent.com/42319300/154982109-ff04a650-c61a-4c0e-a6d3-40bdc58c2d45.png)

<br><br>

##### 🤔 그럼 인덱스를 생성하는건 항상 좋은건가요?
아닙니다. 위에서의 언급처럼, 인덱스는 업데이트나 생성 삭제 시 두번 일해야하기 때문에 매우 비효울적이며,     
인덱스 테이블이 많아질수록 데이터베이스 메모리의 과부화가 걸릴 수 있기 때문에, 쿼리문을 효율적으로 짜는 것을 우선으로 해야합니다.       


<br>

> [SQL-Index인덱스](https://velog.io/@gillog/SQL-Index%EC%9D%B8%EB%8D%B1%EC%8A%A4)     
> [B-Tree 구조](https://beelee.tistory.com/37)        
> [B tree를 인덱스에서 사용하는 이유](https://helloinyong.tistory.com/296)

<br><br>

### 3. 트랜잭션이 무엇인가요
#### 핵심답변
트랜잭션이란 "업무처리의 단위"로써, 데이터베이스의 상태를 변경시키기 위해 수행하는 작업의 단위를 말합니다.        

<br>

##### 🤔 트랜잭션은 왜 사용하나요? (장점)
작업의 안정성을 위해서입니다.        
트랜잭션은 커밋과 롤백을 제공함으로써, 작업이 불안정하게 종되었을 때 작업이전의 상태로 롤백하게됩니다.      
따라서 데이터 정합성을 지킬수 있습니다.
    
<br><br>

##### 🤔 트랜잭션의 특성에 대해 설명해주세요(ACID)
트랜잭션의 특징으로는 원자성, 일관성, 독립성, 영속성이 존재합니다.      
1. 원자성(Atomicity)이란, 작업 중간에 하나라도 문제가 발생한다면, 어떠한 작업도 수행되지 않아야한다는 것을 말합니다.(All or Nothing)
2. 일관성(Consistency)란, 작업 처리 결과가 항상 일관성있어야합니다. 즉, 트랜잭션 도중 DB가 변경되더라도 업데이트된 DB가 아닌 처음 참조된 DB를 사용해 작업이 진행되어야함을 말합니다.
3. 독립성(Isolation)이란, 여러 트랜잭션이 동시에 실행되고 있을경우, 각각의 작업은 서로 독립적으로 진행되어 다른 작업에 끼어들 수 없음을 의미합니다.
4. 영속성(Durability)란, 트랜잭션이 성공적으로 완료되었다면 그 결과는 영구적을 반영되어야함을 의미합니다.(비휘발성 메모리가 데이터가 저장됨을 의미)
<br><br>

##### 🤔 트랜잭션 격리 수준(Transaction Isolation Levels)에 대해서 설명해주세요.

<br><br>

##### 🤔 잠금 타임아웃(Lock timeout)과 교착 상태(Dead Lock)가 발생하는 이유에 대해서 설명해주세요.
트랜잭션은 같은 테이블에 대한 작업을 동시에 진행할 수 없습니다.        
따라서, 먼저 트랜잭션 작업중인 데이터에 다른 작업을위해 복수의 트랜잭션이 접근할 때, 기다리게 되는데 이를 잠금 대기상태라 하고,       
지정한 시간이 지나면 타임아웃이 발생합니다.        

교착 상태(Dead Lock)은 트랜잭션 작업을 위해 필요한 자원을 서로서로 요청하는 경우 무한 대기현상에 걸리기 때문에
이를 교착상태라 합니다.       

![image](https://user-images.githubusercontent.com/42319300/154993131-f6dad3a9-e8eb-4845-924c-3ebd4af79035.png)


<br><br>

### 4. 정규화(Normalization)에 대해서 설명해주세요
#### 핵심답변
정규화란, 테이블 간의 중복된 데이터를 허용하지 않는 것을 목표로 하는 일련의 작업을 말합니다.       
정규화를 진행함으로써 중복된 데이터를 허용하지 않고, 무결성을 유지하며, DB의 용량을 줄이는 것을 목표로합니다.

<br>

##### 🤔 Nomalization 이 무엇인가요? Denormalization은 무엇이고, 언제 시행하게 되는지 설명해주세요.
정규화를 하게되면 테이블을 작은 단위로, 관계를 맺기 편한 단위로 나누어지게 되는데,     
이렇게 되어 너무 많은 Join이 일어나면 쿼리의 비용이 증가되어 오히려 비효울적이게 됩니다.        

이를 해결하기 위한 것이 반정규화 혹은 비정규화이고,       
join의 비용을 줄이기 위해(성능을 개선하기 위해) 어느정도의 중복을 허용하여 테이블(Entity)를 재 통합하는것을 말합니다.

<br><br>

### 5. ORM이란 무엇인가요
#### 핵심답변
객체와 관계형 데이터베이스를 매핑해주는 것으로 쿼리문 작성 없이 객체를 데이터베이스에 직접 저장할 수 있게 도와주는 기술입니다.

<br>

##### 🤔 JPA, Hibernate 그리고 Spring Data JPA 각각에 대해서 설명해주세요.

JPA는 Java Persistance API의 약자로, 자바에서 데이터를 DBMS에 영구히 기록할 수 있는 환경을 제공하는 인터페이스입니다.     

이 JPA를 구현하고 있는 구현체 중에 하나가 Hibernate입니다.     

Spring Data JPA는 JPA를 편하게 사용할 수 있도록 만들어놓은 모듈입니다.        
Springboot에서 Repository를 JPA를 상속받아 특별한 구현체 없이 사용할 수 있도록하는 것이 spring data jpa의 대표적인 기술입니다.       

<br><br>

##### 🤔 데이터 정합성에 대해서 설명해주세요. JPA에서 이것들을 어떻게 처리하는가요?

<br><br>

##### 🤔 DB Lock에 대해서 설명해주세요. JPA에서 이것들을 어떻게 처리하는가요?


<br><br>

### 6. QueryDSL을 사용하는 이유와 JPQL과 차이점에 대해서 설명해주세요.
#### 핵심답변

<br><br>

### 7. (SQL문) A라는 테이블이 존재하여, 새로운 속성(Column)을 추가한다고 할 때, 모든 행(row)에 Default값을 넣어주고 싶다면, 어떤 쿼리문을 작성해야할까요
#### 핵심답변
alter table ~add 문을 사용할 수 있습니다.     
```sql
Alter table A add 컬럼명 자료형 default 초깃값;
```
---

## (2) Web

### 1.
#### 핵심답변
<br>

##### 🤔

<br><br>

---

## (3) Network

### 1.
#### 핵심답변
<br>

##### 🤔

<br><br>