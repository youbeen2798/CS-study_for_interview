<h1> CORS란 </h1>

-  브라우저에서는 보안적인 이유로 cross-origin HTTP 요청을 제한한다.
- 따라서, cross-origin 요청을 하려면 서버의 동의가 필요하다.
- 만약 서버가 동의한다면 브라우저에서는 요청을 허락하고, 동의하지 않는다면 브라우저에서 거절한다.
- 이러한 허락을 구하고 거절하는 메커니즘을 HTTP-header를 이용하여 가능한데, 이를 CORS(Cross-Origin-Resource-Sharing)이라고 한다.
- 따라서 브라우저에서 cross-origin 요청을 안전하게 할 수 있도록 하는 메커니즘이다.

<h3> cross-origin </h3>

- cross-origin이란 다음 중 한 가지라도 다른 경우를 말한다.
1. 프로토콜 - http와 https는 프로토콜이 다르다.
2. 도메인 - domain.com과 other-domain.com은 다르다.
3. 포트번호 - 8080포트와 3000 포트는 다르다.

<
