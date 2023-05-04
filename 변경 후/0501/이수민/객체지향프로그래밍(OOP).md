# 객체지향프로그래밍 (Object Oriented Programming)
- 실제세계를 객체라는 단위로 나누고 객체들간의 상호작용을 의미한다.
- 즉, 프로그램을 여러개의 독립된 단위인 객체들의 모임으로 파악하고자 하는 것이다.


## 객체 (Object)
우리 일상생활에서 인식할 수 있는 모든 사물
- 속성: Field (변수)
- 행위: Method (메서드)

</br>

위 객체를 만드는 설계도 or 틀을 클래스(Class)라 한다. 

```
public class People{
  int name;
  int age;
  int sex;
}

```
- People이라는 class를 만든다.
 
```
public static void main(String[] args){
    People p1; // 객체
    p1 = new People(); // 인스턴스화
}
  
```

- p1은 People 클래스의 인스턴스 (객체를 메모리에 할당함)


</br>

### 클래스(class) VS 객체(Object)
- class: 설계도 
- Object: 설계도를 구현한 모든 대상

</br>

### 객체(Object) VS 인스턴스(Instance)
- 클래스의 타입으로 선언되었을 때 객체라 부르고, 그 객체가 메모리에 할당되어 실제 사용될 때 인스턴스라 한다.
- 객체는 현실 세계에 가깝고, 인스턴스는 소프트웨어 세계에 가깝다.
- 객체는 실체, 인스턴스는 관계에 초점을 맞춘다.
- 객체를 클래스의 인스턴스라고 한다.
</br>

- 객체와 인스턴스를 나누는 것은 모호하다고도 한다.

</br>

## 절차지향 vs 객체지향
![image](https://user-images.githubusercontent.com/58407737/236145349-910f064b-cb8c-4733-8118-fce331a1fff3.png)

</br>

### 객체지향 장점
1. 코드 재사용 용이 
- 상속을 통해 코드의 재사용을 높일 수 있다.
 
2. 유지보수의 우수성
- 캡슐화를 통해 유지보수가 쉽다.

3. 대형 프로젝트에 적합
- 클래스 단위로 모듈화 개발로 업무 분담

### 객체지향 단점
1. 실행 속도가 느리다.
- 객체지향 언어가 대체적으로 실행속도 느림

2. 코딩 난이도 상승
- 다중 상속같은 이유로 복잡도 상승한
 
</br>

## OOP 4가지 특징
### 1. 캡슐화
- 데이터와 코드의 형태를 외부로부터 알 수 없게 하고, 데이터의 구조와 역할, 기능을 하나의 캡슐 형태로 만드는 방법 (정보은닉)

<br>

#### 캡슐화 방법 
= 접근 제어자 private를 붙인다. (자기 클래스 외의 클래스는 접근 불가능 하다.)
- 맴버 변수에 값을 넣고 꺼내 올 수 있는 메서드를 만든다. (set/get을 사용해 메서드를 만든다.)

*접근 제어자* </br>
![image](https://user-images.githubusercontent.com/58407737/236147246-4f852b6a-0c82-45bd-8296-ff9c15c54c3c.png)

</br>

(예시)
![image](https://user-images.githubusercontent.com/58407737/236147426-8fa2ff64-289f-4e1f-ae47-33ce84a10ae5.png) </br>
![image](https://user-images.githubusercontent.com/58407737/236147524-9e3da308-6efb-4a81-bd13-a22e528ff690.png)

</br>

### 2. 추상화
- 클래스들의 공통적인 특성(변수, 메소드)들을 묶어 표현하는 것

![image](https://user-images.githubusercontent.com/58407737/236155186-6a181b84-7d68-48aa-a7cd-5a6c93b4a5a5.png)


</br>

### 3. 상속
- 부모 클래스에 정의된 변수 및 메서드를 자식 클래스에서 상속받아 사용하는 것

</br>

### 4. 다형성
- 하나의 객체가 메소드가 여러가지 다른 형태를 가질 수 있는 것을 말한다.

</br>

1. 오버라이딩
- 부모클래스의 상속 받은 생성자나 매개변수, 메서드 등을 자식 클래스에서 재정의 하는 것을 의미한다. 


2. 오버로딩
- 하나의 클래스 안에서 같은 이름의 메서드를 여러 개 정의하는 것을 말한다.
- 매개변수 타입이 다르거나, 매개변수 개수가 다른 경우

</br>

## OOP의 5가지 원칙 (SOILD)
### 1. 단일 책임 원칙 (Single Responsibility Principle)
![image](https://user-images.githubusercontent.com/58407737/236155302-79b28f00-3ce7-4f92-a45f-d40c64cd59e2.png)

- 한 클래스는 하나의 책임만 가져야한다. 

</br>

### 2. 개방 폐쇄 원칙 (Open/Closed Principle)
![image](https://user-images.githubusercontent.com/58407737/236155361-21ebe586-51a6-4273-9269-1cafb5f575be.png)

- 확장에는 열려(Open)있지만, 변경에는 닫혀(Close)있어야 한다.

</br>

### 3. 리스코프 치환 원칙 (Liskov’s Substitution Principle)
![image](https://user-images.githubusercontent.com/58407737/236155409-106eb97f-5113-4ef7-87ea-9984cfad012d.png)

- 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야한다.

</br>

### 4. 인터페이스 분리 원칙 (Interface Segregation Principle)
![image](https://user-images.githubusercontent.com/58407737/236155450-4d417b66-321e-4cf6-a447-db65ee3f8b0c.png)

- 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.

</br>

### 5. 의존관계 역전 원칙 (Dependency Inversion Principle)
![image](https://user-images.githubusercontent.com/58407737/236155501-6f0e3e93-23fd-491d-8567-7b04be62f0e0.png)
![image](https://user-images.githubusercontent.com/58407737/236150871-f002e9e8-ac99-4bef-84a7-3790441058ce.png)

- 추상화에 의존하고, 구체화에 의존하면 안된다.

-> 고수준 모듈은 저수준 모듈의 구현에 의존해서는 안된다. 
-> 대신 저수준 모듈이 고수준 모듈에서 정의한 추상 타입에 의존해야한다.

- 고수준 모듈: interface, 추상 클래스
- 저수준 모듈: 메인클래스, 객체
- 코드의 확장성 및 재사용성을 추구하기 위한 원칙이다. 
- 다른 법칙보다 중요도가 떨어지는데 타 원칙의 호위호환이기 때문이다. 

