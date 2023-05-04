![image](https://user-images.githubusercontent.com/58407737/236123581-d65b2ce3-ed3e-4eb7-903c-345570dc422e.png)
</br>
- x86, AMD 등 (CPU 종류) 
- Windows, Linux, mac 등 (OS 종류)
 
# JVM (Java Virtual Machine)
## JVM이란?
- 자바 어플리케이션을 어느 CPU나 OS에서도 실행할 수 있게 지원하는 역할을 수행한다.
- Java와 OS 사이에서 중개자 역할을 한다.

</br>

### JAVA 프로그램 실행 단계 
![image](https://user-images.githubusercontent.com/58407737/236121418-7a0bf0f0-b7a0-4bba-b02b-15fdd5c9c338.png) 
![image](https://user-images.githubusercontent.com/58407737/236121556-192d28e0-0c0a-48a1-90c0-62dc37e71071.png)

</br>

![image](https://user-images.githubusercontent.com/58407737/236122938-507f7e15-bdf4-4e2a-8e07-abc80a26535a.png)

- Java 언어로 프로그래밍된 파일을 Java 컴파일러가 가상 기계어 파일인 Java 클래스 파일로 만든다. (소스 코드 -> Java 바이트 코드로 번역 )
- 이후, Java 바이트 코드를 JVM이 읽고 실행하게 된다.
- JVM은 OS나 CPU가 달라도 실행할 수 있도록 도와준다.

### 즉, JVM은 Java 클래스 파일을 로드하고 바이트 코드를 해석하며, 메모리 등의 자원을 할당하고 관리하며 정보를 처리하는 작업을 하는 프로그램이다. 
- OS는 JVM을 실행하고, JVM은 Java 프로그램을 실행한다. 


</br>

#### (조금 자세하게 들어가면)
1. 어플리케이션이 실행되면 JVM이 OS로부터 메모리를 할당 받는다.
-> JVM은 할당 받은 메모리를 용도에 따라 영역을 구분하여 관리한다.

2. 자바 컴파일러(javac.exe)가 자바 소스코드(.java)를 읽어 바이트 코드(.class)로 변환한다.

3. Class Loader를 통해 바이트 코드를 JVM으로 로딩한다.

4. 로딩된 바이트 코드는 Execution Engine을 통해 해석된다.

5. 해석된 바이트 코드는 Runtime Data Areas에 배치되어 실행된다. 
-> 실행되는 과정에서 GC와 같은 작업이 수행된다. </br>
->  *Runtime Data Area는 실제적인 메모리를 할당받아 관리하는 영역


</br>

## JVM 구조
![image](https://user-images.githubusercontent.com/58407737/236124515-36633b06-971b-48d7-afe1-6fce83eb04d0.png)

</br>

### 1. Class Loader
![image](https://user-images.githubusercontent.com/58407737/236127807-36547bb6-5d10-4bb5-bb6f-85e8699304b6.png)

- JVM 내로 바이트 코드(.class)를 로드하고, 링크를 통해 배치하는 작업을 수행하는 모듈이다.
- 로드된 바이트 코드들을 엮어서 JVM의 메모리 영역인 Runtime Data Areas에 배치한다.
- 클래스를 메모리에 올리는 로딩 기능을 한번에 메모리에 올리지 않고, 어플리케이션에서 필요한 경우 동적으로 메모리에 적재하게 된다. 
(런타임 시에 동적으로 클래스를 로드한다.)
- 클리스 파일 로딩
Loading -> Linking -> lnitialization

</br>

### 2.  Execution Engine
![image](https://user-images.githubusercontent.com/58407737/236125618-4d400a7c-e394-4342-8fd3-8cccfd7cd3d9.png)
</br>

- Runtime Data Area에 할당된 바이트 코드를 실행키는 주체이다.
- 코드를 실행하는 방식은 크게 2가지 방식이 존재한다.

### (1) Interpreter
- 바이트 코드를 해석하여 실행하는 역할을 수행한다.
- 다만 같은 메소드라도 여러번 호출될 때 매번 새로 수행해야한다.(단점) 

</br>

### (2) JIT(Just In Time) Compiler
![image](https://user-images.githubusercontent.com/58407737/236134597-af22470f-acc6-4bcb-adbf-e6b78f131a94.png)
- 자바가 다른 언어로 만들어진 어플리케이션과 상호작용을 할 수 있는 인터페이스를 제공한다.
- JVM이 native Method를 적재하고 수행할 수 있도록한다.
- 실질적으로 제대로 동작하는 언어는 C/C++ 이다. (다른 언어로 될 수 있지만 100% 호환되지는 않는다.) - C,C++만 100호환됨

</br>

- Interpreter의 단점 해소
- 반복되는 코드를 반견하여 전체 바이트 코드를 컴파일하고, 그것을 Native Code로 변경하여 사용한다.
* Native Code: 자바에서 부모가 되는 C언어나 C++, 어셈블리어를 의미

</br>

### (3) Garbage Collector
- 더이상 참조되지 않는 메모리 객체를 모아 제거하는 역할을 수행한다. (클래스 객체나 String 객체 등)
- 일반적으로 일정 영역이 차면 자동으로 실행되지만, 수동으로 실행하기 위해 'System.gc()' 를 사용할 수 있지만 사용을 지양함

</br>

### 3. Runtime Data Area
- 어플리케이션이 동작하기 위해 OS에서 할당받은 메모리 공간을 의미한다.
- 크게 5가지로 구성된다.

![image](https://user-images.githubusercontent.com/58407737/236129069-9bfe489f-312f-43b6-9284-628a4505057c.png)

#### (1) Method Area </br>
- static으로 선언된 변수들을 포함하여 Class 레벨의 모든 데이터가 이곳에 저장된다.
- JVM마다 단 하나의 Method Area가 존재한다. -> 다른 영역들은 Thread 마다 생성이 된다. 
- Method Area는 Runtime Constant Pool이라는 별도의 영역이 존재한다. (상수 자료형을 저장하여 참조하는 역할)
- 저장되는 정보 <br>
-- Field Info: 멤버 변수의 이름, 데이터 타입, 접근 제어자의 정보 <br>
-- Method Info: 메소드 이름, Return 타입, 매개변수, 접근 제어자의 정보 <br>
-- Type Info: Class인지 Interface인지 여부 저장, Type의 속성, 이름, Super Class의 이름 <br>

#### Heap과 마찬가지로 GC 관리 대상임

</br>

#### (2) Heap Area </br>
![image](https://user-images.githubusercontent.com/58407737/236130760-7b8a04c6-83cf-44f8-8ab8-cc5795fb040e.png)
- 객체를 저장하기 위한 메모리 영역이다.
- new 연산자로 생성된 모든 Object와 Instance 변수, 그리고 배열을 저장한다.
- Heap 영역은 물리적으로 두 영역을 구분할 수 있음 (Young Generation, Old Generation)
- Garbage Collection 생명주기에 의해 지속적으로 메모리가 정리된다. (Major GC, Minor GC)
- Method Area와 Heap Area는 여러 스레드들 간에 공유되는 메모리이다.

</br>

#### (3) Stack Area </br>
![image](https://user-images.githubusercontent.com/58407737/236132740-6b4109ac-df17-4778-aeda-a71463bee93d.png)
- 각 스레드를 위한 분리된 Runtime Stack 영역이다.

<br>

![image](https://user-images.githubusercontent.com/58407737/236133411-9c1f3bf6-48df-4340-8acc-8eba8d70ca9a.png)

- 메소드를 호출할 때 마다 Stack Frame(메서드만을 위한 공간)으로 불리는 Entry가 Stack Area에 생성된다.
- 각종 형태의 변수나 임시 데이터, 스레드 또는 메소드의 정보를 저장한다. (매개변수, 지역변수, 리턴 값 및 연산 시 일어나는 값들을 임시로 저장한다.)
- 스레드의 역할이 종료되면 바로 소멸되는 특성의 데이터를 저장한다.

</br>

##### (4) PC Register </br>
![image](https://user-images.githubusercontent.com/58407737/236133557-781679fe-5229-4e25-b580-b1da1c29dc5a.png)
- Program Counter 약자
- 각 Thread가 시작될 때 생성되며, 현재 실행중인 상태 정보를 저장하는 영역이다.
- Thread가 로직을 처리하면서 지속적으로 갱신된다.
- THread가 생성될 때마다 하나씩 존재한다.
- 어떤 명령을 실행해야 할지에 대한 기록을 한다.(현재 수행 중인 JVM 명령의 주소를 가진다.)

</br>

##### (5) Native Method Stack </br>
![image](https://user-images.githubusercontent.com/58407737/236134206-a0d69fa1-f8a1-4ea4-becd-4552674cb181.png)
- 바이트 코드가 아닌 실제 실행할 수 있는 기계어로 작성된 프로그램을 실행 시키는 영역이다.
- Java가 아닌 다른 언어로 작성된 코드를 위한 영역이다.
- Java Native Interface를 통해 바이트 코드로 전환하여 저장한다.
- 각 스레드 별로 생성된다.






</br>
</br>

참고자료 </br>
https://www.youtube.com/watch?v=zta7kVTVkuk&t=72s </br>
https://steady-coding.tistory.com/305 </br>
