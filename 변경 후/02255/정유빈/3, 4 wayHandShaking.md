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
- TCP는 연결형 서비스로, 신뢰적인 
