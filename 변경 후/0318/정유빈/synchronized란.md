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
