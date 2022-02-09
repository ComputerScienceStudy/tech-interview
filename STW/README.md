면접 스터디 4팀 서태욱 자료 정리입니다. 

1주차

### JVM 동작과정/원리
자바 가상 머신(Java Virtual Machine)은 OS에 구애받지 않는 플랫폼 독립성을 특징으로 하여 Java와 OS 사이에 중개자 역할을 한다. 
![](https://images.velog.io/images/apolontes/post/e4893f72-bd7d-47ab-a7fd-0692a737c12a/2022-02-09_11-40-58.png)

1. 자바 프로그램 실행시 JVM은 OS에서 실행에 필요한 메모리를 할당받는다. 
2. 자바 컴파일러(javac)가 자바 소스코드(.java)를 읽어 자바 바이트코드(.class)파일로 컴파일링한다.
3. 컴파일링된 자바 바이트 코드는 클래스로더를 통해 JVM으로 동적 로딩(Dynamic Loading)된다.
4. 로딩된 파일들은 실행 엔진(Execution engine)을 통해 해석된다.
5. 해석된 코드는 각 런타임 데이터 영역(Runtime Data Areas)에 배치되어 실질적으로 수행된다.

※동적 로딩: 실행시에 모든 클래스를 로딩하지 않고 필요한 시점에 클래스를 로딩하여 사용

### GC(Garbage Collector)의 종류와 동작 과정/원리
GC는 쓰레기 객체 정리(Garbage Collector)의 약자이다. Java Runtime시 Heap 영역에 저장되는 객체는 따로 정리하지 않으면 계속 쌓여 OutOfMemory Exception이 발생할 수 있다. 이를 방지하기 위해 JVM이 OS로부터 메모리를 할당받은 후 GC를 통해 스스로 메모리 관리를 하게 된다.

#### GC의 종류
GC는 Heap영역 내에서 어떤 영역에서 수행되는지에 따라 Minor GC와 Major GC로 구분할 수 있다. 
Minor GC: Young Generation 영역에서 발생하는 GC
Major GD: Old, Perm 영역에서 발생하는 GC
![](https://images.velog.io/images/apolontes/post/edf9a604-8c59-4e81-a58c-a1c558e94bc4/2022-02-09_12-11-57.png)

#### 동작 과정
1. 메모리에 있는 개체가 현재 사용중인지 여부를 판단해야 한다.
2. 새 객체는 Young Generation의 일부인 Eden 영역에 위치한다.
3. 다른 곳에서 참조되지 않는 객체는 Minor GC가 발생하여 제거된다.
4. Eden영역에서 살아남은 객체는 Survivor 영역으로 이동한다.
5. Survivor 영역은 Survivor1 영역과 Survivor2 영역으로 구성되어 있다. 
Minor GC가 발생할 때마다 Survivor1 영역과 Survivor2 영역으로 객체들이 이동하며, 이 과정에서 참조되지 않는 객체는 제거된다.
6. 살아남은 객체는 Old Generation 영역으로 옮겨진다.
7. Old Generation, perm 영역에서 참조되지 않는 객체는 Full GC를 통해 제거된다.

### Java 언어 기초

#### 1. 정적 타입 언어와 동적 타입 언어의 차이
* 타입: 자료형이라고도 부르며, int, float, bool, short, 객체형 등이 있다. 
변수 선언시에 앞에 붙여 사용한다. 

* 정적 타입 언어: '정적'의 의미는 컴파일 시에 타입을 결정한다는 뜻이다. C, C#, C++, Java 등의 언어가 이에 해당한다. 변수에 들어갈 값에 따라서 타입을 지정해주어야 하는 언어들이다. 컴파일 시 미리 정보를 결정하기 때문에 속도가 빠르고 타입 에러로 인한 문제를 조기에 발견할 수 있어 안정성이 높다. 반면 타입이 미리 제한되기 때문에 유연성은 떨어진다.

* 동적 타입 언어: 동적 타입은 컴파일 시가 아니라 실행 시에 타입을 정하게 된다. Python, Ruby, JavaScript 등의 언어가 해당한다. 타입에 대한 결정을 Runtime까지 끌고 갈 수 있어 유연성이 있고, 상대적으로 코드 작성이 빠르다. 반면 실행 도중 변수에 예상하지 못한 타입이 들어와 에러가 발생할 수 있고, 코드가 복잡해지면 타입 에러를 찾기 어려운 측면이 있다.

#### 2. Java 코드의 컴파일 과정
1. 자바 소스코드(.java)를 작성한다.
2. 자바 컴파일러(javac)가 자바 소스코드(.java)를 읽어 자바 바이트코드(.class)파일로 컴파일링한다. 바이트 코드의 각 명령어는 1바이트 크기의 Opcode와 추가 피연산자로 구성된다.
3. 컴파일링된 자바 바이트 코드는 클래스로더를 통해 JVM으로 동적 로딩(Dynamic Loading)된다.
  클래스로더 동작 순서
  ①로드: 클래스파일을 JVM 메모리에 불러옴  
  ②검증: 자바 언어 명세 및 JCM 명세에 명시된 대로 구성되어 있는지 검사
  ③준비: 클래스가 필요로 하는 메모리 할당  
  ④분석: 클래스의 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경  
  ⑤초기화: 클래스 변수를 적절한 값으로 초기화 
4. 로딩된 파일들은 실행 엔진(Execution engine)을 통해 해석된다.
5. 해석된 코드는 각 런타임 데이터 영역(Runtime Data Areas)에 배치되어 실질적으로 수행된다.

#### 3. Java 변수
* 원시 타입(Primitive Type)과 참조 타입(Reference Type)
-원시 타입: 정수, 실수, 문자, 논리 리터럴 등 실제 데이터 값을 저장하는 
|타입|형|저장공간|범위|비고|
|:------:|:---:|:---:|:---:|:---:|
|int|정수|4 Byte|2,147,483,648 ~ 2,147,483,647 (약 ±20억)|-|
|long|정수|8 Byte|9,223,372,036,854,775,808|접미어 L 사용|
|short|정수|2 Byte|32,768 ~32,767|-|
|byte|정수|1 Byte|128 ~ 127|-|
|float|부동 소수점|4 Byte|약 +-3.40282347E+38F (자릿수 6~7)|접미어 F 사용|
|double|부동 소수점|8 Byte|약 +-1.79769313486231579E+308 (자릿수 15)|-|
|char|char|테스트3|-|UTF-16 문자 인코딩|
|boolean|boolean|-|True, False만 가능|논리 값 판단(참, 거짓)|

-참조 타입: 객체(Object)의 주소를 저장(참조)하는 타입. Array, Class, Interface 등

#### 4. overriding vs overloading 개념과 활용
* Overloading
자바 클래스 내에 이미 사용하려는 이름과 같은 메서드가 있더라도, 매개변수의 유형과 개수가 다르다면 같은 이름을 사용하여 다양한 유형의 호출에 응답하도록 하는 것.
```java
class OverloadingTest{
    //이름이 cat인 메서드
    void cat(){
        System.out.println("매개변수 없음");
    }
    
    //매개변수 int형이 2개인 cat 메서드
    void cat(int a, int b){
        System.out.println("매개변수 :"+a+", "+b);
    }
    
    //매개변수 String형이 한 개인 cat 메서드
    void cat(String c){
        System.out.println("매개변수 : "+ c);
    }
    
}
 
public class OverTest {
 
    public static void main(String[] args) {
        
        //OverloadingTest 객체 생성
        OverloadingTest ot = new OverloadingTest();
        
        //매개변수가 없는 cat() 호출
        ot.cat();
        
        //매개변수가 int형 두개인 cat() 호출
        ot.cat(20, 80);
        
        //매개변수가 String 한개인 cat() 호출
        ot.cat("오버로딩 예제입니다.");
        
    }
 
}

출처: https://private.tistory.com/25 [공부해서 남 주자]
```
* Overriding
메서드의 이름, 매개변수, 반환형이 같은 경우 상속받은 메서드를 덮어쓴다는 개념. 상위 클래스가 가진 메서드를 하위 클래스로 상속하여 사용할 수 있고, 상속한 메서드를 재정의해서 사용할 수도 있다.
```java
class Woman{ //부모클래스
    public String name;
    public int age;
    
    //info 메서드
    public void info(){
        System.out.println("여자의 이름은 "+name+", 나이는 "+age+"살입니다.");
    }
    
}
 
class Job extends Woman{ //Woman클래스(부모클래스)를 상속받음 : 
 
    String job;
    
    public void info() {//부모(Woman)클래스에 있는 info()메서드를 재정의
        super.info();
        System.out.println("여자의 직업은 "+job+"입니다.");
    }
}
 
public class OverTest {
 
    public static void main(String[] args) {
        
        //Job 객체 생성
        Job job = new Job();
        
        //변수 설정
        job.name = "유리";
        job.age = 30;
        job.job = "프로그래머";
        
        //호출
        job.info();
        
    }
 
}

출처: https://private.tistory.com/25 [공부해서 남 주자]
```