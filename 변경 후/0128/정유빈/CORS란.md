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
- access-control-allow-origin은 CORS 헤더의 중요 요소 중 하나로 어떤 요청을 허용할지 결정한다.
- 이 헤더 값은 하나의 출처가 될 수 있고, "*" 를 사용해 어떤 출처도 허용할 수 있다.
- 만약 서버가 이 헤더에 응답하지 않거나, 헤더 값이 요청의 출처와 일치하지 않다면, 브라우저는 응답을 차단한다.
- 또한 요청한 출처가 서버의 access-control-allow-origin에 포함되어 있는 경우도 마찬가지이다.

<h4> 2. 프리 플라이트(Preflight Request) </h4>

- OPTIONS 메소드로 HTTP 요청을 미리 보내 실제 요청이 전송하기에 안전한지 확인한다.
- 다른 출처 요청이 데이터에 영향을 줄 수 있기 때문에 미리 전송한다.
- 요청 헤더에는 다음 값이 포함된다.
- 1. origin : 어디서 요청을 했는지 서버에 알려주는 주소
- 2. access-control-request-method : 실제 요청이 보낼 HTTP 메소드
- 3. access-control-request-headers : 실제 요청에 포함된 header

- 응답 헤더는 다음 값이 포함된다.
- 1. access-control-allow-origin : 서버가 허용하는 출처
- 2. access-control-allow-methods : 서버가 허용하는 HTTP 메소드 리스트
- 3. access-control-allow-headers : 서버가 허용하는 header 리스트
- 4. access-control-max-age : 프리 플라이트 요청의 응답을 캐시에 저장하는 시간

- 프리 플라이트 요청은 OPTIONS를 통해 자신의 주소를 보낸다.
- 또한 origin, access-control-request-method, access-control-request-headers를 같이 보낸다.
- 정상적인 응답으로 access-control-allow-origin, access-control-allow-method, access-control-allow-headers, access-control-max-age를 응답받는다.
- 정상 요청과 응답이 가능하다는 프리 플라이트 덕분에 실제 요청을 한다. 그리고 정상 응답을 받는다.

<h4> 신용 요청(Credentialed Request) </h4>
- 신용 요청은 쿠키, 인증 헤더, TLS 클라이언트 인증서 등의 신용정보와 함께 요청을 합니다.
- 기본적으로 CORS 정책은 다른 출처 요청에 인증 정보 포함을 허용하지 않습니다.
- 요청에 인증을 포함하는 플래그가 있거나 access-control-allow-credentials가 true로 설정한다면 요청할 수 있습니다.
- 만약 서버의 응답에 access-control-allow-credentials가 true로 설정되지 않았거나 access-control-allow-origin 헤더에 있는 값이 허용된 출처가 아니라면 오류가 발생한다.
