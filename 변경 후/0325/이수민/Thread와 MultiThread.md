# Thread 란?
- 하나의 프로세스 내부에서 독립적으로 실행되는 하나의 작업 단위를 말하며, 세부적으로 운영체제에 의해 관리되는 하나의 작업을 의미한다. </br>

</br>

1. JVM에 의해 하나의 프로세스가 발생하고 main() 안의 실행문들이 하나의 스레드이다.
2. main() 이외의 또 다른 스레드를 만들려면 Thread 클래스를 상속하거나 Runnable 인터페이스를 구현한다.
3. 다중 스레드 작업 시에는 각 스레드끼리 정보를 주고받을 수 있어 처리 과정의 오류를 줄일 수 있다.
4. 프로세스끼리는 정보를 주고 받을 수 없다.

</br>

## Thread 사용이유
### 1. 메모리 절약
-> OS마다 다르지미ㅏㄴ, 무슨 작업을 수행하려고 할 때 JVM은 적어도 32 ~ 64MB 물리 메모리 점유한다. </br>
하지만 스레드는 1MB 이내의 메모리만 점유한다. </br>
### 그래서 스레드를 경량 프로세스라고 부른다.

### 2. 프로세스 컨텍스트 스위칭에 비해 오버해드 절감
-> 멀티 프로세스로 실행되는 작업을 멀티 스레드로 실행하게 되면 프로세스를 생성하여 자원을 할당하는 과정도 줄어들 뿐더러 프로세스를 콘텍스트 스위칭 하는 것보다 오버헤드를 더 줄일 수 있게 된다. </br>

### 3. 작업들 간 통신 비용 절감

</br>

## 특징 
- 프로세스 내에서 stack만 따로 할당받고, code, data, heap 영역은 공유한다. (스택만 공유 x)
- 한 스레드가 프로세스 자원을 변경하면, 이웃 스레드도 그 변경결과를 즉시 볼 수 있다.
- 프로세스 내에서 스레드 간 자원을 공유하거나 하지 않는 경우 둘 다 있다.

</br>
</br>

# Multi Thread
- 여러 스레드를 동시에 실행시키는 응용 프로그램을 작성하는 기법을 말한다. (주어진 자원을 극한으로 사용하기 위한 모델)
-> 유튜브로 노래 들으면서 워드 작성을 할 수 있게 해준다.

</br>

## 장점 
1. 메모리 공유로 잉한 시스템 자원 소모가 줄어든다.
2. 동시에 두가지 이상의 활동 하는 것이 가능해진다.

</br>

## 단점
1. 서로 자원을 소모하다가 충돌이 일어날 가능성이 존재한다.
2. 코딩이 난해해져 버그생성확률이 높아진다.

</br>

