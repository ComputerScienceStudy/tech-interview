## JVM 동작 과정/원리
### 핵심답변

<br><br>

## GC(Garbage Collector)의 종류와 동작 과정/원리
### 핵심답변

<br><br>

## 정적 타입 언어와 동적 타입 언어의 차이
### 핵심답변
정적타입 언어과 동적 타입 언어의 차이는 변수의 타입의 결정이 컴파일 과정에서 결정되는지, 런타임 과정에서 결정되는지의 차이입니다.       
정적타입 언어는 컴파일 때 변수의 타입이 결정되는 언어를 말합니다.               
따라서, 프로그래머가 변수에 들어갈 값의 형태에 따라 직접 변수의 타입을 명시해줘야 합니다.         
정적타입의 언어로는 Java, C, C++  등이 있습니다.           

동적타입 언어는 자료형이 런타임 때 결정됩니다.      
타입 없이 변수만 선언하여 값을 지정할 수 있습니다.           
동적타입 언어로는 Python, JavaScript, PHP 등이 있습니다.          

#### 🤔 각각의 장단점을 설명해주세요.
- 정적 타입 언어의 경우        
컴파일 때 미리 타입을 결정하기 때문에 실행속도가 빠르고 타입 에러로 인한 문제점을 초기에 발견할 수 있어 타입의 안정성이 높습니다.      
하지만, 매번 코드 작성시 변수형을 결정해줘야 하는 번거로움이 있습니다.        
- 동적 타입 언어의 경우            
런타임까지 타입에 대한 결정을 끌고 갈 수 있기 때문에 유연성이 높고,
컴파일시 타입을 명시해주지 않아도 되기 때문에 빠르게 코드를 작성할 수 있습니다.           
하지만, 실행 도중에 변수에 예상치 못한 타입이 들어와 타입에러가 발생할 수 있습니다.            
동적타입 언어는 런타임 시 확인할 수 밖에 없기 때문에, 코드가 길고 복잡해질 경우 타입 에러를 찾기가 어려워 집니다.

<br><br>

## Java 코드의 컴파일 과정
### 핵심 답변
Java 코드의 컴파일 과정을 다음과 같습니다.      
개발자가 자바 소스 코드를 작성하면,        
첫번째로, 자바 컴파일러가 자바 소스 파일을 컴파일 합니다.           
이때 나오는 파일은 자바 바이트 코드 파일로 아직 컴퓨터가 읽을 수 없는 자바 가상 머신이 이해할 수 있는 코드입니다.      
두번째로, 컴파일 된 바이트 코드를 JVM의 클래스 로더에게 전달합니다.      
세번째로, 클래스 로더는 동적로딩을 통해 필요한 클래스들을 로딩 및 링크하여 JVM의 런타임 데이터 영역에 올립니다.       
마지막으로 실행엔진은 JVM 메모리에 올라온 바이트 코드들을 명령어 단위로 하나씩 가져와서 실행합니다.       
이때, 실행엔진은 바이트 코드를 각 OS가 실행할 수 있는 기계어로 변환시킵니다.
<br><br>

#### 🤔 바이트 코드란?
바이트코드는 특정 하드웨어가 아닌 가상 머신에서 돌아가는 실행 프로그램을 위한 이진 표현법입니다.     
바이트 코드의 대부분 명령어는 0개 이상의 매개변수를 갖는 1바이트 크기를 가지고 있습니다.

#### 🤔 클래스로더 동작에 대해 구체적으로 설명해주세요.
클래스 로더의 세부 동작은 다음과 같습니다.      
가장 먼저, 클래스 파일을 가져와서 JVM의 메모리에 로드합니다.      
그 다음, 자바 언어 명세 및 JVM 명세에 명시된 대로 구성되어 있는지 검사합니다.          
검사 후에는, 필드, 메서드, 인터페이스 등 메서드클래스가 필요로 하는 메모리를 할당합니다.      
이 후, 클래스의 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경합니다.        
마지막으로 클래스 변수들을 적절한 값으로 초기화합니다.         

