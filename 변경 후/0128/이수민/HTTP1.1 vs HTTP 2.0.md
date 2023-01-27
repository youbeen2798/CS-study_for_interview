# HTTP/1.1
- 기본적으로 Connection당 하나의 요청을 처리 하도록 설계되었다.
- 동시 전송이 불가능하고 요청과 응답이 순차적으로 이루어져있다.
- HTTP 문서 안에 포함된 다수의 리소스 (Images, CSS, Script)를 처리하려면 요청할 리소스 개수에 비례해서 Latency(대기 시간)는 길어진다.

## 단점
### 1. HOL (Head Of Line) Blocking - 특정 응답의 지연
- connection당 하나의 요청 처리를 개선할 수 있는 기법 중 pipelining이 존재한다.
- cononection을 통해 다수개의 파일을 요청/응답 받을 수 있는 기법이다. </br>
![image](https://user-images.githubusercontent.com/58407737/215033718-ee152ec4-7494-4a14-976a-9910385b0301.png)

</br> </br> 
![image](https://user-images.githubusercontent.com/58407737/215034040-fbad481b-71df-434c-a0ff-59c85d43d03f.png)

### 2. RTT( Round Trip Time) 증가
- 하나의 connection에 하나의 요청을 처리한다.
- 그렇기에 매 요청별로 connection을 만들게 되고 TCP상에서 동작하는 HTTP의 특성상 3-way Handshake가 반복적으로 일어나고 또한 불필요한 RTT증가와 네트워크 지연을 초래하여 성능을 저하시킴  </br>

![image](https://user-images.githubusercontent.com/58407737/215034315-eb802980-ce61-4824-b0d4-5e81a03b8f44.png) </br>

### 3.무거운 Header 구조 (특히 Cookie)
- http/1.1의 헤더에는 많은 메타정보들을 저장한다.
- 매 요청 시 마다 중복된 Header 값을 전송하게 되며 별도의 domain sharding을 하지 않았을 경우 또한 해당 domain에 설정된 cookie 정보도 매 요청시마다 헤더에 포함되어 전송한다.
- 전송하려는 값보다 헤더 값이 더 큰 경우도 자주 발생한다.

</br> </br> 

### 단점 극복 방법
1. Image Spriting
2. Domain Sharding
3. Minify CSS/ JavaScript (코드 축소)
4. Data URI Scheme
5. Load Faster

</br> </br> 
### SPDY 등장
- 구글은 더 빠른 Web을 실현하기 위해 throughput 관점이 아닌 Latency 관점에서 HTTP를 고속화한 SPDY(스피디)라 불리는 새로운 프로토콜을 구현하였다.
- SPDY는 HTTP를 대치하는 프로토콜이 아니고 HTTP를 통한 전송을 재 정의하는 형태로 구현하였고, 실제 상당한 성능과 효율을 보여줘 HTTP/2 초안의 참고 규격으로 사용되었다. </br>

![image](https://user-images.githubusercontent.com/58407737/215035254-62a4833f-1f92-4ac8-9f29-ec81594ad226.png)

# HTTP/2.0
- 최종 사용자가 대기 시간, 네트워크 및 서버 리소스 사용을 인식한다.
- 하나는 브라우저에서 웹 사이트로의 단일 연결을 허용하는 것이다.

## 특징
### 1. Multiplexed Streams
- 한 커넥션으로 동시에 여러 개의 메시지를 주고 받을 수 있고, 응답은 순서에 상관없이 stream으로 주고 받는다.
- HTTP/1.1의 Connection Keep-Alive, Pipelining의 개선을 하였다. </br>
![image](https://user-images.githubusercontent.com/58407737/215035830-e6c20fa4-f252-4fb7-9b56-430383509708.png)

### 2. Stream Prioritization
- 클라이언트가 요청한 HTML 문서 안에서 CSS파일 1개와 Image 파일 2개가 존재하고 이를 클라이언트가 각각 요청하고 난 후 Image 파일보다 CSS파일의 수신이 늦어지는 경우 브라우저의 렌더링이 늦어지는 문제가 발생하는데 HTTP/2의 경우 리소스간 의존관계(우선순위)를 설정하여 이런 문제를 해결하였다. </br>
![image](https://user-images.githubusercontent.com/58407737/215036176-e28621e4-e802-4633-9e98-d5ba9b11b047.png)

### 3. Server Push
- 서버는 클라이언트의 요청에 대한 요청하지도 않은 리소스를 보내줄 수 있다.
- 클라이언트(브라우저)가 HTML문서를 요청하고 해당 HTML에 여러개의 리소스 (CSS, Image 등)가 포함되어 있는 경우 HTTP/1.1에서 클라이언트는 요청한 HTML문서를 수신한 후 HTML문서를 해석하면서 필요한 리소스를 재 요청하는 반면
HTTP/2에서는 Server Push기법을 통해 클라리언트가 요청하지 않은(HTML문서에 포함된 리소스) 리소스를 Push 해주는 방법으로 클라이언트의 요청을 최소화해서 성능 향상을 이끌어 냄
- PUSH_PROMISE라고 부르며 이를 통해 서버가 전송한 리소스에 대해선 클라이언트는 요청을 안함 </br>

![image](https://user-images.githubusercontent.com/58407737/215036718-16fe810e-532c-4a45-ad12-a4caf7be0887.png)

### 4. Header Compression
- Header 정보를 압축하기 위해 Header Table과 Huffman Encording 기법을 사용하여 처리하는데 이를 HPACK 압축방식이라 부르며 RFC 7551로 관리한다. </br>

![image](https://user-images.githubusercontent.com/58407737/215037038-18967a3c-7bbe-451d-806f-d5b3682fb674.png)



</br> 

### 간단하게 정리해보면 

</br>

HTTP/1.1은 출시 이후 지금까지 가장많이 사용되고 있는 클라이언트와 웹서버간 통신 프로토콜이다. </br>
HTTP/1.1은 연결당 하나의 요청과 응답을 처리하기 때문에 동시 전송 문제와 다수의 리소스를 처리하기에 소곧와 성능 이슈를 가지고 있다.</br>
![image](https://user-images.githubusercontent.com/58407737/215037354-59b9d896-c277-42e0-a51d-87cfbab9ee35.png)

그래서 1. HOL(Head Of Line) 2. Blocking-특정응답지연, 3. RTT(Round Trip TIme) 증가, 4. 헤비한 Header구조라는 문제점을 가진다. </br>

문제점을 해결하기 위해 이미지 스프라이트, 도메인 샤딩, CSS/JavaScript 압축, data URI등 사용하였다. </br>

성능 뿐만아니라 속도측에서 월등한 HTTP/2가 등장하였다. </br>
![image](https://user-images.githubusercontent.com/58407737/215038091-d8341965-d5da-4cfb-ac73-58de08b742e8.png)

1. Multiplexed Streams(한 커넥션에 여러개의 메세지를 동시에 주고 받을 수 있음)
2. Stream Prioritization(요청 리소스간 의존관계를 설정)
3. Server Push(HTML문서상에 필요한 리소스를 클라이언트 요청없이 보내줄 수 있음)
4. Header Compression(Header 정보를 HPACK압충방식을 이용하여 압축전송)



