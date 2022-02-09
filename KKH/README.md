# Tech-Interview

### JVM 동작 과정/원리
- JVM이란?<br>
JAVA 바이트 코드를 실행시키기 위한 가상머신이다. 이것은, 자바 애플리케이션을 클래스 로더를 통해 읽어 들여 자바 API와 함께 실행시키는 것을 의미한다.<br>
JVM은 OS와 JAVA 사이의 중개자 역할을 하고 있어 JAVA가 OS에 구애받지 않고 실행될 수 있도록 해준다. 그리고 메모리 관리, Garbage Collection을 수행한다.<br>
JVM은 스택 기반의 가상 머신이다.

- JVM 동작 과정
  1. 프로그램이 실행되면 JVM은 OS로부터 이 프로그램이 필요로 하는 메모리를 할당받는다. JVM은 이 메모리를 용도에 따라 여러 영역으로 나눠 관리한다.
  2. 자바 컴파일러(javac)가 자바 소스코드(.java)를 읽어들여 자바 바이트코드(.class)로 변환시킨다.
  3. Class Loader를 통해 class파일들을 JVM으로 로딩한다.
  4. 로딩된 class 파일들은 Execution Engin을 통해 해석된다.
  5. 해석된 바이트코드는 Runtime Data Area에 배치되어 실질적인 수행이 이루어지게 된다.<br>
  이러한 실행 과정 속에서 JVM은 필요에 따라 Thread Synchronization과 GC같은 관리 작업을 수행한다.<br>
  
  ![image](https://user-images.githubusercontent.com/82690689/153118295-6decce56-97f7-4e13-8fd9-d349bc09b1fe.png)
  JVM의 Class Loader는 동적 로딩을 통해 필요한 클래스들을 로딩 및 링크 하여 Runtime Data Area에 올린다. 그 후 Excution Engine은 JVM에 올라온 바이트 코드(.class)들을 명령어 단위로 하나씩 가져와서 실행시킨다. Execution Engine은 Interpreter와 JIT Compiler에 의해 동작한다.
 
- 클래스 로더(Class Loader) 동작 과정
  1. Loading(로드) : 클래스 로더의 위임모델을 기반으로 가져온 .class 파일을 읽어서 바이너리 코드로 만들고 이를 메모리의 메서드 영역(Method Area)에 저장하는 과정이다.<br>
                     저장하는 데이터는 다음과 같다.<br>
     - FQCN
     - Class, Interface, Enum을 구분하여 저장
     - 메서드와 변수

      로딩이 끝나면 해당 클래스 타입의 객체를 생성하여 메모리의 힙 영역(Heap Area)에 저장한다.
  2. Verifying(검증) : 읽어들인 클래스가 자바 언어 명세 및 JVM 명세에 명시된 대로 구성되어 있는지 검사한다.
  3. Preparing(준비) : 클래스가 필요로 하는 메모리를 할당한다. 필요한 메모리란 클래스에서 정의된 필드, 메서드, 인터페이스들을 나타내는 데이터 구조들 등등을 의미한다.
  4. Resolving(분석) : 클래스의 상수 풀 내 모든 심볼릭 레퍼런스(API를 Link할 수 있는 대상의 이름을 지칭한 것)를 다이렉트 레퍼런스(이름에 맞는 물리적 주소)로 변경한다.
  5. Initializing(초기화) : 클래스 변수들을 적절한 값으로 초기화 한다. (static 필드들을 설정된 값으로 초기화 등)<br>

  <details>
  <summary>동작 과정 그림</summary>
  <div markdown="1">

  ![image](https://user-images.githubusercontent.com/82690689/153119355-e572aa5c-e05e-4d3b-95cd-4b450850a5a7.png)

  </div>
  </details>
  
 
- 클래스로더(Class Loader) 특징
 1. 계층 구조<br>
클래스 로더는 여러 클래스 로더 끼리 부모-자식 관계를 이루고 있어서 계층적인 구조로 되어 있다.
    - 부트스트랩 클래스 로더(Bootstrap Class Loader)
      - jre/lib/rt.jar 에 담긴 JDK 클래스 파일을 로딩한다.
      - 유일하게 네이티브 코드로 구현되어 있다.
      - Object 클래스를 비롯하여 JAVA API들을 로드한다.
    - 익스텐션 클래스 로더(Extension Class Loader)
      - jre/lib/ext 폴더나 java.ext.dirs 환경 변수로 지정된 폴더에 있는 클래스 파일을 로딩한다.
      - 기본 JAVA API를 제외한 확장 클래스들을 로드한다.
    - 시스템 클래스 로더(System Class Loader)
      - 상위 계층들이 JVM 자체의 구성요소들을 로드한다면, 시스템 클래스 로더는 어플리케이션의 클래스들을 로드한다.(개발자가 어플리케이션 구동을 위해 직접 작성한 대부분의 클래스는 이 곳에서 로드한다.)
    - 사용자 정의 클래스 로더(User-Defined Class Loader)
      - 어플리케이션 사용자가 직접 코드상에서 생성하여 사용하는 클래스 로더

    <details>
    <summary>계층 구조 그림</summary>
    <div markdown="2">

    ![image](https://user-images.githubusercontent.com/82690689/153121828-67c29497-0172-4e52-84fd-5107c48938ae.png)

    </div>
    </details>

 2. 위임모델<br>
바이트코드를 넘겨받은 클래스 로더가 필요한 클래스를 로드할 때 혹은 실행엔진에서 명령어 단위로 바이트코드를 실행하다가 처음으로 참조하는 클래스에 대해 클래스 로더에게 로드를 요청할 때 로드를 요청받은 클래스로더는 다음 순서대로 요청받은 클래스가 있는지 확인한다.
    1. 클래스 로더 캐시
    2. 상위 클래스 로더
    3. 자기 자신
    
     이전에 로드된 클래스인지 클래스 로더 캐시를 확인하고, 없으면 상위 클래스 로더를 하나씩 거슬러 올라가면서 확인한다. 올라가는 도중에 클래스를 발견하더라도 부트스트랩 클래스 로더까지 확인을 하고 부트스트랩 클래스로더에도 해당 클래스가 존재하면 부트스트랩 클래스 로더에 있는 클래스를 로드한다. 마지막으로 부트스트랩 클래스 로더에도 해당 클래스가 존재하지 않으면 요청받은 클래스 로더가 파일 시스템에서 해당클래스를 찾는 것으로 마무리가 된다.
     
 3. 가시성 제한<br>
위임모델에 의해서 클래스 로더 캐시를 확인하고 없으면 상위 클래스 로더를 확인하는데 이 때 하위 클래스 로더에 있는 클래스는 확인이 불가능한 특성이다.

 4. 언로드 불가<br>
클래스는 로드하는 것은 가능하지만 언로드하는 것은 불가능하다.

 5. 네임스페이스(Name space)<br>
각 클래스 로더들이 가지고 있는 공간으로 로드된 클래스를 보관하는 공간이다. 위임모델을 통해 상위 클래스 로더들을 확인할 때, 확인하는 공간이 바로 네임스페이스이다. 보관되는 기준은 FQCN(Fully Qualified Class Name)을 기준으로 보관된다. FQCN은 패키지명, 주소까지 포함되어 있는 식별자를 의미한다.<br>
FQCN이 같아도 네임스페이스가 다른 경우 다른 클래스로 간주한다.<br>
 
- 런타임 데이터 영역(Runtime Data Area)
  - heap<br>
  인스턴스화 된 모든 클래스 인스턴스와 배열, 객체를 저장하게 되는데 모든 JVM 스레드에 공유되는 공유 자원이다. 힙에 저장되어 있는 할당된 메모리 회수 권한은 GC에 의해서만 회수 가능하다.
  - Method Area<br>
  메서드 영역에서는 런타임 상수풀, 필드와 메서드 데이터 내용, 즉 클래스 수준의 정보를 저장하게 된다. 논리적으로 힙의 일부여서 GC의 대상이 되기도 한다. JVM을 만드는 회사마다 다르게 정의를 내리고 있다.
  - Runtime Constant Pool<br>
  각 클래스와 인터페이스의 상수 뿐만 아니라, 메서드와 필드에 대한 모든 레퍼런스까지 담고있는 테이블로 어떤 메서드나 필드를 참조할 때 JVM은 런타임 상수 풀을 통해 해당 메서드나 필드의 실제 메모리상 주소를 찾아서 참조한다.
  - PC Register<br>
  PC 레지스터는 현재 실행중인 명령의 주소를 가진다. 즉 연산을 위해 필요한 피연산자를 임시로 저장하기 위한 용도로 사용한다.
  - JVM Stack<br>
  LIFO 동작을 하는 자료구조로써, 쓰레드 마다 런타임 스택을 만들고 스택 프레임이라는 구조체를 저장하는 스택이다. 메서드 하나가 호출될 때마다 새 프레임이 생성되어 스택에 쌓이고, 메서드 호출이 정상 완료되거나 예외가 던져지면 프레임은 스택에서 빠지면서 소멸된다. 또한, 쓰레드가 종료되면 제거된다.
  - Native Method Stack<br>
  네이티브 메서드 스택은 JVM의 스택이 아니라 C 스택을 가르킨다. 자바가 아닌 다른 언어로 작성된 네이티브 메서드를 지원하기 위해 사용되는 스택이다.
  
  <details>
  <summary>런타임 데이터 영역 그림</summary>
  <div markdown="3">

  ![image](https://user-images.githubusercontent.com/82690689/153124060-7b72cb2e-e39b-4248-9034-497c68731afb.png)

  > [Back to the Essence - Java 컴파일에서 실행까지 by HomoEfficio](https://homoefficio.github.io/2019/01/31/Back-to-the-Essence-Java-%EC%BB%B4%ED%8C%8C%EC%9D%BC%EC%97%90%EC%84%9C-%EC%8B%A4%ED%96%89%EA%B9%8C%EC%A7%80-2/)
  
  </div>
  </details>
  
- 실행 엔진(Execution Engine)<br>
실행 엔진은 클래스 로더를 통해 런타임 데이터 영역에 배치된 바이트 코드를 명령어 단위로 읽어서 실행한다.<br>
바이트 코드의 각 명령어는 1바이트 크기의 OpCode(Operation Code)와 추가 피연산자로 이루어져 있다. 실행 엔진은 하나의 OpCode를 가져와서 피연산자와 작업을 수행한 다음, 그 다음 OpCode를 수행하는 식으로 동작한다.<br>
이 수행 과정에서 실행 엔진은 바이트 코드를 기계가 실행할 수 있는 형태로 변경하고 이러한 형태는 인터프리터와 JIT 컴파일러가 있다.

- 이해하는데 도움되는 정보

  <details>
  <summary>스택 기반 VM</summary>
  <div markdown="5">

  하드웨어(CPU 레지스터)의 한계를 벗어나기 위해 사용되는 기법으로 바이트 코드를 통해 값을 가져오고, 계산하고, 저장하고, 반환하는 과정에서 스택을 활용하는 것이 스택 기반 VM이다. 스택의 특징 상 명령어들이 간단하지만, 간단한 코드를 수행하기 위해 꽤나 많은 Byte Code가 필요하다.<br>
(레지스터 기반 VM의 경우 메모리의 주소를 명시해야 하므로 명령어의 길이가 길어지지만, 하나의 명령어로 계산할 수 있어지므로 명령어의 수가 적어지는 장점이 있다, 대신 하드웨어(CPU 레제시트)를 기반으로 하기 때문에 하드웨어 성능에 스택 기반 VM보다 더 많은 영향을 받는다.)
  
  </div>
  </details>
  
  <details>
  <summary>프레임(Frame)</summary>
  <div markdown="6">

  반환주소, 메서드로 넘어온 매개변수, 메서드가 정의하는 지역 변수를 포함한다. 모든 메서드 호출에는 프레임이 필요하다.
  
  </div>
  </details>
  
  <details>
  <summary>피연산자 스택(Operand stack)</summary>
  <div markdown="7">

  LIFO 자료 구조이다. JVM이 지원하는 대부분의 명령어는 매개변수를 받는데, 이 매개변수를 저장한다. 즉, 스택 기반의 VM에서 활용되는 스택이 바로 피연산자 스택이다.
  
  </div>
  </details>
  
  <details>
  <summary>Java API란?</summary>
  <div markdown="7">

  응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 의미한다. 즉, java언어를 사용하면서 누군가 코딩을 쉽게 할 수 있도록 만들어 놓은 것이다. 내장되어 있는 API는 jdk를 설치하면서 설치가 된다.<br>
예) System.out.println
  
  </div>
  </details>
  
  <details>
  <summary>동적 로딩이란?</summary>
  <div markdown="8">

  실행 시에 모든 클래스가 로딩되지 않고 필요한 시점에 클래스를 로딩하여 사용할 수 있게 하는 것을 동적 로딩이라 한다.
  - 런타임 동적 로딩 : 코드를 실행하는 순간에 필요한 클래스를 로딩하는 것
  
  </div>
  </details>
  
  <details>
  <summary>Interpreter란?</summary>
  <div markdown="9">

  고레벨언어를 기계어로 해석해주는 번역 프로그램이다. 컴파일러는 전체 소스코드를 보고 명령어를 수집하고 재구성하는 반면 인터프리터는 소스코드의 각 행을 연속적으로 분석하며 실행한다. 때문에 일반적으로 각 행마다 실행하는 인터프리터보다는 컴파일러가 더 빠르다.
  
  </div>
  </details>
  
  <details>
  <summary>JIT compiler(Just-In-Time compiler)란?</summary>
  <div markdown="10">

  각 행마다 변환해줘야 해서 속도 측면에서 느린 인터프리터를 개선하기 위해 등장한 것으로 바이트 코드 전체를 네이티브 코드로 변환하여 네이티브 코드 자체를 실행시키는 것이다. 하지만, 바이트 코드를 전체 프로그램 수행 초기에 모두 컴파일하게 되면 초기 속도가 너무 느리게 될 수 있다는 문제가 있다. 그렇기 때문에 모든 코드는 초기에 인터프리터에 의해 시작되고, 해당 코드를 충분히 많이 사용할 경우 JIT 컴파일러에서 컴파일을 수행하게 된다. 초기에 인터프리터 방식으로 바이트 코드를 변환하면서 그 코드를 캐싱하여, 같은 함수가 여러 번 불릴 때 매번 코드가 생성되는 것을 방지한다.
  
  </div>
  </details>
  
  <details>
  <summary>JNI(JAVA Native Interface)란?</summary>
  <div markdown="11">

  JAVA에서 Native영역(C/C++)으로 들어가 호출 또는 Native(C/C++)에서 JAVA를 호출하는 Interface이다.  즉, Java와 Java 이외의 언어로 만들어진 어플리케이션이나 라이브러리가 상호작용할 수 있도록 연결시켜주는 인터페이스이다.<br>
JVM이 Native Method를 Runtime Data Area의 Native Method Stack에 적재할 수 있도록 한다.<br>
JNI가 JVM내에 포함됨으로써 JVM이 호스트 운영체제상의 입출력, 그래픽스, 네트워킹, 그리고 스레드와 같은 기능들을 작동하기 위한 로컬시스템호출(local system calls)을 수행할 수 있도록 한다.
  
  </div>
  </details>
  
  >[JVM 동작원리 및 기본개념](https://steady-snail.tistory.com/67)<br>
  >[자바가상머신, JVM(Java Virtual Machine)이란 무엇인가?](https://asfirstalways.tistory.com/158)<br>
  >[자바의 동작과정 Java Compiler와 JVM](https://kingofbackend.tistory.com/123)<br>
  >[Java 클래스로더 훑어보기](https://homoefficio.github.io/2018/10/13/Java-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%8D%94-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0/)<br>
  >[스택 기반 VM과 레지스터 기반 VM](https://www.korecmblog.com/jvm-stack-and-register/)<br>
  
### GC(Garbage Collector)의 종류와 동작 과정/원리

- Garbage Collection(가비지 컬렉션)란?<br>
유효하지 않은 메모리, 즉 주소를 잃어버려서 사용할 수 없는 메모리를 Garbage라고 하는데, Garbage Collector는 메모리가 부족할 때 이런 Garbage를 메모리에서 해제시켜 다른 용도로 사용할 수 있게 해주는 프로그램을 말한다.<br>
GC가 수행될 땐 CG를 수행하는 스레드를 제외한 모든 스레드들이 작업을 멈추고, 이후 완료되면 작업을 다시 시작하게 된다.<br>
C/C++은 사용자가 메모리를 직접 해제해줘야 하지만, JAVA에서는 GC가 이 작업을 대신 수행해준다. 주의할 점은 메모리 누수까지 잡아주지는 않는다

- Garbage Collection 종류 - Minor GC, Major GC <br>
JVM의 Heap 영역은 처음 설계될 때 다음의 2가지를 전체로 설계되었다.
  - 대부분의 객체는 금방 접근 불가능한 상태(Unreachable)가 된다.
  - 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다.
  
  즉, 객체는 대부분 일회성이며, 메모리에 오랫동안 남아있는 경우는 드믈다는 것이다. 그렇기 때문에 객체의 생존 기간에 따라 물리적인 Heap 영역을 나누게 되었는데, Young, Old 총 2가지 영역이다.
  - Young 영역
    - 새롭게 생성된 객체가 할당(Allocation)되는 영역이다.
    - 대부분의 객체가 금방 Unreachable 상태가 되기 때문에, 많은 객체가 Young 영역에서 생성되었다가 사라진다.
    - Young 영역에 대한 가비지 컬렉션(Garbage Collection)을 Minor GC라고 한다.
  - Old 영역
    - Young 영역에서 Reachable 상태를 유지하여 살아남은 객체가 복사되는 영역
    - 복사되는 과정에서 대부분 Young 영역보다 크게 할당되며, 크기가 큰 만큼 가비지는 적게 발생한다.
    - Old 영역에 대한 가비지 컬렉션(Garbage Collection)을 Major GC 또는 Full GC라고 한다.
    
  예외적인 상황으로 Old영역에 있는 객체가 Young 영역의 객체를 잠조하는 경우도 존재하는데, 이런 경우를 대비해서 Old 영역에는 512Byte의 덩어리로 되어 있는 카드 테이블이 존재한다. 이 테이블에는 Old 영역에 있는 객체가 Young 영역의 객체를 참조할 때 마다 그에 대한 정보가 표시된다. 이 테이블의 존재 이유는 Minor GC가 실행 될 때, 모든 Old 객체를 검사하여 Young 영역에 있는 참조하지 않는 객체를 찾아내는 것은 비효율적이기 때문에, 카드 테이블만 조회하여 GC의 대상인지 식별하기 위함이다.
  
- Garbage Collection의 동작 방식 - 공통 동작 <br>
    1. Stop The World<br>
    GC가 실행되기 위해서는 JVM이 애플리케이션의 실행을 멈추는 작업이다. GC가 실행 될 때는 GC를 실행하는 쓰레드를 제외한 모든 쓰레드들의 작업이 중단되야 한다.(GC의 성능 개선을 위해 튜닝을 하게 된다면 이 과정을 줄이는 것이 최우선이다.)
    2. Mark and Sweep<br>
       - Mark: 사용되는 메모리와 사용되지 않는 메모리를 식별하는 작업
       - Sweep: Mark 단계에서 사용되지 않음으로 식별된 메모리를 해제하는 작업<br>
      
     GC는 스택의 모든 변수 또는 Reachable 객체를 스캔하면서 각각이 어떤 객체를 참고하고 있는지 탐색한다. 그리고 사용되고 있는 메모리를 식별하는데, 이러한 과정을 Mark라 하고 Mark가 되지 않은 객체를 메모리에서 제거하는 것을 Sweep이라 한다.
     
- Garbage Collection의 동작 방식 - Minor GC <br>
Young 영역은 1개의 Eden 영역과 2개의 Survivor 영역 총 3가지로 나뉜다.
   - Eden 영역 : 새로 생성된 객체가 할당(Allocation)되는 영역
   - Survivor 영역 : 최소 1번의 GC 이상 살아남은 객체가 존재하는 영역
  
  Young 영역의 동작 순서
     1. 새로 생성된 객체가 Eden 영역에 할당된다.
     2. 객체가 계속 생성되어 Eden 영역이 꽉차게 되고 Minor GC가 실행된다.
       - Eden 영역에서 사용되지 않는 개체의 메모리가 해제된다.
       - Eden 영역에서 살아남은 객체는 1개의 Survivor 영역으로 이동된다.
     3. 1~2번의 과정이 반복되다가 Survivor 영역이 가득 차게 되면 Survivor 영역의 살아남은 객체를 다른 Survivor 영역으로 이동시킨다.(1개의 Survivor 영역은 반드시 빈 상태가 된다.)
     4. 이러한 과정을 반복하여 계속해서 살아남은 객체는 Old 영역으로 이동(Promotion)된다.<br>

  <details>
  <summary>Promotion 여부 결정</summary>
  <div markdown="12">

  Minor GC에서 객체가 살아남은 횟수를 의미하는 age를 Object Header에 기록한다. 그리고 이 age는 Promotion 여부를 결정하게 된다.
  
  </div>
  </details>
  
  <details>
  <summary>Eden 영역에 객체를 빠르게 할당하는 두가지 방법</summary>
  <div markdown="13">

  HotSpot JVM에서는 Eden에 객체를 빠르게 할당하기 위해 ‘bump the pointer’와 TLABs(Thread-Local-Allocation Buffers)라는 기술을 사용한다.<br>
    
    - bump the pointer : Eden 영역에 마지막으로 할당된 객체의 주소를 캐싱해두었다가 새로운 객체를 할당할 때, 캐싱해 놓은 주소의 다음 주소를 사용함으로서 속도를 높이는 방법이다.
 
    - TLABs : 멀티쓰레드 환경에서는 Eden 영역에 할당할 때 락(Lock)을 걸어 동기화를 해줘야하는데 HotSpot JVM에서 이 문제를 해결하기 위해서 각각의 쓰레드마다 Eden에 할당할 수 있는 주소를 제한함으로써 동기화 작업 없이 빠르게 메모리를 할당하도록 하는 기술이다. 각각의 쓰레드는 자신이 갖는 주소에만 객체를 할당함으로써 동기화 없이 bump the pointer를 통해 빠르게 객체를 할당할 수 있게된다.
    
  
  </div>
  </details>

- Garbage Collection의 동작 방식 - Major GC <br>
Major GC는 객체들이 계쏙 Promotion되어 Old 영역의 메모리가 부족해지면 발생하게 된다. Young 영역은 일반적으로 Old 영역보다 크기가 작기 때문에 GC가 보통 0.5초 1초 사이에 끝나지만 Old 영역은 Young 영역보다 크며 Young 영역을 참조할 수 도 있기 때문에 일반적으로 10배 이상의 시간이 사용된다.

- Garbage Collection의 알고리즘 - Serial GC <br>
Old 영역에서는 Mark Sweep Compact 알고리즘이 사용된다. 기존의 Mark Sweep에 Compact라는 작업이 추가된 것으로 Compact는 Heap 영역을 정리하기 위한 단계로 유용한 객체들이 연속되게 쌓이도록 힙의 가장 앞 부분부터 채워서 객체가 존재하는 부분과 객체가 존재하지 않는 부분으로 나누는 것이다.<br>
Serial GC는 서버의 CPU 코어가 1개일 때 사용하기 위해 개발되었으며, 모든 GC를 처리하기 위해 1개의 쓰레드만을 이용한다. 그렇기 때문에 CPU의 코어가 여러 개인 운영 서버에서 Serial GC를 사용하는 것은 반드시 피해야한다.

- Garbage Collection 알고리즘 - Parallel GC <br>
기본적인 처리 과정은 Serial GC와 동일하다. 다른 점은 여러개의 쓰레드를 통해 Parallel하게 GC를 수행함으로써 GC의 오버헤드를 상당히 줄여준다. Parallel GC는 멀티 프로세서 또는 멀티 쓰레드 머신에서 중간 규모부터 대규모의 데이터를 처리하는 애플리케이션을 위해 고안되었다.

- Garbage Collection 알고리즘 - G1(Garbage First) GC <br>
장기적으로 문제를 일으킬 수 있는 CMS GC를 대체하기 위해 개발되었고, Java7부터 지원되기 시작했다.<br>
기존의 GC알고리즘은 Heap 영역을 물리적으로 Young 영역과 Old 영역으로 나누었는데, G1 GC는 물리적으로 메모리 공간을 나누지 않고 Region(지역)이라는 개념을 도입하여 Heap을 균등하게 여러 개의 지역으로 나누고, 각 지역을 역할과 함께 논리적으로 구분하여 객체를 할당한다.<br>
G1 GC의 핵심은 Heap을 동일한 크기의 Region으로 나누고, 가비지가 많은 Region에 대해 우선적으로 GC를 수행하는 것이다.

  ![image](https://user-images.githubusercontent.com/82690689/153128924-b57c6f62-bb45-444c-9c58-f0dbcc12f205.png)

    - Humongous : Region 크기의 50%를 초과하는 객체를 저장하는 Region을 의미한다.
    - Available/Unused : 사용되지 않는 Region을 의미한다.
    
  <details>
  <summary>G1GC Minor GC</summary>
  <div markdown="14">

    한 지역의 객체를 할당하다가 해당 지역이 꽉차면 다른 지역에 객체를 할당하고, Minor GC가 실행된다. G1 GC는 각 지역을 추적하고 있기 때문에, 가비지가 가장 많은(Garbage First) 지역을 찾아서 Mark and Sweep을 수행한다.<br>
    Eden 지역에서 GC가 수행되고 살아남은 객체를 다른 지역으로 이동하게 된다. 복제되는 지역이 Available/Unused 지역이면 해당 지역은 이제 Survivor 영역이 되고, Eden 영역은 Available/Unused 지역이 된다.
  
  </div>
  </details>
  
  <details>
  <summary>G1GC Major GC</summary>
  <div markdown="15">

    객체가 너무 많아 빠르게 메모리를 회수할 수 없을 때 Major GC(Full GC)가 실행된다.<br>
    기존의 다른 GC 알고리즘은 모든 Heap 영역에서 GC가 수행되었으며, 그에 따라 처리 시간이 상당히 오래 걸렸다. 하지만 G1 GC는 어느 영역에 가비지가 많은지 알고 있기 때문에 GC를 수행할 지역을 조합하여 해당 지역에 대해서만 GC를 수행한다. 그리고 이러한 작업은 Concurrent하게 수행된다.
    
  </div>
  </details>
  
>[다양한 종류의 Garbage Collection(가비지 컬렉션) 알고리즘](https://mangkyu.tistory.com/119)<br>
>[Garbage Collection(가비지 컬렉션)의 개념 및 동작 원리](https://mangkyu.tistory.com/118?category=872426)
  
### JAVA 언어 기초

<details>
<summary>정적 타입 언어와 동적 타입 언어의 차이</summary>
<div markdown="16">

  - 정적 타입 언어 (Statically typed language)<br>
  컴파일 시 변수의 타입(자료형)이 결정되는 언어를 말한다. 따라서, 개발자가 변수에 들어갈 값의 형태에 따라 직접 변수의 타입을 명시해줘야 한다.<br>
  타입 에러로 인한 문제점을 초기에 발견할 수 있어 안정성이 높고, 실행속도가 빠르지만, 매번 코드 작성시 변수형을 결정해줘야하는 번거로움이 있다.
  
  - 동적 타입 언어 (Dynamically typed languages)<br>
  컴파일 시 자료형을 정하는 것이 아니라 런타임 시 결정된다. 따라서, 타입 없이 변수만 선언하여 값을 지정할 수 있다.<br>
  타입 결정에 대해 유연성이 높고 컴파일 시 타입을 명시해주지 않아도 되기 때문에 빠르게 코드를 작성할 수 있지만, 실행 도중 변수에 예상치 못한 타입이 들어와 타입에러가 발생할 수 있다.

</div>
</details>

<details>
<summary>Java 코드의 컴파일 과정</summary>
<div markdown="17">

  1. 모든 소스코드는 .java 포맷의 파일로 작성된다.
  2. javac 컴파일러는 자바코드를 .class파일로 컴파일한다. .class 파일은 JVM이 이해할 수 있는 바이트코드로 이루어진다.
  3. JVM의 인터프리터와 JIT 컴파일러는 바이트코드를 각 OS가 실행할 수 있는 기계어로 변환시킨다.
  4. 프로세서는 기계어에 따라 동작을 수행한다.
  
</div>
</details>

<details>
<summary>각 변수 타입이 몇 byte인지, primitive type과 reference type 인지</summary>
<div markdown="18">

  - 변수 타입
  ![image](https://user-images.githubusercontent.com/82690689/153129748-e293f5ee-5d79-44fd-a6aa-671c47a1c956.png)
  
  - 기본 데이터 타입(Primitive Data Type)<br>
  기본 타입의 크기가 작고 고정적이기 때문에 메모리의 Stack 영역에 저장된다.
    - 정수형 : byte, short, int, long
    - 실수형 : float, double
    - 논리형 : boolean(ture/false)
    - 문자형 : char
  
  - 참조 타입(Reference Data Type)<br>
    - class, array, interface, Enumeration
    - 기본형을 제외하고는 모두 참조형이다.
    - new 키워드를 이용하여 객체를 생성하여 데이터가 생성된 주소를 참조하는 타입이다.
    - String, StringBuffer, List, 개인이 만든 클래스 등
    - 참조 타입의 데이터의 크기가 가변적, 동적이기 때문에 동적으로 관리되는 Heap 영역에 저장된다.
    - 더 이상 참조하는 변수가 없을 때 GC에 의해 파괴된다.
    - 참조 타입은 값이 저장된 곳의 주소를 저장하는 공간으로 객체의 주소를 저장한다.
  
</div>
</details>

<details>
<summary>Overriding vs Overloading 개념과 활용</summary>
<div markdown="19">

  - 오버로딩(Overloading)<br>
  두 메서드가 같은 이름을 갖고 있으나 인자의 수나 자료형이 다른 경우<br>
  EX)
    - public int Article(int a) {...}
    - public int Article(int a, int b) {...}
    - public int Article(long a) {...}
  
  - 오버라이딩(Overriding)<br>
  상위 클래스의 메서드와 이름과 용례(signature)가 같은 함수를 하위 클래스에 재정의하는 것<br>
  상속 관계에 있는 클래스 간에 같은 이름의 메서드를 정의한다.<br><br>
  
  Ex) Cirlce에서 printMe() 메서드를 재정의한다.
  
  ```java
    public abstract class Shape {
    public void printMe() { System.out.println("shape"); }
  }
  public class Circle extends shape {
    private double rad = 5;
    @Override // 개발자의 실수를 방지하기 위해 @Override 어노테이션 쓰는 것을 권장
    public void printMe() { System.out.println("Circle"); }
  }
  ```
  
</div>
</details>

<details>
<summary>접근자 종류와 기능</summary>
<div markdown="20">

  - public <br>
    - 모든 패키지, 모든 클래스에서 접근을 허용한다.
  - protected <br>
    - 같은 패키지의 모든 클래스에 접근 허용한다.
    - 다른 패키지에 있어도 자식 클래스일 경우 접근 허용한다.
  - default <br>
    - 동일한 패키지 내에 있는 클래스만 접근 허용한다.
  - private <br>
    - 오직 해당 멤버를 선언한 클래스에서만 접근 허용한다.
  
</div>
</details>


<details>
<summary>final 키워드</summary>
<div markdown="21">

  - final <br>
    - 개념 : 변수나 메서드 또는 클래스가 ‘변경 불가능’하도록 만든다.
    - 기본(Primitive) 변수에 적용 시
      - 해당 변수의 값은 변경이 불가능하다.
    - 참조(Reference) 변수에 적용 시
      - 참조 변수가 힙(heap) 내의 다른 객체를 가리키도록 변경할 수 없다.
    - 메서드에 적용 시
      - 해당 메서드를 오버라이드할 수 없다.
    - 클래스에 적용 시
      - 해당 클래스의 하위 클래스를 정의할 수 없다.
  
  - finally <br>
    - 개념 : try/catch 블록이 종료될 때 항상 실행될 코드 블록을 정의하기 위해 사용한다.
    - finally는 선택적으로 try 혹은 catch 블록 뒤에 정의할 때 사용한다.
    - finally 블록은 예외가 발생하더라도 항상 실행된다.
      - 단, JVM이 try 블록 실행 중에 종료되는 경우는 제외한다.
    - finally 블록은 종종 뒷마무리 코드를 작성하는 데 사용된다.
    - finally 블록은 try와 catch 블록 다음과, 통제권이 이전으로 다시 돌아가기 전 사이에 실행된다.
  
  - finalize() 메서드 <br>
    - 개념: 쓰레기 수집기(GC, Garbage Collector)가 더 이상의 참조가 존재하지 않는 객체를 메모리에서 삭제하겠다고 결정하는 순간 호출된다.
    - Object 클래스의 finalize() 메서드를 오버라이드해서 맞춤별 GC를 정의할 수 있다.
      - protected void finalize() throws Throwable { // 파일 닫기, 자원 반환 등등 }
  
</div>
</details>

<details>
<summary>Generic의 개념</summary>
<div markdown="22">
  
  - 개념 : 모든 종류의 타입을 다룰 수 있도록 일반화된 타입 매개 변수(generic type)로 클래스나 메서드를 선언하는 기법
  - 처리 방법 : 타입제거(type erasure)라는 개념에 근거한다.
    - 소스 코드를 JVM이 인식하는 바이트 코드로 변환할 때 인자로 주어진 타입을 제거하는 기술
    - 제네릭을 사용한다고 크게 달라지는 것은 없다. 단지 코드를 좀 더 예쁘게 만든다.
  
</div>
</details>

>[WeareSoft/tech-interview 7. JAVA](https://github.com/WeareSoft/tech-interview/blob/master/contents/java.md)
