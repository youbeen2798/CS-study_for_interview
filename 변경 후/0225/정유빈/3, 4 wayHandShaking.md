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
- 일반적으로 TCP와 IP는 함께 사용되며, IP는 배달을, TCP는 패킷의 추적 및 관리를 하게 된다.
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

- <h3> 포트(PORT) 상태 번호 </h3>

  - CLOSED : 포트가 닫힌 상태
  - SYN-SENT : SYN 플래그를 보내고 기다리는 중
  - LISTEN : 포트가 열린 상태로 연결 요청 대기 중
  - SYN-RCV : SYNC 요청을 받고 상대방의 응답을 기다리는 중
  - ESTABLISHED : 포트 연결 상태

- <h3> 플래그 정보 </h3>

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

- TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 <b> 연결을 설정(Connection Establish) </b> 하는 과정
- 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이터 전달이 시작하기 전에 한 쪽이 다른 쪽이 준비되었다는 것을 알 수 있도록 한다.
- 즉, TCP/IP 프로토콜을 이용해서 통신을 하는 응용 프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 윙해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다.

<h3> 3-Way handshake의 기본 매커니즘 </h3>

- TCP 통신은 <b> PAR(Positive Acknowledgement with Re-transmission) </b>을 통해 신뢰적인 통신을 제공한다.

