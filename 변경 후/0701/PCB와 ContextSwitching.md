<h3> Process Management </h3>

- cpu가 프로세스가 여러 개일 때, cpu 스케쥴링을 통해 관리하는 것을 말한다.
- 이 때, cpu는 각 프로세스들이 누군지 알아야 관리자 가능하다.
- 이러한 프로세스들의 특징을 갖고 있는 것이 바로 <b> Process Metadata </b> 이다.

Process Metadata에는 다음과 같은 정보들이 들어있다.
- Process ID : PID(Process Identification Number)라고도 한다.
    - 프로세스 고유 식별 번호
- Process State ( 프로세스 상태 )
    - 프로세스의 현재 상태(준비, 실행, 대기상태)를 기억시킨다.
- Process Priority(스케쥴링 정보)
    - 프로세스 우선순위와 같은 스케쥴링 관련 정보를 기억한다.
- CPU Registers
    - 프로세스의 레지스터 상태를 저장하는 공간
    - cpu 내 범용 레지스터(AX, BX, CX, DX), 데이터 레지스터(SP, BP, SI, DI), 세그먼트 레지스터(CS, DS, ES, SS) 등이 갖고 있는 값을 기억시킨다.
- Owner(계정 정보)
    - cpu 사용 시간의 정보(Quantum), 각종 스케쥴러에 필요한 정보를 기억시킨다.
- 기억장치 관리 정보
    - 프로그램이 적재될 기억 장치의 상한치, 하한치, 페이지 테이블 등의 정보를 기억시킨다.
- 입출력 정보
    - 프로그램 수행 시 필요한 주변 장치, 파일들의 정보를 기억시킨다.
- 프로그램 카운터(계수기)
    - 다음에 실행되는 명령어의 주소를 기억시킨다.


<h2> PCB (Process Controll Block) </h2>

- 프로세스 메타데이터들을 저장해 놓는 곳
- 하나의 PCB 안에는 하나의 프로세스 정보가 담겨있다.

![image](https://github.com/youbeen2798/CS-study_for_interview/assets/62228401/a028dab3-df6a-482d-98e9-58838ed9dfe0)

- 프로그램 실행 -> 프로그램 생성 -> 프로세스 주소 공간에 (코드, 데이터, 스택)생성 -> 이 프로세스의 메타데이터들이 PCB에 저장

<h2> PCB(Process Control Block) 상세 구조 </h2>

![image](https://github.com/youbeen2798/CS-study_for_interview/assets/62228401/a02d955a-e01c-4593-bb0f-ef1173f4c4b4)

- Process State : 프로세스 상태 (Create, Ready, Running, Block, Terminated)
- Process Counter : 다음 실행할 명령어의 주소값
- CPU Registers : accumulater, index register, stack pointers, general purpose registers.

<h2> PCB가 필요한 이유? </h2>

- CPU에서는 프로세스의 상태에 따라 교체 작업이 이루어진다.
- 인터럽트가 발생해서 할당받은 프로세스가 block 상태가 되고 다른 프로세스를 running으로 바꿀 때
