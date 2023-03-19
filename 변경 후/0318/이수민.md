# System call과 Libary Call 
### 차이점
System Call은 커널에 대한 Resource Access 요청이다. </br>
Library Call은 프로그래밍 라이브러리에 정의 된 함수를 사용하라는 요청이다. </br>

- 운영체제 관련 용어
- 커널: System Call을 제공
- 라이브러리: Library Call 제공


# System Call
시스템에는 1.Kernel Mode 2. User Mode 두가지 모드가 있다. </br>

1. Kernel Mode에서 프로그램은 메모리 및 하드웨어 리소스에 직접 액세스 할 수 있다.
2. User Mode에서 프로그램은 메모리 및 하드웨어 리소스에 직접 액세스 할 수 없다.

</br>

대부분의 프로그램은 User Mode에서 실행된다. </br>
프로그램에 메모리나 하드웨어 리소스가 필요한 경우 System Call을 사용하여 커널에 요청을 보내고, 그런 다음 모드가 User Mode에서 Kernel Mode로 전환되고, </br>
작없이 끝나면 Kernel Mode에서 User Mode로 다시 바뀌게 된다. </br>

이러한 모드 전환을 Context Switching이라고 한다.


### Unix 환경에서 두가지 System Call 예 </br>
### fork()
- 기존 프로세스를 유지하면서 새 프로세스를 작성하는데 사용된다. 
- 특정 프로세스가 fork()를 호출하면 프로세스의 사본이 작성된다.
- 따라서 두 가지 프로세스가 있다. (Parent 프로세서, Child 프로세스: 작성된 새로운 프로세스)

### exec()
- 새 프로세스를 작성하고 종료 프로세스를 새 프로세스로 바꾼다.
- 따라서 exec()를 호출하면 새 프로세스만 존재한다.
- 즉, System Call을 수행한 프로세스가 파괴된다.

## System Call 종류
![image](https://user-images.githubusercontent.com/58407737/226169232-a754fd78-6f54-434a-8630-d0dc406c400a.png) 

</br>


# Library Call
- 프로그래밍 라이브러리에서 제공하는 기능을 사용하도록 요청한다.
- 프로그래머가 특정 Library Call을 사용하는 경우 먼저 관련 라이브러리를 가져와야한다.
- C 프로그래밍에서 프로그래머는 프로그램에 헤더 파일을 포함시켜 라이브러리 함수를 호출할 수 있고, 전처리기 기시문(#include)을 사용하여 헤더 파일을 포함시켜 사용할 수 있다. </br>


### 예시
- stdio.h 파일에는 입력 및 출력 조작을 수행하는 다양한 기능이 포함되어 있다.
- fopen()은 파일을 여는데 사용되고, fclose() 파일을 닫는데 사용된다. 
- math.h 헤더 파일에는 수학 연산을 수행하는 기능이 포함되어 있고,
- time.h 헤더 파일에는 시간 및 데이터 계산을 수행하는 기능이 있다.
- String.h 헤더 파일에는 문자열 조작을 수행하는 기능이 있다. 


## System Call과 Library Call 차이
- System Call은 자원에 Access하기 위해 커널 모드로 들어가기 위해 프로그램이 커널에 요청한 반면, Library Call은 프로그래밍 라이브러리에 정의 된 기능에 Access하기 위한 요청이다.

- UNIX / LINUX의 Manul은 명령어 man(manual)을 통해서 제공되고 있으며, manual의 영역에 따라 Section 번호를 제공한다.
- System Call은 Section 2번을 사용하고, Library Call은 Section 3번을 사용한다. 
