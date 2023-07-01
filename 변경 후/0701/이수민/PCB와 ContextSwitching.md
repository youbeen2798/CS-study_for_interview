## ContextSwitching (문맥 교환)
- 멀티프로세스 환경에서 CPU가 하나의 프로세스를 실행하고 있는 상태에서 인터럽트 요청에 의해 다음 우선 순위의 프로세스가 실행되어야 할 때 현재 진행하고 있는 Task(Process, Thread)의 상태를 저장하고 다음 진행할 Task의 상태값을 읽어 적용하는 과정을 말한다.
- System Call이나 인터럽트가 발생한다고 반드시 context switcing이 일어나는 것은 아니다.
</br>

## Why use?
- Task를 동시에 사용하는 것처럼 보이기 위해 CPU가 Task를 바꿔 가며 Context Switching을 한다.

</br>

### 문맥 교환 흐름
![image](https://github.com/leesuuuuumm/CS-study_for_interview/assets/58407737/8f7b08f4-6ae5-4ab4-a208-1f63feaaa648)

- Task의 대부분의 정보는 Register에 저장되고 PCB로 관리되고 있다.
- CPU가 현재 실행(연산)하면 상태 변화가 생기는데 상태(Task의 PCB정보)를 저장하게 된다. -> Process Stack, Ready Queue
- 다음 실행할 Task의 PCB를 읽어 Register에 적재하고 CPU가 이전에 진행했던 과정을 연속적으로 수행할 수 있다.

</br>

## PCB 구조
![image](https://github.com/leesuuuuumm/CS-study_for_interview/assets/58407737/3f00f880-97a8-4f53-8424-269f3e960ae6)
- process state: 프로세스 상태 (create, ready, running, waiting, terminated)
- process counter: 다음 실행할 명령어의 주소값
- registers:누산기, 스택, 색인 레지스터
- process number

</br>

### Context Switcing이 일어날때 해당 CPU는 아무런 일을 못하기 때문에 Context Switcing이 잦아지면 오히려 오버헤드가 발생해 효율이 떨어진다. 

</br>

인터럽트는 cpu가 프로그램을 실행하고 있을 때 실행중인 프로그램 밖에서 예외 상황이 발생하여 처리가 필요한 경우 CPU에게 알려 예외 상황을 처리할 수 있도록 말해주는 것이다.
</br>

1. I/O Request (입출력 요청할 때)
2. time slice expired (Cpu 사용시간이 만료 되었을 때)
3. fork a child (자식 프로세스를 만들 때)
4. wait for an interrupt (인터럽트 처리를 기다릴 때)


</br>

## Context Switching Cost
- Cache 초기화
- Memory Mapping 초기화

### Thread는 Stack 영역을 제외한 모든 메모리를 공유하기 때문에 Context Switching 발생 시 stack 영역만 변경을 진행하면 되기 때문에 Process 보다 비용이 적다.
(캐시가 쌓아놓은 데이터들이 무너지고, 새로운 캐시 정보를 불러 와야 하기 때문에 시스템에 부하도 간다.)