![image](https://user-images.githubusercontent.com/62228401/221327340-428fdf2a-0feb-47a5-acf2-15ddecf19c53.png)

- PAR을 사용하는 기기는 ACK를 받을 때까지 데이터 유닛을 재전송한다.
- 수신자가 데이터 유닛(세그먼트)이 손상된 것을 확인하면(Error Detection에 사용되는 transport layer의 Checksum을 활용), 해당 세그먼트를 없앤다.
- 그러면 sender는 positive ACK가 오지 않은 데이터 유닛을 다시 보내야 한다.
- 이 과정에서 클라이언트와 서버 사이에서 3개의 Segment가 교환되는 것을 확인할 수 있다.
- 이것이 바로 3-Way handshake의 기본 매커니즘이다.

<h1> 작동 방식 </h1>

- Client는 Server와 연결하기 위해 3-way Handshake를 통해 연결 요청을 하게 된다.
- 우리가 일반적으로 생각하는 Client와 Server는 모두 서로 연결 요청을 먼저 할 수 있기 때문에, 연결 요청을 먼저 시도한 요청자를 Client(아래 그림에서 HOST P)로, 연결 요청을 받은 수신자를 Server(아래 그림에서 HOST Q)로 생각할 수 있다.
- <b> SYN(Synchornization) </b> : 연결 요청, 세션을 설정하는데 사용되며 초기에 시퀀스 번호를 보냄
- <b> ACK(Acknowledgement) </b> : 보낸 시퀀스 번호에 TCP 계층에서의 길이 또는 양을 더한 것과 같은 값을 ACK에 포함하여 전송
  - 동기화 요청에 대한 답변 : Client의 Sequence Number에 1을 더하여 ACK로 돌려줍니다.

![image](https://user-images.githubusercontent.com/62228401/221327864-0fd7da67-cefb-4a05-9cb5-6dceb2a1bd67.png)

<h3> Step 1 <h3>
  
  - <b> 클라이언트는 서버와 커넥션을 연결하기 위해 SYN을 보낸다.(seq : X)  </b>
  
    - 송신자가 최초로 데이터를 전송할 때 Sequence Number를 임의의 랜덤 숫자로 지정하고, SYN 플래그 비트를 1로 설정한 세그먼트를 전송한다.
  - PORT 상태
    - Client : CLOSED - SYN_SENT로 변함
     - Server : Listen 
  
<h3> Step 2 </h3>

  - <b> 서버가 SYN(x)를 받고, 클라이언트로 받았다는 신호인 ACK와 SYN 패킷을 보냄(seq : y, ACK : x + 1) 
    - 접속 요청을 받은 Q가 요청을 수락했으며, 접속 요청 프로세스인 P도 포트를 열어달라는 메시지를 전송(SYN-ACK signal bits set)
  - ACK Number 필드를 Sequence Number + 1로 지정하고 SYN과 ACK 플래그 비트를 1로 설정한 세그먼트 전송(Seq = y, Ack = x + 1, SYN, ACK)
  - Port 상태
    - Client : CLOSED
    - Server : SYN_RCV </b>
  
  <h3> Step 3 </h3>
  
  - <b> 클라이언트는 서버의 응답인 ACK(x+1)와 SYN(y) 패킷을 받고, ACK(y+1)을 서버로 보냄
  
    - 마지막으로 접속 요청 프로세스 P가 수락 확인을 보내 연결을 맺음(ACK)
    - 이 때, 전송할 데이터가 있으면 이 단계에서 데이터를 전송할 수 있다.
    - PORT 상태
      - Client : ESTABLISHED
      - Server : SYN_RCV -> ACK -> ESTABLISHED
  
  <h3> full - duplex 통신의 구성 </h3>
  
  - Step 1, 2에서는 P -> Q 방향에 대한 연결 파라미터(시퀀스 번호)를 설정하고, 이를 승인한다.
  - Step 2, 3에서는 Q -> P 방향에 대한 연결 파라미터(시퀀스 번호)를 설정하고, 이를 승인한다.
  
  => 이를 통해 full-duplex 통신이 구축된다.
  
  
  <h1> TCP의 4-Way Handshake </h1>
  
  - 4-Way Handshake은 연결을 해제(Connection Termination)하는 과정이다.
  - 여기서 FIN 플래그를 이용한다.
    - FIN (finish) : 세션을 종료시키는데 사용되며, 더 이상 보낸 데이터가 없음을 나타낸다.
  
  <h1> Termination 종류 </h1>
  
  - TCP는 대부분의 connection-oriented 프로토콜과 같은 2가지 연결 해제 방식이 있다.
  
  <b> 1. Graceful connection release(정상적인 연결 해제) </b>
  - 정상적인 연결 해제에서는 양쪽이 커넥션이 서로 모두 커넥션을 닫을 때까지 연결되어 있다.
  <b> 2. Abrupt connection release(갑작스러운 연결 해제) </b>
  - 1. 갑자기 한 TCP 엔티티가 연결을 강제로 닫는 경우
  - 2. 한 사용자가 두 데이터 전송 방향을 모두 닫는 경우
  
  <h1> 작동 방식(Abrupt) </h1>
  
  - RST(TCP Reset) 세그먼트가 전송되면, 갑작스러운 연결 해제가 수행되는데, RST 세그먼트는 다음과 같은 경우에 전송된다.
  
  1. 존재하지 않는 TCP 연결에 대해 비SYN 세그먼트가 수신되는 경우
  2. 열린 커넥션에서 일부 TCP 구현이 잘못된 헤더가 있는 세그먼트가 수신되는 경우
    - RST 세그먼트를 보내, 해당 커넥션을 닫아 공격을 방지한다.
  3. 일부 구현에서 기존 TCP 연결을 종료해야 하는 경우
  
  - 연결을 지원하는 리소스가 부족할 때
  - 원격 호스트에 연결할 수 없고, 응답이 중지되었을 때
  
  <h1> 작동방식 (Abrupt) </h1>
  
  - 연결 종료 요청 역시, 일반적으로 생각하는 Client와 Server는 모두 서로 연결 요청을 할 수 있기 때문에, 연결 요청을 먼저 시도한 요청자를 Client로, 연결 요청을 받은 수신자를 Server쪽으로 생각하면 된다. 
  
  <h2> Half-Close 기법 </h2>
  
  - 아래 그림에서 처음 보내는 종료 요청인 <b> (1) FIN </b> 패킷에 실질적으로 ACK가 포함되어 있는 것을 알 수 있는데, 이는 <b> Half-Close 기법 </b>을 사용하기 때문이다.
  
  - 즉, 연결을 종료하려고 할 때 완전히 종료하지 않고 반만 종료한다.
  - Half-Close 기법을 사용하면 종료 요청자가 처음 보내는 FIN 패킷에 승인 번호를 함께 담아서 보내게 되는데, 이 때 승인번호의 의미는 <b> "일단 연결은 종료할 건데, 귀는 열어둘게. 이 승인 번호까지 처리했으니까 더 보낼 거 있으면 보내" </b> 가 됩니다.
  - 이후, 수신자가 남은 데이터를 모두 보내고 나면 다시 요청자에게 FIN 패킷을 보냄으로써 모든 데이터가 처리되었다는 신호 <b> (3) FIN </b>를 보냅니다.
  - 그럼 요청자는 나머지 반을 닫음녀서 좀 더 안전하게 연결을 종료할 수 있게 됩니다.

  ![image](https://user-images.githubusercontent.com/62228401/221329664-cdc4b3d9-43e4-47e5-875d-07bce31a2cbf.png)

  <h3> STEP1(Client -> Server : FIN( + ACK) </h3>
  
  - 서버와 클라이언트가 연결된 상태에서 클라이언트가 close()를 호출하여 접속을 끊는다.
  - 이 때, 클라이언트는 서버에게 연결을 종료한다는 FIN 플래그를 보낸다.
    - 이 때, FIN 패킷에는 실질적으로 ACK도 포함되어 있다.
  
  <h3> STEP2(Server -> Client : ACK) </h3>
  
  - 서버는 FIN을 받고, 확인했다는 ACK를 클라이언트에게 보내고 자신의 통신이 끝날 때까지 기다린다. ( 이 상태가 TIME_WAIT 상태)
    - Server(수신자)는 ACK Number 필드를 Sequence Number + 1로 지정하고, ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다.
  - 서버는 클라이언트에게 응답을 보내고 <b> CLOSE_WAIT </b> 상태에 들어갑니다. 그리고 아직 남은 데이터가 있다면 마저 전송을 마친 후에 close()를 호출
 - 클라이언트는 서버에서 ACK를 받은 후에 서버가 남은 데이터 처리를 끝내고 FIN 패킷을 보낼 때까지 기다립니다. (FIN_WAIT_2)
  
  <h3> STEP3(Server -> Client : FIN) </h3>
  
  - 데이터를 모두 보냈다면, 서버는 연결이 종료에 합의한다는 의미로, FIN 패킷을 클라이언트에게 보낸 후에, 승인 번호를 기다리는 LAST_ACK 상태로 들어간다.
  
  <h3> STEP4(Client -> Server : ACK) </h3>
  
  - 클라이언트는 FIN을 받고, 확인했다는 ACK를 서버에게 보낸다.
  - 아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT를 통해 기다린다.
  - 이 때, TIME_WAIT는 의도치 않은 에러로 연결이 데드락에 빠지는 것을 방지
  - 만약 에러로 인해 종료가 지연되다가 타임이 초과되면 CLOSED로 들어감
  
  - 서버는 ACK를 받은 후 소켓을 닫는다.(closed)
  - TIME_WAIT 상태가 끝나면 클라이언트도 닫는다.(closed)
