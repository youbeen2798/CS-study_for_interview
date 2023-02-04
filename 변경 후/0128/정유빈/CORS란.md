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

<h3> CORS는 왜 필요한가? </h3>

- CORS가 없이 모든 곳에서 데이터를 요청할 수 있게 되면, 다른 사이트에서 원래 사이트를 흉내낼 수 있게 된다.
- 예를 들어 기존 사이트와 완전히 동일하게 동작하도록 하여 사용자가 로그인을 하게 만들고, 로그인했던 세션을 탈취하거나 악의적으로 정보를 추출할 수 있다.
- 이렇게 공격을 할 수 없도록 브라우저에서 보호하고, 필요한 경우에만 서버와 협의하여 요청할 수 있도록 하기 위해 필요하다.
- 기본적으로 동일 출처 요청만 자유롭게 요청이 가능한 동일 출처 정책을 "Same-Origin-Policy"라고 한다.
- 하지만 기준을 완화하여 다른 출처 요청도 할 수 있도록 기준을 만든 체제가 다른 출처 정책 "Cross-Origin-Policy"이다.


<h3> CORS 요청 정책 3가지 </h3>

<h4> 1.단순요청</h4>

- GET, HEAD, POST만 가능
- Content-Type 헤더는 application/x-www-form-urlencoded, multipart/form-data, text/plain만 가능
- 브라우저는 자신의 주소를 origin에 담아 요청을 보내고, 서버는 접근이 가능하다는 access-control-allow-origin에 해당 주소를 담아 보낸다.
- access-control-allow-origin은 CORS 헤더의 중요 요소 중 하나로 어떤 
