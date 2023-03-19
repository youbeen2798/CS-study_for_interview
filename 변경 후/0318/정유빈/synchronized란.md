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
- lock을 획득하는 thread1을 먼저 수행하고, thread가 진행되는 도중에 thread2에서 synchronized 키워드가 붙지 않은 print 메소드를 호출하도록 했습니다.
- 출력 결과를 보면 중간에 hello가 찍힌 것을 확인할 수 있습니다.
- <b> 즉, 인스턴스 접근 자체에 lock이 걸린 것은 아닌 것을 확인할 수 있습니다. </b>
<br>

- 그렇다면, print 메소드에도 synchronized 키워드를 붙이면 어떻게 될까?

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

    public synchronized void print(String name){
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
// 출력 결과
thread1 lock
thread1 unlock
thread2 hello
```
- synchronized를 붙였더니 앞선 결과와 다르게 thread2는 thread이 lock을 해제하고 나서야 찍힌 것을 확인할 수 있었습니다.
- 즉, 동기화가 발생했습니다.
- <b> 정리하자면, 인스턴스에 lock을 거는 synchronized 키워드는 synchronized가 적용된 메소드끼리 일괄적으로 lock을 공유합니다. </b>


<h1> static synchronized method </h1>

- static이 붙은 synchronized method는 일반적으로 생각하는 static 성질을 가지므로 인스턴스가 아닌 <b> 클래스 단위 </b> 로 lock을 겁니다.

```
public class Main {

    public static void main(String[] args) throws InterruptedException {
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

    public static synchronized void run(String name) {
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
- 다른 인스턴스에 접근했지만 lock이 발생한 것을 확인할 수 있습니다.
- 즉, 다른 인스턴스라도 static 메소드에 synchronzied가 붙은 경우 lock을 공유하는 것을 확인할 수 있다.

<h1> 동기화 순서 </h1>

- synchronized를 통해 lock을 물고 있을 때 여러 개의 스레드가 접근 요청을 한다고 가정하자,
- 이후 lock이 풀리고 나면 과연 접근한 순서대로 접근하게 될까?

```
public class Main {

    public static void main(String[] args) throws InterruptedException {
        A a = new A();

        Thread[] threads = new Thread[5];

        for (int i = 0; i < threads.length; i++) {
            final int idx = i;
            threads[i] = new Thread(() -> {
                a.run("thread" + idx);
            });
        }

        for (Thread thread : threads) {
            thread.start();
            Thread.sleep(100);
        }
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
thread0 lock
thread0 unlock
thread4 lock
thread4 unlock
thread3 lock
thread3 unlock
thread2 lock
thread2 unlock
thread1 lock
thread1 unlock
```
첫 번째 0이 진입한 이후에는 동기화 순서가 보장되지 않는 것을 확인할 수 있다.
