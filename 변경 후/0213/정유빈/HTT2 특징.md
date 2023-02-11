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
