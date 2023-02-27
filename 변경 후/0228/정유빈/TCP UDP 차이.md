<h1> TCP와 UDP 차이 </h1>

- 전송 계층은 송신자와 수신자를 연결하는 통신 서비스를 제공하는 계층으로, 쉽게 말해 데이터의 전달을 담당
- 그리고 데이터를 전송하기 위해 사용하는 프로토콜이 있는데, 그 프로토콜들이 TCP와 UDP

![image](https://user-images.githubusercontent.com/62228401/221562329-99688a08-0541-42c4-b75a-ec1c9fe84621.png)

<h1> TCP(Transmission Control Protocol) </h1>

- TCP란 전송을 제어하는 프로토콜(규약)이라는 뜻인데, 아래의 정의와 같다.
- <b> "인터넷 상에서 데이터를 메시지의 형태로 보내기 위해 IP와 함께 사용하는 프로토콜" </b>
- 일반적으로 TCP와 IP를 함께 사용하는데, IP가 데이터의 배달을 처리한다면 TCP는 패킷을 추적 및 관리하게 된다.
- TCP는 연결형 서비스를 지원하는 프로토콜로, 인터넷 환경에서 기본으로 사용한다.

![image](https://user-images.githubusercontent.com/62228401/221562837-b17a0e9e-4381-4f4f-bed1-30b47ffc78fa.png)

<h3> TCP 특징 </h3>

- 연결 지향 방식이다.
- 3-way handshaking 과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제한다.
- 흐름 제어 및 혼잡 제어
- 높은 신뢰성을 보장한다.
- UDP보다 속도가 느리다.
- 전이중(Full-Duplex), 점대점(Point to Point) 방식

- TCP가 연결 지향 방식이라는 것은 패킷을 전송하기 위한 논리적 경로를 배정한다는 말이다.
- 또한, 3-way handshaking 과정은 목적지와 수신지를 확실히 하여 정확한 전송을 보장하기 위해서 세션을 수립하는 과정을 의미한다.
- TCP는 연결형 서비스로 신뢰성을 보장하는데, 따라서 3-way handshaking, 흐름제어, 혼잡제어와 같은 기능이 있다.(물론, 이러한 기능 때문에, UDP보다 속도가 느리며, CPU를 사용하기 때문에 속도에 영향을 준다.)
- 