###### + 심볼릭 레퍼런스는 무엇인가요?
심볼릭 레퍼런스란 참조할 때, 클래스의 특정 메모리 주소를 참조 관계로 구성한 것이 아닌 참조하는 대상의 이름을 지칭합니다.       
Class 파일이 JVM에 올라가게 되면 심볼릭 레퍼런스는 그 이름에 맞는 객체의 주소를 찾아서 연결하는 작업을 수행합니다.         
그러므로, 실제 메모리 주소가 아니라 이름만을 가집니다.        

###### + 다이렉트 레퍼런스로 변경이라는 의미는?
실제 메모리 주소 값으로 변경해 주는 작업을 의미합니다.

#### 🤔 동적로딩이란 무엇인가요?
동적로딩은 프로그램을 실행할 때, 필요할 때마다 동적으로 메모리를 생성하고 필요없는 메모리는 자동으로 메모리에서 소멸시키는 것을 말합니다.       

#### 🤔 실행엔진은 어떻게 바이트 코드들을 실행하나요?
- 바이트코드 프로그램은 보통 한 번에 하나의 명령어를 읽은 후 실행합니다. 이러한 형태의 바이트코드 인터프리터는 높은 이식성을 갖습니다.               
- 또 다른 형태로는 저스트 인 타임 컴파일러라 불리는 시스템은 실행 중에 필요에 따라서 바이트코드를 기계어로 번역합니다. 이로 인해, 자바는 네이티브 언어와 유사한 수준의 퍼포먼스를 낼 수 있게 되었습니다.
<br><br>
  
## 각 변수 타입이 몇 byte인지, primitive type과 reference type 인지
### 핵심답변
- 기본 데이터 타입(Primitive Data Type)의
  - 종류는 byte, short, char, int, float, double, boolean이 있습니다.
    - 정수형 : byte, short, int, long `1, 2, 4, 8 byte`
    - 실수형 : float, double `4, 8 byte`
    - 논리형 : boolean(ture/false) `1 byte`
    - 문자형 : char `2 byte`
  - 기본 타입의 크기가 작고 고정적이기 때문에 메모리의 Stack 영역에 저장됩니다.
- 참조 타입(Reference Data Type)의
  - 종류는 class, array, interface, Enumeration이 있습니다.
  - 기본형을 제외하고는 모두 참조형입니다.
  - 참조 타입은 값이 저장된 곳의 주소를 저장하는 공간으로 `객체의 주소`를 저장합니다.  
  - 참조 타입은 `4 byte` 크기의 주소값이 들어갑니다.

#### 🤔 참조 타입에 대해 더 자세히 설명해주세요.
- 참조 타입은 보통 new 키워드를 이용하여 객체를 생성하여 데이터가 생성된 주소를 참조하는 타입입니다.
- 참조 타입의 데이터의 크기가 가변적, 동적이기 때문에 동적으로 관리되는 Heap 영역에 저장됩니다.
- 더 이상 참조하는 변수가 없을 때 가비지 컬렉션에 의해 파괴됩니다.
<br><br>

## overriding vs overloading 개념과 활용
### 핵심답변
- 오버라이딩은 부모 클래스가 가지고 있는 메서드를 자식 클래스에서 재정의해서 사용하는 기술을 말합니다. 
- 오버라이딩은 코드를 재사용하기 위해서 사용하는데요. 
- 자식 클래스가 부모 클래스를 상속 받아 중복 코드를 없애고, 자식 클래스마다 재정의가 필요한 부분만 오버라이딩하여 추가로 구현 할 수 있습니다.
- 오버로딩은 메서드의 이름은 동일하나 매개변수의 개수 또는 타입이 다르면 같은 이름을 재정의해서 사용할 수 있는 기술을 말합니다. 
- 오버로딩의 이점은 같은 기능을 하는 메서드를 하나의 이름으로 사용할 수 있다는 것입니다. 
- `System.out.println()`함수에서 오버로딩의 이점을 느낄 수 있었습니다.
  <br><br>

