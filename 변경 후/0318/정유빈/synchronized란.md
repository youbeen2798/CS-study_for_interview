<h1> Synchronized method </h1>

- 클래스 인스턴스에 lock을 거는 것
- 아래는 두 개의 스레드에서 하나의 인스턴스에 접근하는 상황이다.

```
public class Main {

    public static void main(String[] args) {
        A a = new A();
        Thread thread1 = new Thread(() -> {
            a.run("thread1");
        });

        Thread thread2 = new Thread(() -> {
            a.run("thread2");
        });

        thread1.start();
        thread2.start();
    }
}
```

```
public class A {

    public synchronized void run(String name) {
        System.out.println(name + " lock");
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(name + " unlock");
    }
}
```

```
// 출력 결과
thread1 lock
thread1 unlock
thread2 lock
thread2 unlock
```
접근한 순서대로 lock를 획득하고 반납했기 떄문에 thread1, thread2가 차례대로 출력된다.

- 이번에는 스레드 2개가 각각의 다른 인스턴스에 접근하는 경우이다.
```
public class Main {

    public static void main(String[] args) {
        A a1 = new A();
        A a2 = new A();
        Thread thread1 = new Thread(() -> {
            a1.run("thread1");
        });

        Thread thread2 = new Thread(() -> {
            a2.run("thread2");
        });

        thread1.start();
        thread2.start();
    }
}
```
```
public class A {

    public synchronized void run(String name) {
        System.out.println(name + " lock");
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(name + " unlock");
    }
}
```
```
// 출력 결과
thread2 lock
thread1 lock
thread1 unlock
thread2 unlock
```

- 이 상황에서는 각 스레드가 서로 다른 인스턴스에 접근하기 때문에 lock을 공유하지 않는다는 것을 확인할 수 있습니다.
- 앞서 Synchronized method는 <b> 클래스 인스턴스 </b>에 lock을 건다고 표현했습니다.
- 이 의미가 '인스턴스 접근 자체에 lock을 걸리는 것인가'라고 이해할 수 있지만, 그렇지 않습니다.
- 한 번 만들어서 확인해봅시다.

```
public class Main {

    public static void main(String[] args) throws InterruptedException {
        A a = new A();
        Thread thread1 = new Thread(() -> {
            a.run("thread1");
        });

        Thread thread2 = new Thread(() -> {
            a.print("thread2");
        });

        thread1.start();
        Thread.sleep(500);
        thread2.start();
    }
}
```
```
public class A {

    public void print(String name){
        System.out.println(name + " hello");
    }

    public synchronized void run(String name) {
        System.out.println(name + " lock");
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(name + " unlock");
    }
}
```
```
// 출력
thread1 lock
thread2 hello
thread1 unlock
```
lock을 획득하는 thread1을 먼저 수행하고, thread가 진행되는 도중에 thread2에서 synchronized 키워드가 붙지 않는
