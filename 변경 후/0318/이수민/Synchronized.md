# Synchronized
Java는 크게 3가지 메모리 영역
1. static 영역
2. heap 영역
3. stack 영역


</br>

자바 멀티 스레드 환경에서는 스레드끼리 static 영역과 heap영역을 공유-> 공유 자원에 대한 동기화 문제를 신경 써야 한다.
원자성을 해결하기 위한 방법 -> Synchronized

### Synchronized는 lock을 이용해 동기화를 수행하며 4가지의 사용 방법이 존재한다.

## 1. synchronized method
- 동기화를 시키고 싶은 클래스의 메소드에 synchronized 키워드를 붙이면 되고, synchronized method는 인스턴스 단위의 synchronized 키워드가 붙은 메소드에 대해서만 lock 공유한다. 

## 2. static synchronized method
- static synchronized method는 인스턴스가 아닌 클래스 단위로 lock을 공유하며, synchronized method와 동일하게 함수 간의 동기화가 발생한다. 
- 만약 synchronized method과 함께 사용되면 인스턴스 락과 클래스 락은 공유가 안 되기 때문에 동기화 이슈가 발생할 수 있다

## 3. synchronized block
- synchronized block은 block 단위로 lock을 걸며 2가지 사용 방법이 있따.
1. synchronized의 인자 값에 this를 사용하는 방식이다. </br>
이 방식은 여러 스레드가 들어와 서로 다른 block을 호출해도  this를 사용해 자기 자신에 lock을 걸었기 떄문에 기다려야한다. </br>

2. synchronized의 인자값에 object를 사용하는 방식이다. </br>
이 방식은 block마다 서로 다른 lock을 걸리게해 훨 씬 효율적인 코드를 작성할 수 있다.

## 4. static synchronized block
- static synchronized method 방식과 차이는 lock객체를 지정하고 block으로 범위를 한정지을 수 있따는 점이다.
- 클래스 단위로 lock을 공유한다는 점은 같다.
