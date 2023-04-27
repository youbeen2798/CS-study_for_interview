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

