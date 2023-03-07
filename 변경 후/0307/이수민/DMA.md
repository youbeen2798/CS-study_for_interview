# 입출력 제어 방식
### 1. 프로그램에 의한 I/O (CPU 개입 O)
### 2. 인터럽트에 의한 I/O (CPU 개입 O)
### 3. DMA에 의한 I/O (CPU 개입 X)
### 4. 채널에 의한 I/O (CPU 개입 X)

</br>
</br>

### 메모리에 접근할 수 있는 장치는 CPU 밖에 없다. 

</br>

# DMA(Direct Memory Access): 직접 메모리 접근
### 주변 장치(하드 디스크, 그래픽 카드 등)들이 메모리에 직접 접근하여 읽거나 쓸 수 있도록 하는 기능이다. 
### CPU 없이 I/O 장치와 기억장치 사이에 데이터를 전송하는 접근 방식이다.

중요한 것은 CPU가 해야할 주변장치와의 데이터 전송을 DMA장치가 해주는 것이다. 그래서 그만큼 CPU 효율을 늘릴 수 있다. 

PIO(Programmed Input/Output)은 CPU가 주변장치와 데이터를 주고받는 방식으로 효율이 떨어진다. 이를 극복하기 위해 DMA가 개발되었다. </br>

![image](https://user-images.githubusercontent.com/58407737/223424561-86d5fadb-0ab6-4257-a8e7-c7c1c92d9e31.png)

하드디스크에서 데이터를 꺼낸 후, 시스템 버스를 통해 CPU를 레지스터에 옮겨 다시 시스템 버스를 통해 CPU 레지스터에서 메모리로 이동한다. </br> 
CPU를 1곳 거쳐가는 데 지연 시간이 걸리겠지만, 입출력 시간동안 CPU가 idle 상태로 대기한다. </br>
I/O 디바이스에 비해 CPU는 비교할 수 없을 정도로 고속이기 깨문에 그 시간을 낭비한다는 것은 비효율적이다. </br>

</br>
</br>


![image](https://user-images.githubusercontent.com/58407737/223425116-74652fa1-6506-4f3d-9515-91f2215cf196.png)

PIO 방식의 단점을 제거한것이 DMA 방식이다. </br>
DMA Controller를 이용하면 하드디스크와 메모리를 직접 연결하여 CPU는 제어 신호만 주고받을 뿐 데이터 전송에서 제외시킬 수 있다.</br>
따라서 입출력 시 CPU는 제어를 위해 전송 시작과 완료에만 할당되어 CPU 낭비가 제거된다. </br>

또한, 고속의 I/O 장치의 경우 빈번하게 인터럽트가 발생하는데, DMA를 사용함으로써 프로그램 수행 중 인터럽트의 횟수를 최소화한다. </br>
DMA가 없다면 Data I/O 처리가 끝날 때까지 CPU는 대기해야한다. </br>


## 동작 절차
### CPU 명령 
### 버스 사용 요구 (Bus Request)
### 버스 사용 허가 (Bus Grant)
### 데이터 전송
### 인터럽트

1. I/O가 CPU에게 입출력 요청
2. CPU가 DMA 컨트롤러에 명령 송신
3. DMA가 CPU에게 시스템 버스 사용 요청
4. CPU가 버스 사용 허가(CPU가 버스 사용 포기)
5. DMA 컨트롤러가 입출력장치에서 데이터 읽은 후 메모리로 전송
6. 전송 완료 후 CPU에게 완료 신호 송신



![image](https://user-images.githubusercontent.com/58407737/223426384-79dda4ed-74cc-4c9c-91cd-604f39fcf5fa.png)