## Thread의 생명주기
![image](https://user-images.githubusercontent.com/58407737/227584973-39109117-2290-4901-86c0-0f162e6e3c46.png)

</br>

### 1. Runnable (준비 상태): 쓰레드가 실행되기 위한 준비 단계
- cpu를 점유하고 있지 않으며 실행(Running 상태)을 하기 위해 대기하고 있는 상태이다. 
- 코딩 상에서 start() 메소드를 호출하면 run() 메소드에 설정된 스레드가 Runnable 상태로 진입한다. 
- "Ready" 상태라고도 한다.

### 2. Running (실행 상태): 스케줄러에 의해 선택된 쓰레드가 실행되는 단계
- cpu를 점유하여 실행하고 있는 상태며 run() 메서드는 JVM만이 호출 가능하다.
- Runnable(준비상태)에 있는 여러 쓰레드 중 우선 순위를 가진 스레드가 결정되면 JVM이 자동으로 run() 메소드를 호출하여 스레드가 Running 상태로 진입한다. 

### 3. 종료 상태
- Running 상태에서 스레드가 모두 실행되고 난 후 완료 상태이다.
- "Done" 상태라고도 한다.

### 4. Blocked (지연 상태): 쓰레드가 작업을 완수하지 못하고 잠시 작업을 멈추는 단계
- cpu 점유권을 상실한 상태이다. 후에 특정 메서드를 실행시켜 Runnable(준비상태)로 전환한다.
- wait() 메소드에 의해 Blocked 상태가 된 스레드는 notify() 메소드가 호출되면 Runnable 상태로 간다. 
- sleep(시간) 메소드에 의해 Blocked 상태가 된 스레드는 지정된 시간이 지나면 Runnable 상태로 간다.

</br>

# Thread 예제
## 1. Single Tread (Thread 클래스 상속)

```
public class SingleThreadEx extends Thread{
    private int[] temp;
    public SingleThreadEx(String threadname){
	super(threadname);
	temp = new int[10];
		
	for(int start=0;start<temp.length;start++){
		temp[start]=start;
	}
    }
	
    public void run(){
	    for(int start:temp){
		try {
			Thread.sleep(1000);
				
		} catch (InterruptedException ie) {
			ie.printStackTrace();
			// TODO: handle exception
		}
		System.out.println("스레드이름:"+currentThread().getName());
		System.out.println("temp value :"+start);
	}
    }
	
    public static void main(String[] args) {
	SingleThreadEx st = new SingleThreadEx("첫번째");
	st.start();
    }
}
```
## 2. Sing Thread (Runnable 인터페이스 상속) 
-> 1번 방법보다 많이 쓰인다. 
```
public class SingleThreadEx2 implements Runnable{

    private int[] temp;
	
    public SingleThreadEx2(){
	temp = new int[10];
		
	for(int start=0;start<temp.length;start++){
		temp[start]=start;
	}
    }
	
    @Override
    public void run() {
	// TODO Auto-generated method stub
	for(int start:temp){
		try {
			Thread.sleep(1000);
				
		} catch (InterruptedException ie) {
			ie.printStackTrace();
			// TODO: handle exception
		}
			
		System.out.println("스레드이름:"+Thread.currentThread().getName());
		System.out.println("temp value :"+start);
	}
    }
	
    public static void main(String[] args) {

	SingleThreadEx2 ct = new SingleThreadEx2();
	Thread t = new Thread(ct,"첫번째");

	t.start();
    }
}
```
</br>
결과: </br>

![image](https://user-images.githubusercontent.com/58407737/227587240-9b14553f-533f-4104-be67-f4f2aeb71928.png)

</br>

## 3. Multi Thread (1)
```
public class Main {
    public static void main(String[] args) {
	ThreadEX threadex = new ThreadEX();
	ThreadEX threadex2 = new ThreadEX();
	Thread thread1 = new Thread(threadex,"A");
	Thread thread2 = new Thread(threadex2,"B");
		
	thread1.start();
	thread2.start();
		
	Thread.currentThread().getName();
    }
}

public class ThreadEX implements Runnable{

    int TestNum=0;
    @Override
    public /*synchronized 하나가 끝나야 실행됨*/ void run() {
	// TODO Auto-generated method stub
	for(int i=0;i<10;i++){
		if(Thread.currentThread().getName().equals("A")){
			System.out.println("=======================");
			TestNum++;
		}
		System.out.println("ThreadName ="+Thread.currentThread().getName()+"TestNum ="+TestNum);
			
		try {
			Thread.sleep(500);
		} catch (InterruptedException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	 }
      }
}
```
</br>
결과: </br>

![image](https://user-images.githubusercontent.com/58407737/227587780-23d3cceb-b086-498c-898b-e1aeb4b607f3.png)

</br>

## 4. Mult Thread (2)
```
class ATM implements Runnable {
    private long depositeMoney = 10000;

    public void run() {
	synchronized (this) {
			
	    for (int i = 0; i < 10; i++) {
	           notify();
		try {
			wait();
			Thread.sleep(1000);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		if (getDepositeMoney() <= 0)
			break;
		withDraw(1000);
	    }
	}
}

public void withDraw(long howMuch) {
	if (getDepositeMoney() > 0) {
		depositeMoney -= howMuch;
		System.out.print(Thread.currentThread().getName() + " , ");
		System.out.printf("잔액 : %,d 원 %n", getDepositeMoney());
	} else {
		System.out.print(Thread.currentThread().getName() + " , ");
		System.out.println("잔액이 부족합니다.");
	}
}

public long getDepositeMoney() {
	return depositeMoney;
    }
}

public class SynchronizedEx {
    public static void main(String[] args) {
	ATM atm = new ATM();
	Thread mother = new Thread(atm, "mother");
	Thread son = new Thread(atm, "son");
	mother.start();
	son.start();
    }
}
```

</br>
결과: </br>

![image](https://user-images.githubusercontent.com/58407737/227587537-eba8c5c1-854a-4538-97c1-0348ff2da7af.png)

</br>


# Runnable과 Thread 차이
## 1. Runnable
- Implements Runnable을 통해 Runnable 인터페이스를 구현할 수 있다.
- 재사용성이 높고, 코드의 일관성을 유지할 수 있어서 Thread보다 효율적인 방법이다.
- 추상 메서드 run을 구현해야한다.

-> 인터페이스를 사용함으로써 객체를 만들 때 재사용할 수 있기 때문에 효율적이다. 
</br>


## 2. Thread 
- 상속을 받아 사용하기 때문에 다른 클래스를 상속받아 사용할 수 없다는 단점이 있음


### 추상 메서드로 run() 밖에 존재하지 않은 Runnable을 사용하는 이유?
- Thread를 바로 사용하려면 상속을 받아야하는데, 자바는 다중상속을 허용하지 않기 때문에 Thread 클래스를 바로 상속받는 경우 다른 클래스를 상속 받지 못한다.
- 반면에 Runnable 인터페이스를 구현한 경우에는 다른 인터페이스를 추가로 구현할 수 있을 뿐만 아니라, 다른 클래스도 상속 받을 수 있다.
- 따라서 클래스의 확장성이 중요하다면 Runnable 인터페이스를 구현해 Thread에 주입 해준다. 


