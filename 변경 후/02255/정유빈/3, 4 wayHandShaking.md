<h1> Transport Layer </h1>

-  OSI 7 레이어에서 Transport Layer는 양 끝단(End to End) 사용자들이 신뢰성 있는 데이터를 주고 받을 수 있도록, 상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 않도록 해준다.
-  전송 계층은 인터넷 기반인 TCP/IP 참조 모델과 일반적인 네트워크 모델인 개방형 시스템 간 상호 접속(Open Systems Interconnection, OSI) 모두 포함하고 있다.
-  전송 프로토콜 중 잘 알려진 것이 바로 TCP와 UDP이다.

<h3> Transport Layer VS Network Layer </h3>

- Transport Layer : Application 프로세스 간의 논리적 통신을 제공
- Network Layer : host 간의 논리적 통신을 제공 ( 데이터의 전달 경로를 설정하는 역할 )

<h1> TCP와 UDP </h1>

- 트랜스포트 계층의 패킷을 "세그먼트"라고 한다.
- UDP에서는 종종 이를 "데이터 그램"이라고 한다.

<h1> TCP(Transmission Control Protocol) </h1>

- 인터넷 상에서 데이터를 메시지 형태로 보내기 위해 IP와 함께 사용하는 프로토콜

- TCP는 애플리케이션에게 신뢰적이고 연결지향성 서비스를 제공한다.
- 일반적으로 TCP와 IP는 함께 사용되며, IP는 배달을, TCP는 패킷의 추적 및 관리르 하게 된다.
- TCP는 연결형 서비스로, 신뢰적인 전송을 보장하기에 handshaking하고 데이터의 흐름 제어와 혼잡 제어를 수행합니다.
- 하지만 이러한 기능으로 인해 TCP의 속도는 느립니다.

<h3> TCP 특징 </h3>

- 3-way handshaking 과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제한다.
- 흐름 제어 및 혼잡 제어
- 높은 신뢰성을 보장한다.
- UDP보다 속도가 느리다.
- 전이중(Full-Duplex), 점대점(Point to Point) 방식

![image](https://user-images.githubusercontent.com/62228401/221325966-8d575834-8494-4103-9316-f090c3405444.png)

<h1> UDP(User Datagram Protocol) </h1>

- 데이터를 데이터그램 단위로 처리하는 프로토콜(데이터그램이란 독립적인 관계를 지니는 패킷이라는 뜻)
- UDP는 비연형 프로토콜
- 할당되는 논리적인 경로가 없고 각각의 패킷이 다른 경로로 전송되고, 이 각각의 패킷은 독립적인 관계를 지니게 되는데, 이렇게 데이터를 서로 다른 경로로 독립 처리하는 프로토콜을 UDP라고 한다.
- UDP는 연결을 설정하고 해제하는 과정이 존재하지 않는다.
- 서로 다른 경로로 독립적으로 처리함에도 패킷에 순서를 부여하여 재조립하거나 흐름제어 및 혼잡제어를 수행하지 않아 속도가 빠르며 네트워크 부하가 적다는 장점이 있지만 데이터 전송의 신뢰성이 낮다.
- 연속성이 중요한 실시간 서비스(스트리밍)에 좋다.

<h3> UDP 특징 </h3>

- 비연결형 서비스로 데이터그램 방식을 제공한다.
- 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다.
- UDP 헤더의 CheckSum 필드를 통해 최소한의 오류만 검출한다.
- 신뢰성이 낮다.
- TCP보다 속도가 빠르다.

![image](https://user-images.githubusercontent.com/62228401/221325991-43c5f714-ad56-4e44-890e-d4a7d1275dc6.png)

<h3> TCP vs UDP </h3>

- UDP와 TCP는 각각 별도의 포트 주소 공간을 관리하므로 같은 포트 번호를 사용해도 무방하다.
- 즉, 두 프로토콜에서 동일한 포트 번호를 할당해도 서로 다른 포트로 간주한다.
- 또한 같은 모듈(UDP or TCP) 내에서도 클라이언트 프로그램에서 동시에 여러 커넥션을 확립한 경우에는 서로 다른 포트 번호를 동적으로 할당한다. (동적할당에 사용되는 포트번호는 49,152 ~ 65,535이다.)

![image](https://user-images.githubusercontent.com/62228401/221326276-eab04c75-dad4-4935-b7d6-2e2980dc656b.png)

<h1> 3-Way Handshake와 4-Way Handshake </h1>

- 3-Way Handshake는 TCP의 접속, 4-Way Handshake는 TCP의 접속 해제 과정이다.

- <h1> 포트(PORT) 상태 번호 </h1>
  - CLOSED : 포트가 닫힌 상태
  - LISTEN : 포트가 열린 상태로 연결 요청 대기 중
  - SYN-RCV : SYNC 요청을 받고 상대방의 응답을 기다리는 중
  - ESTABLISHED : 포트 연결 상태

- <h1> 플래그 정보 </h1>

  - TCP Header에는 CONTROL BIT(플래그 비트, 6bit)가 존재하며, 각각의 bit는 "URG-ACK-PSH-RST-SYN-FIN"의 의미를 가진다.
    - 즉, 해당 위치의 bit가 1이면 해당 패킷이 어떠한 내용을 담고 있는 패킷이즐 나타낸다.
  - SYN(Synchronize Sequence Number) / 000010
    - 연결 설정. Sequence Number를 랜덤으로 설정하여 세션을 연결하는 데 사용하며, 초기에 Sequence Number를 전송한다.
  - ACK(Acknowledgement) / 010000
    - 응답 확인. 패킷을 받았다는 것을 의미한다.
    - Acknowledgement Number 필드가 유효한지를 나타낸다.
    - 양단 프로세스가 쉬지 않고 데이터를 전송한다고 가정하면 최초 연결 설정 과정에서 전송되는 첫 번째 세그먼트를 제외한 모든 세그먼트의 ACK 비트는 1로 지정된다.
  - FIN(Finsih) / 000001
    - 연결 해제. 세션 연결을 종료시킬 때 사용되며, 더 이상 전송할 데이터가 없음을 의미한다.

<h1> TCP의 3-Way Handshake </h1>
