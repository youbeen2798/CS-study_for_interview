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

- 프로세스는 수행할 차례가 되면 cpu를 할당받아 작업을 처리한다.
- 작업을 처리하던 도중 프로세스의 시간이 모두 경과되거나 인터럽트가 발생하는 등 프로세스 전환이 발생하면, 진행하던 작업을 저장하고 cpu를 반환한다.
- 이 때 수행하던 프로세스 관련 데이터를 pcb에 저장한다.
- 그리고 다시 프로세스의 수행 차례과 와서 cpu를 할당받게 되면, pcb에 저장되어있던 내용을 불러와 이전에 종료되었떤 시점부터 다시 작업을 수행한다.
- 이렇게 <b> 사용하던 프로세스 데이터를 pcb에 저장하고, 실행할 프로세스의 데이터를 pcb에서 불러오는 과정을 Context Switching </b> 이라고 한다.

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

- 프로세스는 수행할 차례가 되면 cpu를 할당받아 작업을 처리한다.
- 작업을 처리하던 도중 프로세스의 시간이 모두 경과되거나 인터럽트가 발생하는 등 프로세스 전환이 발생하면, 진행하던 작업을 저장하고 cpu를 반환한다.
- 이 때 수행하던 프로세스 관련 데이터를 pcb에 저장한다.
- 그리고 다시 프로세스의 수행 차례과 와서 cpu를 할당받게 되면, pcb에 저장되어있던 내용을 불러와 이전에 종료되었떤 시점부터 다시 작업을 수행한다.
- 이렇게 <b> 사용하던 프로세스 데이터를 pcb에 저장하고, 실행할 프로세스의 데이터를 pcb에서 불러오는 과정을 Context Switching </b> 이라고 한다.

<h2> 캐시 메모리? </h2>

- 문맥 교환시 Cache memory flush가 이루어지는데 cpu와 메인 메모리 사이에 존재하는 작은 메모리 공간으로 프로세스가 바뀔 때 cache memory를 밀어버리게 된다.
- 이 작업의 오버헤드가 크다.
- 캐시를 밀어버림으로써 hit가 줄어들게 되고 초반 프로세스의 작업속도가 느릴 수 있다.

<h2> PCB가 필요한 이유? </h2>

- CPU에서는 프로세스의 상태에 따라 교체 작업이 이루어진다.
- 인터럽트가 발생해서 할당받은 프로세스가 block 상태가 되고 다른 프로세스를 running으로 바꿀 때
- <b> 이 때, 앞으로 다시 수행할 Block 상태의 프로세스 상태 값을 PCB에 저장해 두는 것 </b> 이다.

<h2> PCB의 관리 방식 </h2>

- Linked List 방식으로 관리가 된다.
- PCB List Head에 PCB들이 생성될 때마다 붙게 된다.
- 주소값으로 연결이 이루어져 있는 연결 리스트 형태로, <b> 삽입, 삭제가 용이 </b> 하다.
- <b> 즉, 프로세스가 생성되면 해당 PCB가 생성되고 프로세스 완료 시 제거된다. </b>
- 이렇게 수행 중인 프로세스를 변경할 때, <b> CPU의 레지스터 정보가 변경되는 것을 Context Switching </b> 이라고 한다.

<h2> Context Switching이 필요한 이유 </h2>

- 만약 컴퓨터가 매번 하나의 Task만 처리할 수 있다면?
- 다음 Task를 처리하기 위해 현재 Task가 끝날 때까지 기다려야 한다.
- 반응 속도가 매우 느리고 사용하기 불편하다.

  <b> 다양한 사람들이 동시에 사용하는 것 처럼 하기 위해 Context Switcing이 필요하게 되었다. </b>
  - 컴퓨터 멀티 태스킹을 통해 빠른 반응 속도로 응답이 가능하다.
  - 빠르게 Task를 바꿔가면서 실행하기에 사람은 실시간 처리가 되는 것처럼 보인다.
  - CPU가 Task를 바꿔가며 실행하기 위해 Context Switching이 필요하게 되었다.

 <h2> Context Switching의 뜻 </h2>

