# Tech Interview

## 목차
- [JAVA]()
    - [JVM 동작 과정/원리](https://github.com/ComputerScienceStudy/tech-interview#jvm-%EB%8F%99%EC%9E%91-%EA%B3%BC%EC%A0%95%EC%9B%90%EB%A6%AC)
    - [GC(Garbage Collector)의 종류와 동작 과정/원리](https://github.com/ComputerScienceStudy/tech-interview#gcgarbage-collector%EC%9D%98-%EC%A2%85%EB%A5%98%EC%99%80-%EB%8F%99%EC%9E%91-%EA%B3%BC%EC%A0%95%EC%9B%90%EB%A6%AC)
    - [정적 타입 언어와 동적 타입 언어의 차이](https://github.com/ComputerScienceStudy/tech-interview#%EC%A0%95%EC%A0%81-%ED%83%80%EC%9E%85-%EC%96%B8%EC%96%B4%EC%99%80-%EB%8F%99%EC%A0%81-%ED%83%80%EC%9E%85-%EC%96%B8%EC%96%B4%EC%9D%98-%EC%B0%A8%EC%9D%B4)
    - [Java 코드의 컴파일 과정](https://github.com/ComputerScienceStudy/tech-interview#java-%EC%BD%94%EB%93%9C%EC%9D%98-%EC%BB%B4%ED%8C%8C%EC%9D%BC-%EA%B3%BC%EC%A0%95)
    - [각 변수 타입이 몇 byte인지, primitive type과 reference type의 차이와 활용
    ](https://github.com/ComputerScienceStudy/tech-interview#%EA%B0%81-%EB%B3%80%EC%88%98-%ED%83%80%EC%9E%85%EC%9D%B4-%EB%AA%87-byte%EC%9D%B8%EC%A7%80-primitive-type%EA%B3%BC-reference-type%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%99%80-%ED%99%9C%EC%9A%A9)
    - [overriding vs overloading 개념과 활용](https://github.com/ComputerScienceStudy/tech-interview#overriding-vs-overloading-%EA%B0%9C%EB%85%90%EA%B3%BC-%ED%99%9C%EC%9A%A9)
    - [접근자 종류와 기능](https://github.com/ComputerScienceStudy/tech-interview#%EC%A0%91%EA%B7%BC%EC%9E%90-%EC%A2%85%EB%A5%98%EC%99%80-%EA%B8%B0%EB%8A%A5)
    - [final 키워드](https://github.com/ComputerScienceStudy/tech-interview#final-%ED%82%A4%EC%9B%8C%EB%93%9C)
    - [Generic의 개념](https://github.com/ComputerScienceStudy/tech-interview#generic%EC%9D%98-%EA%B0%9C%EB%85%90)
    - [ThreadLocal이 무엇이고 언제 활용되는지](https://github.com/ComputerScienceStudy/tech-interview#threadlocal%EC%9D%B4-%EB%AC%B4%EC%97%87%EC%9D%B4%EA%B3%A0-%EC%96%B8%EC%A0%9C-%ED%99%9C%EC%9A%A9%EB%90%98%EB%8A%94%EC%A7%80)
- Spring
  - POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?
  - spring IoC/DI의 동작원리
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
- JPA
  - JPA를 사용할 때의 이점에 대해서 설명해주세요.
  - JPA에서 N + 1 문제가 발생하는 이유와 이를 해결하는 방법을 설명해주세요.


<br><br>

### JVM 동작 과정/원리

---

****핵심답변****

JVM은 자바 가상 머신의 약자로, 컴퓨터가 자바 바이트코드를 실행시키는 역할을 합니다.        
JVM은 OS의 종류에 구애받지 않고서도 자바 파일이 실행될 수 있도록 중개자 역할을 해줍니다. 

1. 프로그램 실행시 JVM은 OS로부터 프로그램이 필요로하는 메모리를 할당받습니다.
2. 자바 컴파일러(.javac)가 자바 소스코드(.java)를 읽어 자바 바이트코드(.class)로 변환 시킵니다.
3. 컴파일링 된 바이트코드는 클래스 로더(Class Loader)를 통해 JVM으로 로딩됩니다.
4. 로딩된 파일들은 실행 엔진(Execution Engine)을 통해 해석됩니다.
5. 해석된 바이트코드는 Runtime Data Area에 배치되어 실질적으로 수행됩니다.

<br>

****🤔  JVM의 구조에 대해 자세히 설명해주세요.****

JVM은 Class Loader, Execution Engine, Runtime Data Area, Garbage Collector로 이루어져 있습니다. 

![image](https://user-images.githubusercontent.com/82690689/153175874-7d3ce60b-0858-4d79-9f8f-b79b93961e5e.png)

****🤔  자바를 platform independent programming language하는 이유는 무엇일까요?****   

JVM은 자바 코드를 컴파일해서 얻은 바이트 코드를 해당 운영체제가 이해할 수 있는 기계어로 바꿔 실행시켜주는 역할을 하기 때문에, 자바는 운영체제의 종류와 상관없이 동일하게 실행됩니다. 그래서 자바를 platform independent programming language라고 합니다.

---

<br><br>

### GC(Garbage Collector)의 종류와 동작 과정/원리

---

**핵심 답변**

가비지 콜렉터는 Young 영역에서 동작하는 Minor GC와 Old 영역에서 동작하는 Major GC로 그 종류를 나눌 수 있습니다.

가비지 콜렉터는 힙의 메모리가 가득찼을 때 발생하는데, GC를 실행중인 쓰레드를 제외한 쓰레드들이 동작을 멈추는 단계인 Stop the World가 실행되고, 참조되고 있는 객체들을 구분합니다. 이때, 참조되지 않는 객체들은 Garbage라고 판단하고 메모리에서 삭제함으로써 가비지 콜렉터 동작과정이 완료됩니다.

<br>

****🤔 가비지 콜렉터(Garbage Collector) 동작 과정을 조금 더 디테일하게 설명해주세요.****

1. 객체를 최초 생성하면 Young 영역에 Eden 영역에 위치합니다.
2. Eden 영역에서 Minor GC가 발생하면, 참조 중인 객체는 1번 Survivor 영역으로 이동합니다.
3. 1번 Survivor 영역에서 Minor GC가 발생하면, 참조 중인 객체는 2번 Survivor 영역으로 이동하고 1번 Survivor 영역은 비게됩니다.
4. Young 영역에서 오래 살아남은 객체는 Old영역으로 이동하게 됩니다.
5. Old 영역에 있는 객체는 Major GC가 발생했을 때, 참조 여부에 따라 유지되거나 제거됩니다. 

<br>

****🤔 가비지 콜렉터(Garbage Collector)가 뭔가요?****

유효하지 않은 메모리, 즉 주소를 잃어버려서 사용할 수 없는 메모리를 Garbage라고 하는데, Garbage Collector는 메모리가 부족할 때 이런 Garbage를 해제시켜 다른 용도로 사용할 수 있게 해주는 프로그램을 말합니다.

<br>

****🤔 Young영역과 Old 영역이 뭔가요?****

JVM에서 가비지 콜렉터 기능을 향상시키기 위해 힙을 물리적으로 구분한 것으로 Young영역의 경우 할당된지 얼마 안되는 객체가 존재하고 Old영역의 경우 오래동안 살아남은 객체가 존재합니다.

<br>

****🤔 Young 영역에서 Old 영역으로 이동(Promotion)하게 되는 기준이 무엇인지 설명해주실 수 있을까요?****

Minor GC에서 객체가 살아남은 횟수를 의미하는 것을 age라고 하는데, 이 age는 Object Header에 기록이 됩니다. 이 age를 기반으로 Old 영역으로의 이동 여부를 결정하게 됩니다.

<br>

****🤔 Garbage Collector의 알고리즘 종류 아시는거 있으면 설명해주실 수 있을까요?****

첫번째로 Serial GC가 있습니다. Old 영역에서 Mark Sweep Compact 알고리즘이 사용되고, 기존의 GC동작과 동일하지만, Sweep단계 이후 힙의 가장 앞 부분부터 채워서 객체가 존재하는 부분과 존재하지 않는 부분을 구분하는 Compact 단계가 추가로 존재하는 알고리즘입니다. 이 가비지 콜렉터의 경우 1개의 쓰레드로만 동작됩니다.

두번째로 Parallel GC가 있습니다. Serial GC와 동일하지만, 차이점은 여러개의 쓰레드를 통해 Parallel하게 GC를 수행할 수 있게 되어 있어 오버헤드를 줄여줍니다.

마지막으로 G1(Garbage First)GC가 있습니다. 기존의 GC와는 다르게 Heap을 물리적으로 Young 영역과 Old 영역을 나누는 것이 아니라, 지역(Region)개념을 도입하여 논리적으로 Heap을 균등하게 여러개의 지역으로 나눠 각 지역을 역할과 함께 논리적으로 구분하여 객체를 할당하게 만드는 GC입니다.

---

<br><br>

### 정적 타입 언어와 동적 타입 언어의 차이

---

****핵심답변****

타입(자료형)의 결정을 컴파일할 때 결정한다면 정적 타입 언어(Java, C, C++), 런타임 과정에서 결정한다면 동적 타입 언어(Python, JavaScript, Rudy)입니다.

<br>

****🤔 각각의 장단점은 무엇 일까요?****

정적 타입 언어는 미리 타입이 결정되어 실행 속도가 빠르며 타입 에러로 인한 문제점을 초기에 발견할 수 있어 타입 안정성이 높다는 장점이 있습니다. 반면 매번 타입을 결정해야 하기 때문에 유연성이 떨어집니다.

동적 타입 언어는 런타임까지 타입 결정을 끌고 갈 수 있어 유연성이 있고 상대적으로 코드 작성도 빠릅니다. 하지만 실행 도중 변수에 예상치 못한 타입이 들어와 타입 에러가 발생할 수 있고, 코드가 길고 복잡해질 경우 에러를 발견하기 힘듭니다. 

<br>

****🤔 타입은 무엇이고, 어떤 것들이 있죠?****

자료형이라고도 부르며, 저장하는 데이터 표현 방식을 달리하고 저장 공간을 효율적으로 사용하기 위해 사용합니다. 정수형에 해당하는 byte, short, long, int, 실수에 해당하는 float, double, 문자를 나타내는 char, 논리형으로 참,거짓을 나타내는 boolean등이 있습니다. 변수 선언시에 앞에 붙여 사용합니다.

---

<br><br>

### Java 코드의 컴파일 과정

---

**핵심 답변**

첫번째로, 개발자가 자바 소스 코드를 작성하면, 자바 컴파일러가 자바 소스 파일을 컴파일 합니다. 

이때 나오는 파일은 자바 바이트 코드 파일로, 아직 컴퓨터가 읽을 수 없는 자바 가상 머신이 이해할 수 있는 코드 입니다.

두번째로, 컴파일 된 바이트 코드를 JVM의 클래스 로더에게 전달합니다.

세번째로, 클래스 로더는 동적로딩을 통해 필요한 클래스들을 로딩 및 링크하여 JVM의 런타임 데이터 영역에 올립니다.

마지막으로 실행엔진은 JVM 메모리에 올라온 바이트 코드들을 명령어 단위로 하나씩 가져와서 실행합니다.   
이때, 실행엔진은 바이트 코드를 각 OS가 실행할 수 있는 기계어로 변환시킵니다.

<br>

**🤔 바이트 코드란?**

바이트 코드는 특정 하드웨어가 아닌 가상 머신에서 돌아가는 실행 프로그램을 위한 이진 표현법입니다.

바이트 코드의 대부분 명령어는 0개 이상의 매개변수를 갖는 1바이트 크기를 가지고 있습니다.

<br>

**🤔 클래스로더 동작에 대해 구체적으로 설명해주세요.**

클래스 로더의 세부 동작은 다음과 같습니다.

1. 가장 먼저, 클래스 파일을 가져와서 JVM의 메모리에 로드합니다.
2. 그 다음, 자바 언어 명세 및 JVM 명세에 명시된 대로 구성되어 있는지 검사합니다.
3. 검사 후에는, 필드, 메서드, 인터페이스 등 메서드클래스가 필요로 하는 메모리를 할당합니다.
4. 이 후, 클래스의 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경합니다.
5. 마지막으로 클래스 변수들을 적절한 값으로 초기화합니다.

<br>

**+ 심볼릭 레퍼런스는 무엇인가요?**

심볼릭 레퍼런스는 참조할 때, 클래스의 특정 메모리 주소를 참조 관계로 구성한 것이 아닌 참조하는 대상의 이름을 지칭합니다.

Class 파일이 JVM에 올라가게 되면 심볼릭 레퍼런스는 그 이름에 맞는 객체의 주소를 찾아서 연결하는 작업을 수행합니다. 그러므로, 실제 메모리 주소가 아니라 이름만을 가집니다.

<br>

**+ 다이렉트 레퍼런스로 변경이라는 의미는?**

실제 메모리 주소 값으로 변경해 주는 작업을 의미합니다.

<br>

**🤔 동적로딩이란 무엇인가요?**

동적로딩은 프로그램을 실행할 때, 필요할 때마다 동적으로 메모리를 생성하고 필요없는 메모리는 자동으로 메모리에서 소멸시키는 것을 말합니다. 일부 클래스가 변경되어도 전체 어플리케이션을 다시 컴파일 하지 않아도 되기에, 변경사항이 발생해도 비교적 적은 작업만으로도 처리할 수 있습니다.

<br>

**🤔 실행엔진은 어떻게 바이트 코드들을 실행하나요?**

두가지 방식을 사용하게 됩니다.

- `인터프리터` 방식은 바이트코드 프로그램은 보통 한 번에 하나의 명령어를 읽은 후 실행합니다. <br>이러한 형태의 바이트코드 인터프리터는  한 줄씩 수행하기 때문에 느립니다.
- 인터프리터 방식의 단점을 보완하기 위해 도입된 `JIT 컴파일러`가 나왔습니다.
    
    인터프리터 방식으로 실행하다가 적절한 시점에서 바이트 코드 전체를 컴파일 하여 네이티브 코드로 변경하고, <br>이후에는 더이상 인터프리팅 하지 않고 네이티브 코드를 직접 실행합니다. 
    
    JIT 컴파일러를 사용하는 JVM은 내부적으로 해당 메서드가 얼마나 자주 수행되는지 체크하고, 일정 정도를 넘었을 때, 컴파일을 수행합니다.
    
- JIT 컴파일러로 인해, 자바는 네이티브 언어와 유사한 수준의 퍼포먼스를 낼 수 있게 되었습니다.

---

<br><br>

### 각 변수 타입이 몇 byte인지, primitive type과 reference type의 차이와 활용

---

### 핵심 답변

primitive type는 기본 데이터 타입으로,

종류는 byte, short, char, int, float, double, boolean이 있습니다.

- 정수형 : byte, short, int, long `1, 2, 4, 8 byte`
- 실수형 : float, double `4, 8 byte`
- 논리형 : boolean(ture/false) `1 byte`
- 문자형 : char `2 byte`

<br>

reference type은 참조 데이터 타입으로,

기본 데이터 타입을 제외하고는 모두 참조 데이터 타입입니다.

종류는 class, array, interface, Enumeration이 있습니다.

참조 타입은 값이 저장된 곳의 주소를 저장합니다.

참조 타입은 `4 byte` 크기의 주소값이 들어갑니다.

<br>

primitive type과 reference type의 차이점은 다음과 같습니다.

기본 데이터 타입은 실제 데이터 값 자체를 저장합니다.

데이터의 크기가 작고 고정적이기 때문에 메모리의 Stack 영역에 저장됩니다.

반면, array와 class와 같은 참조 데이터 타입은 객체가 메모리 상에 위치한 주소를 저장합니다.

데이터의 크기가 동적이기 때문에 동적으로 관리하는 Heap 영역에 저장됩니다.

또한, 참조 데이터 타입의 경우 더이상 참조하는 변수가 없을 때, 가비지 컬렉션에 의해 파괴 됩니다.

<br>

primitive type과 reference type의 활용은 다음과 같습니다.

primitive type은 null을 다루지도 못하고, generics에 담기지도 못하지만,      
primitive type이 reference type과 비교해서 갖는 장점은 성능과 메모리에 이점이 있습니다.

왜냐하면, reference type은 스택 메모리에는 참조 값만 있고 실제 값은 힙 메모리에 존재하기 때문입니다.        
따라서 reference type은 값이 필요로 할 때마다, primitive type과 비해 접근 속도가 느려지게 됩니다.

데이터가 동적이지 않으면, 성능과 메모리에 장점이 있는 primitive type을 먼저 고려해보고,        
만약 Null을 다뤄야 하거나, Generic 타입에서 사용되어야 한다면 reference type을 사용합니다.

---

<br><br>

### overriding vs overloading 개념과 활용

---

오버라이딩은 부모 클래스가 가지고 있는 메서드를 자식 클래스에서 재정의해서 사용하는 것을 말합니다.       
오버라이딩은 코드를 재사용하기 위해서 사용하는데요.      
자식 클래스가 부모 클래스를 상속 받아 중복 코드를 없애고, 자식 클래스마다 재정의가 필요한 부문만 오버라이딩하여 추가로 구현할 수 있습니다.     

오버로딩은 메서드의 이름은 동일하나 매개변수의 개수 또는 타입의 종류가 다르면 같은 이름을 재정의해서 사용할 수 있는 것을 말합니다.       
오버로딩의 이점은 같은 기능을 하는 메서드를 하나의 이름으로 사용할 수 있다는 것입니다.     
대표적인 예로 System.out.println() 함수가 있습니다.

---

<br><br>

### 접근자 종류와 기능

---

`접근 제어자`는 클래스, 인터페이스, 멤버 변수/함수 등의 접근을 제어하는 지시어를 말합니다.

| 접근 제어자 | 같은 클래스의 멤버 | 같은 패키지의 멤버 | 자식 클래스의 멤버 | 그 외 영역 |
| --- | --- | --- | --- | --- |
| Public | O | O | O | O |
| Protected | O | O | O | X |
| Default | O | O | X | X |
| Private | O | X | X | X |


- `public` 모든 패키지, 모든 클래스의 접근 허용
- `protected` 같은 패키지, 모든 클래스의 접근 허용
    
    (단, 다른 패키지인 경우 자식 클래스의 접근 허용)
    
- `default` 같은 패키지 내 클래스만 접근 허용
- `private` 같은 클래스 내 접근만 허용

접근 제어자를 사용하는 이유는 다음과 같습니다.
- 객체지향 프로그래밍이란 객체들 간의 상호작용을 코드로 표현하는 것인데요.
- 이때 객체들간의 관계에 따라서 접근 할 수 있는 것과 아닌 것, 권한을 구분할 필요가 생깁니다.
- 클래스 내부에 선언된 데이터의 부적절한 사용으로부터 보호하기 위해서 접근 제어자를 사용합니다.

---

<br><br>

### final 키워드

---

final 키워드는 변수나 메서드 또는 클래스가 '변경 불가능' 하도록 만듭니다.   
`final`로 선언 시, 한 번 초기화 가능합니다.
final 필드가 초기화 되면, 그 초기값이 최종적인 값이 되어 프로그램 실행 도중 수정 불가능합니다.         
클래스, 메서드, 변수가 변하지 않도록 하기 위해 사용합니다.

| 적용 대상 | 적용 결과 |
| --- | --- |
| 기본 변수 | 해당 변수의 값 변경 X |
| 참조 변수 | 참조 변수가 힙(heap) 내의 다른 객체를 가리키도록 변경  X |
| 메서드 | 해당 메서드 오버라이드 X |
| 클래스 | 해당 클래스의 하위 클래스 정의 X |

<details>
<summary>개념 +α</summary>
<div markdown="1">
  
- **finally**
    - `try/catch` 블록이 종료될 때 항상 실행될 코드 블록을 정의하기 위해 사용
    - 예외 발생 시에도 항상 실행 (단, JVM이 `try` 블록 실행 도중 종료되는 경우는 제외)
- **finalize() 메서드**
    - GC(Garbage Collector)가 자동으로 참조하지 않는 배열이나 객체를 힙(Heap) 영역에서 제거하도록 기능을 수행하는 메서드
    - Object 클래스의 finalize() 메서드를 오버라이드해서 맞춤별 GC 정의 가능
        - protected void finalize() throws Throwable { // 파일 닫기, 자원 반환 등등 }


</div>
</details>

---

<br><br>

### Generic의 개념

---

**핵심 답변**

데이터 타입(data type, 자료형)을 일반화(generalize)하는 것으로,      
클래스나 메소드에서 사용할 내부 데이터 타입을 클래스 외부에서 컴파일 시에 미리 지정하는 것입니다.    
<> 괄호 안에 타입을 지정해 줍니다. 

자주 사용되는 타입 인자는 다음과 같습니다.

```java
- <T> == Type
- <E> == Element
- <K> == Key
- <V> == Value
- <N> == Number
- <R> == Result
```

<br>

**🤔 Generic을 사용하면 어떤 점이 좋은가요?**

타입을 미리 명시해서 컴파일 시에 객체 타입이 체크 되므로 의도하지 않은 타입의 객체가 저장되는 것을 막을 수 있습니다.     
또한 잘못된 형 변환을 막을 수 있기 때문에 안정성도 높아집니다.      
더불어 동작은 같지만 클래스 타입만 바뀌어야 하는 경우를 쉽게 다룰 수 있게 됩니다. 

---

<br><br>

### ThreadLocal이 무엇이고 언제 활용되는지

---

**핵심답변**

ThreadLocal은 Thread 내부에서 사용하는 지역변수입니다.    
일반 변수는 특정 코드 블록 범위 내에서만 유효하지만,      
ThreadLocal을 이용하면 쓰레드 영역에 변수를 설정할 수 있기 때문에,     
특정 쓰레드가 실행하는 모든 코드에서 그 쓰레드에 설정된 변수 값을 사용할 수 있게 됩니다.   
멀티 쓰레드 환경에서 각 쓰레드마다 get(), set() 메서드를 통해 독립적으로 변수에 접근할 수 있습니다.      

ThreadLocal의 활용은 다음과 같습니다.      
ThreadLocal은 한 쓰레드에서 실행되는 코드가 동일한 객체를 사용할 수 있도록 해 줍니다.
따라서, 쓰레드와 관련된 코드에서 변수를 공유할 때, 파라미터 또는 리턴 값으로 정보를 제공해주지 않아도 됩니다.     

대표적인 활용 예시는 Spring Security에서 사용자 인증 정보를 사용입니다.       
서버에서 클라이언트 요청들에 대해 각 쓰레드에서 처리하게 될 경우, 해당 유저의 인증 및 세션 정보나 참조 데이터를 저장하는데 ThreadLocal이 사용됩니다.    

<br>

**🤔 ThreadLocal의 내부는 어떻게 되어 있을까요?**

ThreadLocal의 내부는 thread 정보를 key로 하여 값을 저장해두는 Map 구조를 가지고 있습니다.        
기본적인 사용에는 `get`, `set` 메서드를 이용합니다. 

<br>

🤔 **ThreadLocal 사용시 주의 사항은 무엇이 있을까요?**

ThreadLocal은 Thead의 정보를 key로 하여 Map의 형식으로 데이터를 저장한 후 사용할 수 있는 자료구조를 가지고 있습니다.               
따라서 만약 ThreadPool을 사용하여 thread를 재활용한다면                
동일한 이전에 세팅했던 ThreadLocal의 정보가 남아있어 원치않는 동작을 할 수 있습니다.     
따라서 ThreadPool을 사용하는 경우에는 반드시 모두 사용 후 ThreadLocal의 값을 remove 메서드를 사용하여 값을 제거해주는것이 필요합니다.

---

<br><br>

### Java SE와 JAVA EE 애플리케이션 차이가 뭔가요?

---

**핵심답변**

JAVA SE는 자바 표준 에디션이고, JAVA EE는 JAVA SE의 API에 추가로 JSP, Servelt 등의 추가 API를 탑재한 것입니다.

---

<br><br>

### 객체지향 프로그래밍과 절차지향 프로그래밍의 차이를 설명해주실 수 있을까요?

---

**핵심답변**

절차지향 프로그래밍은 실행하고자 하는 절차를 정하고, 이 절차대로 프로그래밍하는 방법을 의미합니다.
객체지향 프로그래밍이란 연관되어 있는 변수와 메서드를 하나의 그룹으로 묶어 클래스(개념)를 구현하고 이들 사이의 상호 작용을 프로그램으로 나타낸것을 의미합니다.

<br>

🤔 **객체지향 프로그래밍의 장,단점을 설명해주세요.**

하나의 클래스에서 서로 다른 상태를 갖는 인스턴스를 만들 수 있어 재활용성이 뛰어나고, 강한 응집력과 약한 결합력을 갖고있습니다. 덕분에 유지보수와 분석에 비교적 쉽습니다.
반면에 단점으로는 각 객체 간의 정보 교환이 일어남으로 실행 시스템에 비교적 많은 Overhead가 발생합니다.
