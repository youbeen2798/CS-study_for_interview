프로그래밍 언어엔 메모리를 프로그래머가 직접 관리해주는 **unmanaged** 언어와 언어단에서 관리해주는 **managed** 언어가 있다. </br>
#### unmanaged: C/C++
#### managed : Java, C#,Python 

- C언어나, C++언어를 이용하면 직접 delete나 free()를 통해 해제시켜줘야하한다.
- Java는 개발자가 직접 해제 시키지 않고 Garbage Collector가 존재해서 GC가 메모리를 자동적으로 관리해준다. (참조하지 않은 데이터를 지움으로써, 메모리 누수를 방지해준다.)


</br>

# Garbage Collection
![image](https://user-images.githubusercontent.com/58407737/235329656-ece2ea96-a33d-4c65-8da5-3d7752fd0eed.png)

- 쓰레기를 정리하는 작업이다.
- Java 프로그래밍을 할 때 쓰레기란? 객체를 의미한다.
- new라는 키워드가 Heap 영역에 동적으로 메모리를 할당해주는 역할을 하고, 그렇게 동적으로 할당된 메모리를 자동으로 해제해주는 것이 GC이다.
- JVM 메모리 중 Heap 영역에 사용하지 않는 객체를 삭제해준다.
</br>

- Java에서는 개발자가 프로그램 코드로 메모리를 명시적으로 해제하지 않기 때문에 GC가 더이상 필요없는 객체(쓰레기)를 찾아 지우는 작업을 한다.
</br>

- Java에서는 메모리를 GC라는 알고리즘을 통해 관리하기 때문에, 개발자가 메모리를 처리하기 위한 로직을 만들 필요가 없고, 절대로 만들어서는 안 된다.
- System.gc()를 호출해 직접 관리 해줄 수 있지만, 해당 메소드 호출은 시스템 성능에 매우 큰 영향을 미친다.</br>
-> 상당히 오래걸린다. </br>
-> 쓸데없는 작업을 계속 하기 때문이다. </br>
-> 가비지를 탐색하고, 정리하는 작업은 꽤나 무거운 작업이기 때문에 이 메서드 자체를 호출하는 것은 오버헤드가 크다.  </br>
-> gc에게 맡기도록 한다.

</br>

### 자바의 시스템 구조 
![image](https://user-images.githubusercontent.com/58407737/235330224-8cbac2a1-b8ab-49b2-aba5-45621c599ad2.png)


</br>

## 언제 동작하는가?
- GC도 결국엔 JVM에 올라가기 때문에 기본적으로 **Runtime** 에동작한다.
- 가비지 컬렉션이 실행되기에는 몇가지 조건이 있는데, 다음 조건 중 하나라도 충족되면 JVM은 GC를 실행한다.

1. OS로부터 할당 받은 시스템의 메모리가 부족할 경우
2. 관리하고 있는 힙에서 사용되는 메모리가 허용된 임계값을 초과하는 경우
3. 프로그래머가 직접 GC를 실행하는 경우(Java는 System.gc() 메서드 있는데 권장 x: 이유는 위에)

</br>

## GC가 만들어진 이유?
두가지 가설(전제 조건)하에 만들어졌다.

### 1. 대부분의 객체는 금방 접근 불가능 상태(unreachable)
### 2. 오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재한다.

이러한 가설을 weak generational hypothesis라 한다. </br>
이 가설의 장점을 최대한 살리기 위해서 HotSpot VM에서는 크게 2개로 물리적 공간을 나누었다.
- Young 영역, Old 영역

</br>

## 해제할 동적 메모리 영역들을 어떻게 알아서 판단할까?
GC를 구현하는 대표적인 알고리즘 </br>
 
* Root Space: 스택 변수, 전역 변수 등 heap 영역 참조를 담는 변수 </br>


### 1. Reference Counting
![image](https://user-images.githubusercontent.com/58407737/235330765-5d40e254-0ca1-465c-a179-fa0e78d72bac.png)

- Heap Space에 선언된 객체들이 각각 Reference count라는 별도의 숫자를 가지고 있다.
- Reference count가 0에 다다르면 가비지 컬렉션 대상이 된다.

### 한계점: 순환참조
- Root Space에서 Heap Space 연결 부분을 다 끊는다 해도 2 1 1 count를 갖는 부분은 서로가 서로를 참조하고 있어 Reference count는 1로 유지한다.

![image](https://user-images.githubusercontent.com/58407737/235330840-438e8c5b-a18e-4aba-834f-b839c2eeaa9a.png)
- a로부터 참조가 끊어져도 다른 노드로부터의 참조가 남아있기 때문에 Reference count가 0이 되지 않고, Garbage 대상이 되지 않아 메모리 누수로 이어진다.

- 이 방식은 각 객체마다 Reference Count를 변경해줘야 하기 때문에 그에 대한 관리 비용이 크고, 참조를 많이 하고 있는 객체의 Reference Count가 0이 될 경우 연쇄적으로 GC가 발생할 수 있는 문제가 있다. 

### 즉, 사용하지 않은 메모리 영역이 해제되지 못하고 Memory Leak 발생

</br>


어떤 객체에 유효 참고가 존재하면 **Reachable**, 그렇지 않으면 **Unreachable**
![image](https://user-images.githubusercontent.com/58407737/235330966-c1a6ec40-6cbe-4ffb-821e-08288f06898f.png) </br>

### GC 조건들
- Stack 영역의 데이터들 (지역변수, 중간 연산 결과들이 저장)
- Method 영역의  static 데이터들(전역)
- JNI에 의해 생성된 객체 들

![image](https://user-images.githubusercontent.com/58407737/235331000-9810efb8-c24f-4cd6-9a42-d5ad8bed4fbd.png) </br>

2번은 Unreachable함 -> GC 수거 대상

</br>

### 2. Mark And Sweep
### Mark
GC는 GC Root로부터 모든 변수를 스캔하면서 각각 어떤 객체를 참조하고 있는지 찾아서 마킹한다. => Reachable한 객체와 UnReachable한 객체 식별한다.

### Sweep
UnReachable 객체들을 Heap에서 제거한다.

</br>

알고리즘에 따라서 Compact 과정이 추가되기도 한다. </br>

![image](https://user-images.githubusercontent.com/58407737/235331133-763291ac-8e8a-4c0d-bbab-9385933dec55.png)

Sweep후에 분산된 객체들을 Heap의 시작 주소로 모아 메모리가 할당된 부분과 그렇지 않은 부분으로 나눈다( 메모리 단편화 막아줌)


### 특징
- 의도적으로 GC를 실행시켜야 한다.
- 어플리케이션 실행과 GC 실행이 병행된다.

</br>

## Heap의 구조
![image](https://user-images.githubusercontent.com/58407737/235331150-8efb172d-701c-4eec-9663-5148769d89f5.png)

- Young Generation에서 발생하는 GC => Minor GC
- Old Generation에서 발생하는 GC => Major GC

</br>

### Eden 영역
- 새롭게 생성된 객체들이 할당되는 영역

### Survival 영역
- Minor GC로부터 살아남은 객체들이 존재하는 영역

</br>

### 특별한 규칙
- Survival 0 또는 Survival 1은 꼭 비어있어야 한다.

</br>

## 실행 과정
![image](https://user-images.githubusercontent.com/58407737/235331232-d862f68f-4c65-4ea2-a7d3-80209c7d5a99.png)
### 1. Eden 영역에 새로운 객체들이 찬다.

### 2. 꽉차게 되면 Minor GC가 일어나 Mark & Sweep을 진행한다.

![image](https://user-images.githubusercontent.com/58407737/235331274-847edd90-0307-4b30-ab0b-a04d41c96271.png)
### 3. Root로부터 Reachable이라고 판단되는 객체는 Survival 0 영역으로 옮겨진다. (이때 Survival 0부터 넣어있는데 Survival 1에 들어가 있어도 상관 없음)

### 4. 그래서 Survival 0에 객체들들이 0 -> 1로 숫자가 증가한다.(= age-bit), 살아 남을때마다 1씩 증가한다. </br>
이러한 과정들이 반복 된다. </br>

![image](https://user-images.githubusercontent.com/58407737/235331310-d104b7f0-de6c-47bc-bc01-0e5a752e2ee4.png)
### 5. 그 후 오래 살아남은 객체의 age-bit가 JVM GC에서 특정 임계치에 도달하게 되면 오래도록 참조될 객체구나 판단하고 

![image](https://user-images.githubusercontent.com/58407737/235331317-874cc137-9dc2-41ef-9bd3-fa8458dcddb0.png)
### 6. 해당 객체를 Old Generation에 넘겨 준다. => Promotion
이러한 과정들이 반복된다.  </br>

### 7. Old generation이 다 채워지면 Major GC가 발생한다.

### 8. Mark and Sweep 방식을 통해 필요없는 메모리 비워준다.

### 9. Major GC는 Minor GC보다 더 오래 걸린다.


</br>

Minor GC가 빈번하게 일어나는게 오히려 메모리 낭비를 막을 수 있다.  </br>
그래서 Eden 영역과 2개의 Survival 영역으로 나눴다. </br>
(Young Generation 안에서 최대한 처리하도록)

Young이 Old 영역보다 비율이 훨씬 적다. 

### Stop - the - world
-> GC를 실행하기 위해 JVM이 어플리케이션 실행을 멈추는 것(Stop the world 시간을 최소화 하는게 최적화 작업)

</br>

## GC 종류
- Old 영역은 기본적으로 데이터가 가득 차면 GC가 실행된다.
- GC방식에 따라 처리 절차가 달라진다.
- 운영 서버에서 절대 사용하면 안 되는 방식이 Serial GC이다.
-> Serial GC는 데스크톱의 CPU 코어가 하나만 있을 떄 사용하기 위해 만든 방식이다. Serial GC를 사용하면 애플리케이션의 성능이 많이 떨어진다.


### Serial GC
    
![image](https://user-images.githubusercontent.com/58407737/235331524-6366811e-23d8-46b3-a975-42d672b2cbbf.png) 

- GC를 처리하는 쓰레드가 1개 (싱글 쓰레드)
- 다른 GC에 비해 stop-the-world 시간이 김
- 싱글 스레드 환경 및 Heap이 매우 작을 때 사용

</br>

### Parallel(페러랠즈) GC

![image](https://user-images.githubusercontent.com/58407737/235331542-8f4431a7-e772-4c8b-b07d-ba842a968349.png)

- 여러 개의 쓰레드로 GC를 실행 (stop-the-world 시간도 짧아짐)
- 멀티코어 환경에서 사용
- Java 8의 default GC 방식
-> age bit가 15가 되면 promotion이 진행됨

</br>

### CMS GC    

![image](https://user-images.githubusercontent.com/58407737/235331568-a0b73881-18e6-4ea9-9eca-33f1a56af330.png)    

- Stop the world 최소화를 위해 고안
- GC 작업을 어플리케이션과 동시에 실행
- Recharble한 객체를 순차적으로 찾음
- 메모리와 CPU를 많이 사용, Mark-And-Sweep 과정 이후 메모리 파편화를 해결하는 Compaction이 기본적으로 제공 X
- G1 GC 등장에 따라 Deprecated

</br>

### G1 GC
    
![image](https://user-images.githubusercontent.com/58407737/235331584-5e8a097f-752f-495e-9f1d-0f483f66b0f9.png)
    
- Garbage First (G1)
- Heap을 일정크기의 Region으로 나누어 사용
-> 어떤 영역은 Young Generation / 어떤 영역은 Old Generation으로 활용
-> 런타임의 G1 GC가 필요에 따라 영역별 Region 개수를 튜닝함 → 그에 따라 Stop the world를 최소화 할 수 있음 (할당된 region에 개수에서만 찾음)
- Java 9부터 default GC 방식

