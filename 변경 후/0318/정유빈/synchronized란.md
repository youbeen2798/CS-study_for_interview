- 멀티 스레드를 잘 사용하면 프로그램적으로 좋은 성능을 낼 수 있지만, 멀티 스레드 환경에서 반드시 고려해야 할 점인 스레드간 동기화 문제는 꼭 해결해야 합니다.
- 예를 들어, 스레드간 서로 공유하고 수정할 수 있는 data가 있는데 스레드 간 동기화되지 않은 상태에서 멀티 스레딩 프로그램을 돌리면, data의 안전성과 신뢰성을 보장할 수 없습니다.


- 따라서 data의 thread-safe를 하기 위해 자바에서는 <b> synchronized 키워드를 통해 스레드 간 동기화를 시켜 data의 thread-safe를 가능하게 합니다. </b>
- 자바에서 지원하는 synchronized 키워드는 여러 개의 스레드가 한 개의 자원을 사용하고자 할 때, <b> 현재 데이터를 사용하고 있는 해당 스레드를 제외하고 나머지 스레드들은 데이터에 접근할 수 없도록 막는 개념입니다. </b>
<br />
- synchronized 키워드는 변수와 함수를 사용해서 동기화 할 수 있습니다.
- 하지만 synchronized 키워드를 너무 남발하면 오히려 프로그램 성능 저하를 일으킬 수 있습니다.
- 그 이유는 synchronized 키워드를 사용하면 자바 내부적으로 메소드나 변수에 동기화를 하기 위해 block과 unblock 처리를 하여 프로그램 성능 저하가 일어날 수 있습니다.
- 따라서 적재적소에 synchronized 키워드를 사용하는 것이 중요합니다.

1. 메소드에서 사용하는 경우

- public synchronized void method

2. 객체 변수에 사용하는 경우(block문)

- private Object obj = new Object();
- public void exampleMethod (){ synchronized(obj) }