- cpu가 현재 실행하고 있는 Task(Process, Thread)의 상태를 저장하고, 다음 진행할 Task의 상태 및 Register에 대한 정보(Context)를 읽어 새로운 Task의 Context 정보로 교체하는 과정을 말한다.
- 다르게 말하면, <b> CPU가 이전의 프로세스 상태를 PCB에 보관하고, 또 다른 프로세스의 정보를 PCB에 읽어서 레지스터에 적재하는 과정 </b> 을 말한다.
- 또 다르게 말하면, <b> 다중 프로그래밍 시스템에서 CPU가 할당되는 프로세스를 변경하기 위해 현재 CPU를 사용하여 실행되고 있는 프로세서의 상태 정보를 저장하고 제어권을 인터럽트 서비스 루틴(ISR)에게 넘기는 작업 </b>을 말한다.
-  여기서 Context란 CPU가 다루는 Task(Process, Thread)에 대한 정보를 말하고, 대부분의 정보는 Register에 저장되고 PCB로 관리된다.
-  인터럽트가 발생하거나, 실행중인 CPU 사용 허가 시간을 모두 소모하거나, 입출력을 위해 대기해야 하는 경우 Context Switching이 발생한다.
-  즉, Context Switcinh은 프로세스가 Ready -> Running, Running -> Ready, Running -> Block 처럼 상태 번경 시에 발생한다.

<h2> Context Switching의 수행 과정 </h2>

1. Task의 대부분 정보는 Register에 저장되고 PCB(Process Control Block)에 관리가 되고 있다.
2. 현재 실행되고 있는 Task의 PCB 정보를 저장하게 된다.(Process Stack, Ready Queue)
3. 다음 실행할 Task의 PCB 정보를 읽어 Register에 적재하고 CPU가 이전에 진행했던 괒어을 연속적으로 수행할 수 있게 된다.

<h2> Context Switcing Cost </h2>

- Context Switcing이 발생하면 다음과 같은 Cost가 소요된다.
  1. Cache 초기화
  2. Memory Mapping 초기화
  3. 메모리 접근을 위해서 Kernel은 항상 실행되야 한다.

- 따라서 잦은 Context Switcing은 성능 저하를 가져온다.

<h2> Context Switcing과 Interrupt </h2>

- CPU는 하나의 프로세스 정보만을 기억한다.
- 여러 개의 프로세스가 실행되는 다중 프로그래밍 환경에서 CPU는 각각의 프로세스 정보를 저장했다 복귀하고 다시 저장했다 복귀하는 일을 반복한다.
- 프로세스의 저장과 복귀는 프로세스의 중단과 실행을 의미한다.
- 프로세스의 중단과 실행 시 인터럽트가 발생하므로, 문맥 교환이 많이 일어난다는 것은 인터럽트가 많이 발생한다는 것을 의미한다.

<h2> Context Switcing과 시간 할당량 </h2>

- 프로세스의 시간 할당량은 시스템 성능의 중요한 역할을 한다.
- 시간 할당량이 적을수록 사용자 입장에서는 여러 개의 프로세스가 거의 동시에 수행되는 느낌을 갖지만, 인터럽트의 수와 문맥 교환의 수가 늘어난다.
- 프로세스 실행을 위한 부가적인 활동을 오버헤드(간점 부담 비용)이라고 하는데, 이 또한 문맥 교환 수와 같이 늘어난다.

- 시간 할당량이 적어지면 : 문맥 교환 수, 인터럽트 횟수, 오버헤드가 증가하지만 여러 개의 프로세스가 동시에 수행되는 느낌을 갖는다.
- 시간 할댱량이 커지면 : 문맥 교환 수, 인터럽트 횟수, 오버헤드가 감소하지만 여러 개의 프로세스가 동시에 수행되는 느낌을 갖지 못한다.

<b> 프로세스를 수행하다가 I/O event가 발생하여 BLOCK 상태로 전환시켰을 때, CPU가 그냥 놀게 놔두는 것보다 다른 프로세스를 수행시키는 것이 효율적 </b> 이므로, CPU에 계속 프로세스를 수행시키도록 하기 위해서 다른 프로세스를 실행시키고 Context Switcing을 할 때, Overhed가 발생한다.

- CPU가 놀지 않도록 만들면서, 사용자에게 빠르게 일처리를 제공해주기 위함이다.

<h2> Process vs Thread </h2>

- Context Switching 비용은 Process가 Thread보다 많이 든다.
- 그 이유는 Thread는 Stack 영역을 제외한 모든 메모리를 공유하기에 Context Switcing 발생시 Stack 영역만 변경하면 된다.

<h1> PCB vs TCB </h1>

- PCB는 OS의 스케쥴러에 의해 Context Switching 되는 프로세스의 정보 단위를 의미하고
- TCB는 스레드 라이브러리에 의해 Context Switching되는 스레드의 정보 단위를 의미한다.

- 
