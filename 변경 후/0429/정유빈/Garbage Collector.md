<h1> 가비지 컬렉터 </h1>

- 프로그램을 개발하다 보면 유효하지 않은 메모리인 가비지(Garbage)가 발생하게 된다.
- C언어를 사용하면 free()라는 함수를 통해 직접 메모리를 해제해주어야 한다.
- 하지만 Java Kotlin을 이용해 개발을 하다보면 개발자가 메모리를 직접 해제해주는 일이 없다.
- 그 이유는 JVM의 가비지 컬렉터가 불필요한 메모리를 알아서 정리해주기 때문이다.
- 대신 Java에서 명시적으로 불필요한 데이터를 표현하기 위해 일반적으로 NULL을 선언해준다. 
- 예를 들어 아래와 같은 코드가 있다고 가정하자.

```java

Person person = new Person();
person.setName("Mang");
person = null;

// 가비지 발생
person = new Person();
person.setName("MangKyu");

```

- 기존에 Mang으로 생성된 person 객체는 더 이상 참조를 하지 않고 사용이 되지 않아서 Garbage(가비지)가 되었다.
- Java나 Kotlin에서는 이러한 메모리 누수를 방지하기 위해 가비지 컬렉터(Garbage Colletor, GC)가 주기적으로 검사하여 메모리를 청소해준다.
- 물론 Java에서도 System.gc()를 이용해 호출할 수 있지만, 해당 메소드를 호출하는 것은 시스템의 성능에 매우 큰 영향을 미치므로 절대 호출해서는 안 된다.

<h1> Minor GC와 Major GC </h1>

- JVM의 Heap 영역은 처음 설계될 때 다음의 2가지르 전제로 설계되었다.
  - 대부분의 객체는 금방 접근 불가능한 상태(Unreachable)가 된다.
  - 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다.

- 즉, <b> 객체는 대부분 일회성이며, 메모리에 오랫동안 남아있는 경우는 드물다 </b>는 것이다.
- 그렇기 때문에 객체의 생존 기간에 따라 물리적인 Heap 영역을 나누게 되었고 Young, Old 총 2가지 영역으로 설계되었다.
- 초기에는 Perm 영역이 존재했지만 Java8부터 제거되었다.

![image](https://user-images.githubusercontent.com/62228401/234888374-100ff1cb-5d03-44ae-820e-69083561abd5.png)

- Young 영역(Young Generation)
  - 새롭게 생성된 객체가 할당(Allocation)되는 영역
  - 대부분의 객체가 금방 Unreacable 상태가 되기 때문에, 많은 상태가 Young 영역에 생성되었다가 사라진다.
  - Young 영역에 대한 가비지 컬렉션(Garbage Collection)을 Minor GC라고 부른다.

- Old 영역(Old generation)
  - Young 영역에서 Reachable 상태를 유지하여 살아남은 객체가 복사되는 영역
  - Young 영역보다 크게 할당되며, 영역의 크기가 큰 만큼 가비지가 적게 발생한다.
  - Old 영역에 대한 가비지 컬렉션(Garbage Collection)을 Major GC 또는 Full GC라고 부른다.

- Old 영역이 Young 영역보다 크게 할당되는 이유는 Young 영역의 수명이 짧은 객체들은 큰 공간을 필요로 하지 않으며 큰 객체들은 Young 영역이 아니라 바로 Old 영역에 할당되기 때문이다.

- 예외적인 상황으로 Old 영역에 있는 객체가 Young 영역의 객체를 참조하는 경우도 존재할 것이다. 
- 이러한 경우를 대비하여 Old 영역에는 512 bytes의 덩어리(Chunk)로 되어 있는 카드 테이블(Card Table)이 존재한다.

![image](https://user-images.githubusercontent.com/62228401/234896377-e8d261bb-d7aa-4ea5-a42c-1421f23bdc12.png)

