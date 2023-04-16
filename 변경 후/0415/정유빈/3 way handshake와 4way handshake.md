<h1> 3 way handshake </h1>

- TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 연결을 설정(connection Establish) 하는 과정
- TCP 통신은 PAR(Positive Acknowlegement with Re-transmission)을 통해 신뢰저긴 통신을 제공한다.
- <b> PAR을 사용하는 기기는 ack를 받을 때까지 데이터 유닛을 재전송한다. </b>
- 수신자가 데이터 유닛(세그먼트)이 손상된 것을 확인하면(Error Detection에 사용되는 transport layer의 checksum을 활용), 해당 세그먼트를 없앤다.
- 그러며 sender는 positive ack이 오지 않은 데이터 유닛을 다시 보내야 한다. 
- TCP 프로토콜은 연결지향적이다.
- 따라서 상대방이 내 신호를 받을 수 있는지 확인하고 전송하는 것을 의미한다.
- 이 때, 내 신호를 받을 수 있는지 확인하는 것이 3 way handshake이다.

<h2> 3 way handsahke의 동작 과정 </h2>

<b> 1단계  - 들려?</b>

- 클라이언트가 연결 요청 메시지(SYN)을 전송한다.
- 클라이언트는 Synchronzied Sequence Number(SYN)이라는 임의의 랜덤 숫자를 함께 전송한다.

<b> 2단계 - 응 들려! 너도 들려? </b>

- 서버가 요청을 수락하며, 클라이언트에게 들리냐는 연결 요청 메시지를 전송한다.
- 그 메시지에 Acknowledgement number(ACK)를 포함하고 있으며, 이 번호는 받은 Synchronize Sequence Number(SYN)보다 +1한 값을 가집니다.
- 이 번호를 전송함으로써, 잘 들린다는 것을 알려줍니다.
- 그리고, 클라이언틍게ㅔ 전송이 잘 되냐고 물어봅니다. 동일하게 Sequence Number를 전송합니다.

<b> 3단계 - 응 들려! </b>

- 클라이언트가 그 질문이 잘 들린다고 Acknowledgement number(ACK)에 받은 Sequence number + 1해서 전송합니다.

<h1> 4-Way-HandShake </h1>

- 4-way handshake는 연결을 해제(Connection Termination) 하는 과정이다.
- 여기서는 FIN 플래그를 이용한다.
- FIN(finish) : 세션을 종료시키는데 사용되며, 더 이상 보낸 데이터가 없음을 나타낸다.
- Half-Close 기법을 사용

<h3> Half-Close 기법이란? </h3>

- 연결을 종료하려고 할 때 완전히 종료하지 않고 반만 종료한다.
- Half-Close 기법을 사용하면 종료 요청자가 처음 보내는 FIN-패킷에 승인 번호를 함께 담아서 보내게 되는데, 이 때 승인 번호의 의미는 "일단 연결은 종료할 건데, 귀는 열어 둘게. 이 승인 번호까지 처리해놨으니가, 더 보낼 거 있으면 보내"이다.
- 이후 수신자가 남은 데이터를 모두 보내고 나면 다시 요청자에게 FIN 패킷을 보냄으로써 모든 데이터가 처리되었다는 FIN을 보낸다. 그럼 요청자는 그때 나머지 반을 닫으면서 좀 더 안전하게 연결을 종료할 수 있다.

<h2> 4-way-handshake 동작 과정 </h2>

<b> STEP1(Client -> Server : FIN) </b>

- 서버와 클라이언트가 연결된 상태에서 클라이언트가 close()를 호출하여 접속을 끊는다.
- 이 때, 클라이언트는 서버에게 연결을 종료한다는 FIN 플래그를 보낸다.

<b> STEP2(Server -> Client : ACK) </b> 

- 서버는 FIN을 받고, 확인했다는 ACK를 클라이언트에게 보내고 자신의 통신이 끝날 때까지 기다린다.
- 서버는 클라이언트에게 응답을 보내고 CLOSE_WAIT 상태에 들어간다. 그리고 아직 남은 데이터가 있다면 마저 전송을 한 후에 close() 호출
- 클라이언트는 서버에게 ACK를 받은 후에 서버가 남은 데이터 처리를 끝내고 FIN 패킷을 보낼 때까지 기다리게 된다.

<b> STEP3(Server -> Client : FIN) </b> 

- 데이터를 모두 보냈다면, 서버는 연결이 종료에 합의한다는 의미로 FIN 패킷을 클라이언트에 보낸 후에, 승인 번호를 보내줄 때까지 기다리는 LAST_ACK 상태로 들어간다.

<b> STEP4(Client -> Server : ACK) </b>

- 클라이언트는 FIN을 받고, 확인했다는 ACK를 서버에게 보낸다.
- 아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT를 통해 기다린다.
- 이 때, TIME_WAIT 상태는 의도치 않은 에러로 인해 연결이 데드라게 빠지는 것을 방지
- 만약 에러로 인해 종료가 지연되다가 타임이 초과되면 CLOSED로 들어간다. 

- 서버는 ACK를 받은 후 소켓을 닫는다. (closed)
- TIME_WAIT 시간이 끝나면 클라이언트도 닫는다. (closed)
