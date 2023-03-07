<h1> DMA(Direct Memory Access) </h1>

- DMA는 CPU를 대신하여 I/O장치와 Memory 사이의 데이터 전송을 담당하는 장치이다.
- DMA에 의한 입출력 방식은 CPU의 개입없이 직접 주기억 장치와 DMA 사이에서 일련의 입출력 동작이 이루어지는 방식이다.

<h3> DMA 특징 </h3>

- CPU를 경우하지 않고, 직접 기억 장치와 입출력 장치 사이에서 전송이 이루어진다.
- 하나의 입출력 명령어에 의해 하나의 블록 전체가 전송된다.
- 사이클 스틸에 의해 전송이 이루어진다.
- 전송이 끝나면 인터럽트를 발생시켜 CPU에게 알린다.
- 데이터 전송 절차 : 버스 사용 요구 -> 버스 사용 허가 -> 데이터 전송 -> 인터럽트

<h3> DMA 필요성 </h3>

- 고속의 I/O 장치의 경우 CPU의 실제 프로세스 작업 시간 감소
- 디스크와 같은 많은 데이터를 입/출력 하는 장치를 위해 CPU가 매번 전송을 제어하는 방법의 비효율성
- 인터럽트 방식이 프로그램에 의한 입출력 방식보다 효율적이지만 입출력을 위한 상태, 제어 정보, 데이터 전송을 위해서 능동적인 CPU 개입이 필요 -> 오버헤드 발생

<h3> DAM I/O와 Direct I/O 환경 비교 </h3>

![image](https://user-images.githubusercontent.com/62228401/223290719-ba51d713-28e2-4ef6-8309-d235266bedc2.png)

- DAM I/O -> DMA 기반 Data 처리 중 CPU는 다른 프로세스를 처리한다.

![image](https://user-images.githubusercontent.com/62228401/223290800-26b82eac-7f5a-4881-a84f-459316bcfced.png)

- Direct I/O(DMA 미사용) - Data I/O 처리 시 완료까지 작업 중지, CPU 대기 필요
