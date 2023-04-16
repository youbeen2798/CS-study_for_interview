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