## 접근자 종류와 기능
### 핵심답변
- 접근 제어자는 멤버 변수/함수 혹은 클래스에 사용되며 외부에서의 접근을 제한하게 합니다.       
- 접근 제어자의 종류는 4가지 입니다. 
  - private는 같은 클래스 내에서만 접근이 가능하도록 하고, 
  - default는 같은 패키지 내에서만 접근이 가능하도록 합니다. 
  - protected는 같은 패키지 내에서, 그리고 다른 패키지의 자손클래스에서 접근이 가능하도록 하고 
  - public : 접근 제한이 전혀 없습니다.
- 접근 제어자를 사용하는 이유는 다음과 같습니다.
  - 객체지향 프로그래밍이란 객체들 간의 상호작용을 코드로 표현하는 것인데요.
  - 이때 객체들간의 관계에 따라서 접근 할 수 있는 것과 아닌 것, 권한을 구분할 필요가 생깁니다.
  - 클래스 내부에 선언된 데이터의 부적절한 사용으로부터 보호하기 위해서 접근 제어자를 사용합니다.
<br><br>

## final 키워드
### 핵심답변
final 키워드는 변수나 메서드 또는 클래스가 '변경 불가능' 하도록 만듭니다.   
final로 선언하면, 한번만 초기화가 가능하고,     
final 필드가 초기화 되면, 그 초기값이 최종적인 값이 되어 프로그램 실행 도중에 수정할 수 없습니다.     
클래스, 메서드, 변수가 변하지 않도록 하기 위해, 사용합니다.

#### 🤔 어떻게 변경되지 않는지 구체적으로 설명해주세요.
final 키워드를 원시 변수에 적용 시 해당 변수의 값은 변경이 불가능합니다.               
참조 변수에 적용 시 참조 변수가 힙(heap) 내의 다른 객체를 가리키도록 변경할 수 없습니다.          
메서드에 적용 시 해당 메서드를 오버라이드할 수 없습니다.        
클래스에 적용 시 해당 클래스의 하위 클래스를 정의할 수 없습니다.       
<br><br>

## Generic의 개념
### 핵심답변
제네릭스는 Java에서 컬렉션을 사용하면 자주 볼 수 있습니다.         
제네릭스는 꺽쇠를 사용하여 타입을 명시해 줌으로서, 컴파일 시에 객체의 타입을 체크하는 것을 말합니다.               
의도하지 않은 타입의 객체가 저장되는 것을 막고 잘못된 형변환을 막을 수 있기 때문에 안정성이 높아집니다.    

#### 🤔 제네릭스의 형식과 약어는?
###### 제네릭스의 형식
```java
public class 클래스명<T> {...}
public interface 인터페이스명<T> {...}
```
###### 제네릭스의 자주 사용되는 타입인자
```java
- <T> == Type
- <E> == Element
- <K> == Key
- <V> == Value
- <N> == Number
- <R> == Result
```
#### 🤔 제네릭스의 사용 예시
제네릭스를 가장 잘 사용한 예제는 바로 Collection으로 볼 수 있습니다.
```java
import java.util.ArrayList;
import java.util.Collection;
import java.util.List;

public class Main {
    public static void main(String[] args) {

        List<String> list = new ArrayList();
        Collection<String> collection = list;
    }
}
```
위의 collection의 경우,String type만을 담겠다고 명시하고, 
```java
public interface Collection<E> extends Iterable<E> {
    int size();
    boolean isEmpty();
    Iterator<E> iterator();
    boolean add(E e);
    <T> T[] toArray(T[] a);
    boolean containsAll(Collection<?> c);
    boolean addAll(Collection<? extends E> c);
}
```

#### 💡 제네릭스의 유용함
- 제네릭스를 활용하면 동작은 같지만 클래스 타입만 바뀌어야 하는 경우를 쉽게 다룰 수 있습니다. 
- 제네릭스를 통해 컴파일언어의 특징인 타입 안정성을 보장하면서도 유연한 프로그램을 작성할 수 있습니다.
<br><br>

## ThreadLocal이 무엇이고 언제 활용되는지
### 핵심답변