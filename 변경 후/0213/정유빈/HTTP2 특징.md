<h1> HTTP? </h1>

- HyperText Transfer Protocol의 약자로, HyperText(링크를 통해 다른 문서로 연결될 수 있는 문서)를 Transfer(전송)라는 Protocol(규격이 정해진 규칙 
계이다.
- 다시 말해, 웹에서 클라이언트(브라우저)가 웹 서버 정보를 주고받는 프로토콜이다.

<h1> HTTP/1.0 </h1>

- 응답에 status code 추가 (브라우저가 요청에 대한 성공과 실패를 구별)

<h1> HTTP/1.1 </h1>

- 커넥션의 재사용 기능
  - Keep-Alive header를 통해 기존 연결과의 handshake 생략 기능

- Pipelining 추가
  - 이전 요청의 응답을 완전히 전송되기 전에 다음 요청을 가능하게 해서 통신 대기 시간을 낮춤
 
 
 <h1> HTTPS </h1>
 
 - TCP/IP 스택을 통해 HTTP를 전송하는 대신, 암호화된 전송 계층인 SSL을 만들었습니다.
 - 웹에서 주소록이나 이메일, 사용자의 위치 정보나 개인정보에 접근하면서 점점 보안의 중요성이 대두되면서 생겨났으며, SSL은 TLS로 발전해왔습니다.
 - 현재는 SSL이 아닌 TLS를 사용하지만, 보편적으로 SSL이라고 부르기 때문에 SSL/TLS를 혼용하여 부른다.

<h1> HTTP/1.1 동작 원리 </h1>

![image](https://user-images.githubusercontent.com/62228401/218254784-c5599da3-fd5d-4174-9942-938de8331a49.png)

- 왼쪽은 HTTP/1.1 Baseline 통신 규약이고, 오른쪽이 바로 Pipelining 기능이 도입된 HTTP/1.1 통신 과정입니다.
- HTTP/1.1 동작은 기본적으로 Connection 한 개당 하나의 요청을 처리하도록 설계되어있습니다.
- 동시 전송이 불가능하고 요청과 응답이 순차적으로 이루어집니다.
- 그래서, 이미지 세 개를 요청한다고 하면 아래와 같습니다.

![image](https://user-images.githubusercontent.com/62228401/218254860-142fea53-45bb-4d13-8386-9bdb2bb59e0d.png)

- 또, HTML 문서 안에 포함된 다수의 리소스(Images, CSS, Script)를 처리하려면 요청할 리소스 개수에 비해서 Latency(대기 시간)은 길어지게 됩니다.

<h1> HTTP/1.1 단점 </h1>

<h3> 단점 1. HOL Blocking </h3>

- Head Of Line Blocking
- HTTP/1.1의 Pipelining은 한 커넥션에 순차적인 여러 요청을 연속적으로 하고, 그 순서에 맞춰 응답을 받는 방식으로 지연 시간을 줄였습니다.
- 하지만, 순차적으로 응답을 받다보니 이전에 받은 응답이 길어지면 그 이후의 응답들은 지연된다.
- 예를 들어, 3개의 이미지를 받기 위해 아래와 같이 순서대로 요청을 보냈다고 했을 때, 이 순서에 맞게 응답을 받아야 한다.

![image](https://user-images.githubusercontent.com/62228401/218255029-9d3d875f-c35c-4add-9346-0256bfbdb23c.png)

- a.png의 응답이 길어지면 뒤에 있는 응답도 그에 따라 지연되게 되는 문제점이 있다.

<h3> 단점 2. RTT(Round Trip Time) 증가 </h3>

- HTTP/1.1의 동작원리에서 일반적으로 Connection 하나에 요청 한 개를 처리한다.
- 매번 요청 별로 Connection을 만들고 TCP 상에서 동작하는 HTTP의 특성 상 3-Way HandShake가 반복적으로 일어나며, 불필요한 RTT 증가와 네트워크 지연을 초래하여 성능을 지연시킬 수 있다.
- 참고로 RTT란, 요청(SYN)을 보낼 때부터 요청에 대한 응답(SYN+ACK)을 받을 때까지의 왕복 시간을 의미한다.

<h3> 단점 3. 무거운 Header 구조 </h3>

- HTTP/1.1은 여러 발전을 해오면서 헤더에 많은 메타 정보들을 저장하게 되었습니다.
- 사용자가 방문한 웹 페이지는 다수의 http 요청이 발생하게 되는데, 이 경우 매 요청 시마다 중복된 헤더 값을 전송하게 됩니다.
- 또한 해당 domain에 설정된 cookie 정보도 매 요청시마다 헤더에 포함되어 전송되어 성능을 저하시킨다.
- 
