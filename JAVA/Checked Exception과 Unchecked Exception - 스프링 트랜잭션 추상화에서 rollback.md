(1) Throwable<br/>
(1-1) Error (1-2)Exception <br/>
(1-2-1) IOException  (1-2-2) RuntimeException<br/>
 (1-2-2-1)ArithmeticException
 
 **Unchecked Exception**

- **RuntimeException**을 **상위 클래스**로 가지고 있는 클래스
- NullPointException, IllegalArgumentExcetpion, ArithmeticException 등
<br/>

****Checked Exception****

- **RuntimeException을 부모로 가지는 클래스 제외**한 Exception의 하위 클래스
- **IOException, SQLException,** **Error**
<br/>

- Error가 발생할 때에는?
    - 비정상적인 상황(OutofMemoryError, StackOverflowerError 등) 발생했을 경우
    - JVM 에 문제, 우리가 처리 할 수 없을 때, JVM이 운영할 수 없을 때, 하드웨어 문제생길시
    - 즉 개발자가 해결할 수 없고, 예측할 수도 없을 때
    
    ⇒ 개발자가 사용하는 기반 시스템에 문제가 생길 경우
    
- error 처리 할 필요 없음
<br/>

****Checked Exception****

1. 반드시 예외처리해야한다.
2. 컴파일 단계에서 발생

위와 같은 속성에 따라 `Checked Exception`은 IDE에서 예외처리 강요

→ 컴파일 단계에서 발생. 따라서 Checked Exception 은 반드시 `try ~ catch`문이나 `throws`로 `Exception` 처리해줘야함
<br/>
<br/>

**Unchecked Exception** 

1. 명시적인 처리를 강제하지 않는다.
2. 실행(Runtime) 단계에서 발생한다.

→ IllegalArgumentException를 발생시킬 때  `try ~ catch`문이나 `throws`로 `Exception` 처리 안해줘도 IDE에서 컴파일에러가 나지 않음, 이는 실행(Runtime)에서 Exception이 발생할 것임을 유추

하지만 이것이 Exception 처리를 하지 않는다는 뜻이 아님 

→ “명시적인 처리를 강제하지 않음”

→ ExceptionHandler 등을 통하여 유저 메시지를 출력하던, 로그를 쌓던, 알림을 보내던 **Excetpion 상황에 대처하기 위해 필요한 후 처리 반드시 필요!!** 

클린코드에선 Unchecked Exception 사용 권장 (이유: checked Exception은 OCP 위배)

<br/>
또한, Java Exception 종류와 DB 트랜잭션 Rollback은 아무 상관이 없음

***java Exception의 종류와 DB 트랜잭션 Rooback은 아무 상관이 없다.***

Spring의 Exception 발생 시 트랜잭션 기본 동작은

`RuntimeException`  **Rollback 처리** `Checked Exception` **Rollback**을 하지 않음

→ [16. Transaction Management](https://docs.spring.io/spring-framework/docs/4.2.x/spring-framework-reference/html/transaction.html)

또한, Spring은 다양한 옵션을 통해 Rollback에 대한 처리를 개발자가 Optional하게 처리

`@Transactional`어노테이션에서 rollback 관련 지정할 수 있는 옵션 제공

즉, Spring의 Exception 발생에 대한 동작 옵션들을 지원하기 때문에 개발자가 지정할 수 있음
 
                         
                         
