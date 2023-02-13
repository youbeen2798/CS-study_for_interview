기존에 햇갈리던 것 
HTTP 보다 HTTPS가 더 빠르다(?) 
- http/2는 http보다 빠르다. 
- 여기서 이야기가 나온것은 http2가 https로만 동작해서 이러한 이야기가 나오는것같음
- http1.x에도 https를 사용할 수 있다.
- http(번호)는 통신 규역버전이고 https는 보안이 추가된 것이다!!!! 

</br></br>
해당 논쟁으로 이해-> https://okky.kr/articles/480266 </br></br>

https://americanopeople.tistory.com/115

HTTP/2는 2015년 05월에 공개 -> HTTP 1.1 발표는 1997년도 </br>

그 사이에 웹 처리되는 방식이 많이 바뀜 </br>

1. 필요한 리소스의 양이 달라짐
2. 전에 비해 웹페이지가 동적으로 작용한다.

HTTP1이 느린 이유는 </br>

HTTP1에서는 앞에 날렸던 요청의 응답을 받아야만 다음 요청이 처리될 수 있다. </br>

![image](https://user-images.githubusercontent.com/58407737/218381774-bb45c149-0e25-4dc8-81cd-f155c1ccce54.png)

</br>
HTTP1.0 버전대만 하더라도, Request를 날릴 때마다  Connection을 새로 생성했다. -> 비효율적 
</br> 

HTTP1.1에서는 지속 커넥션, HTTP 파이프라이닝이라는 개념 등장 </br>
커넥션을 재사용할 수있고, Request를 미리 여러개 서버에 날릴 수 있다. </br>
하지만 이러한 개선에도 Request를 보낸 순서대로 Response를 받을 수 있다는 지점에서 문제가 발생했다. </br>

### Head of line blocking 
![image](https://user-images.githubusercontent.com/58407737/218382156-00d02b24-976b-4786-91ae-6c2bcd4cc609.png)

</br>

처음에 요청한 Request에 문제가 있어서 응답이 늦어지면 2번째, 3번째 요청한 Request의 응답도 같이 늦어진다는 문제점 발생한다. </br>

</br>

HTTP1 환경에서 웹 브라우저에 웹페이지를 보여줄 때, 한 Connection에서 Request를 보내고 Response를 받기를 기다리고, 다시 또 이를 순차적으로 반복하는건 시간이 오래 걸린다. </br>

그래서 최적화 방법중 하나인 **도메인샤딩**

</br>

![image](https://user-images.githubusercontent.com/58407737/218382552-da9aeea1-238a-40a4-9403-80179895ec9e.png)

</br>

서버는 같지만, 도메인명을 여러개 설정해서 이를 리소스 주소로 내려주면, 한 브라우저에서 여러개의 커넥션을 맺을 수 있게 된다. </br>
이렇게 되면, 리소스를 병렬적으로, 동시다발로 받을 수 있게 된다. </br>

하지만 브라우저별로 도메인 커넥션 갯수 제한 있고 너무 많은 도메인을 연결하는 경우 DNS 검색과 TCP Handshake에서 발생하는 시간 때문에 근본 해결책으로는 되지 못했다. </br>

HTTP2에서는
### 개선된 Multiplexing 등장
![image](https://user-images.githubusercontent.com/58407737/218383290-d9136827-36ad-4145-8ba5-2bed11ce13b7.png)
</br>

HTTP 1.1에서는 한 Request 당 한개의 리소스를 받아올 수 있다.(Request -> Response) </br>

HTTP/2는 Multiplexed Stream을 이용해 Connection 한 개로 여러개의 메시지를 주고 받을 수 있으며 응답은 순서에 상관없이 Stream으로 주고 받는다. </br>
RTT 시간(클라이언트에서 서버로 Request를 보내고 서버에서 처리하고 다시 돌아오기까지의 시간= 패킷 왕복거리) 시간을 줄어들어 별도의 최적화 과정이나 도메인 샤딩없이 웹 사이트 로드 속도가 빨라진다.  </br>

HTTP/1.1의 Connection Keep-Alive, Pipelining이 개선되었다. 

###  Binary Protocol
기존의 HTTP1은 플레인텍스트로 구성되어 있다. </br>
HTTP2에서는 데이터를 전송할 때, 바이너리로 인코딩하여 전송하게 되었다. </br>
바이너리 포멧의 데이터를 사용하게 되어, 이전에는 한 뭉태기로 모여있던 데이터를 프레임이라는 단위로 나눠서 관리 전송할 수 있게 되었다. </br>

- 데이터의 파싱이 더 빠르고, 오류 발생 가능성이 낮음
- 네트워크 리소스의 효과적 사용 (네트워크 지연 시간을 줄이고 처리량을 개선)
- 텍스트 특성과 관련된 보안 문제를 해결할 수 있음

### Header Compression
HTTP/2는 중복 헤더 프레임을 압축해서 전송한다. HPACK 규격을 사용하는데 클라이언트와 서버에서 모두 이전 요청에 사용된 헤더 목록을 유지관리한다. </br>
HPACK은 서버로 전송되기 전에 각 헤더의 개별 값을 압축한 다음 이전에 전송된 헤더 값 목록에서 인코딩된 정보를 조회하여 전체 헤더 정보를 재구성한다.  </br>

![image](https://user-images.githubusercontent.com/58407737/218385964-552d52c7-0afe-4ba3-a47c-7d753d36987f.png) </br>

위 그림처럼 클라이언트가 두번의 요청을 보낸다고 가정하면 HTTP/1.x의 경우는 두개의 요청 header에 중복값이 존재해도 그냥 중복 전송한다. </br>
하지만, HTTP/2에선 Header에 중복값이 존재하는 경우 static/Dynamic Header Table 개념을 사용해 중복 Header를 검출하고 중복된 Header는 index값만 전송하고 중복되지 않은 Header 정보의 값은 Huffman Encoding 기법으로 인코딩 처리하여 전송한다. </br>

![image](https://user-images.githubusercontent.com/58407737/218386347-08744c7f-9e05-434d-bf07-db672a3b1c8a.png)

 </br>

### Stream Prioritization 
HTTP 1.1에서 HTTP 요청과 응답은 메시지라는 단위로 구성되어 있다. 메시지는 Header/Body 등의 데이터로 구성되어 있다.  </br>
그런데 HTTP2에서는 Frame과 Stream이라는 개념이 추가됐다.  </br>

Frame은 HTTP2 통신에서 데이터를 주고받을 수 있는 가장 작은 단위다. (헤더 프레임, 데이터 프레임으로 구성)  </br>

메시지는 HTTP1.1처럼 요청과 응답의 단위이다. 메시지는 다수의 Frame으로 구성되어 있다.  </br>

Stream은 클라이언트와 서버사이에 맺어진 연결을 통해 양방향으로 데이터를 주고받는 한개 이상의 메시지를 의미한다.  </br>

즉, 프레임이 여러개가 모여 메시지가 되고, 메시지가 여러개가 모여 스트림이 되는 구조다.  </br>


HTTP1 시절에는 요청과 응답이 메시지라는 단위로 완벽하게 구분되었다. HTTP2에서는 스트림이라는 단위로 요청과 응답이 묶일 수 있는 구조이다.  </br>

HTTP2는 스트림 하나가 다수개의 요청과 응답을 처리할 수 있는 구조이다.  </br>
동시에 여러 메시지를 처리할 수 있게 되었고 응답 프레임들은 요청 순서에 상관없이 만들어진 순서대로 클라이언트에 전달될 수 있게 되었다.  </br>

문서 내에 CSS파일 1개 이미지 파일 2개가 존재하고 이를 클라이언트가 요청을 한다.  </br>
이미지 파일보다 CSS파일의 수신이 늦어지면 브라우저 렌더링에 문제가 생기게 될 수 있는데 HTTP/2는 이러한 상황을 고려해 리소스간의 의존관계에 따른 우선순위를 설정하여 리소스 문제를 해결하였다. 

그래서 HTTP1때처럼 중간에 응답이 막히면, 대기하고 있던 Response들이 모두 기다려야하는 HeadOfBlocking이슈에서 벗어날 수 있다.  </br>

</br>


### Server Push
기존의 속도 개선 하기 위해 요청수 자체를 줄이는 방법  </br>
1. Image Splite CSS - 큰 이미지 한 번에 받아와 CSS로 이미지를 쪼개서 웹페이지에 보여주는 방법
2. Data URI Scheme - 이미지를 BASE 64인코딩을 사용해서, 이미지 코드로 보여주는 방식 
3. JavaScript, CSS 리소스 요청수 최적화 - 파일 압축 (하나로 합치면 JS/CSS 데이터를 각각 한번만 내려받으면 된다.) 

이런 방법을 사용하지 않아도 된다. Server Push가 있기 때문에!!  </br>

![image](https://user-images.githubusercontent.com/58407737/218388230-a67c780a-2790-454e-828b-3c51f729d78b.png)

기존의 동작 방식은 
1. 애플리케이션에서 HTML 태크 데이터를 내려주고
2. 브라우저는 태그를 파싱해, 요청을 날려야하는 리소스들이 무엇인지 파악한다.
3. CSS/ JS/ 이미지 등을 요청해서 받아온다.
4. 브라우저에 뿌져준다.

</br>

웹 브라우저에서 리소스를 보려면 계속 기다려야한다. 하지만 애플리케이션은 본인이 어떤 데이터를 받아봐야하는지 알고 있었다. </br>

브라우저에서 필요한 리소스들이 이미 서버에 있는 로직들이라면, 웹브라우저가 다시 Connection을 맺고, Request를 날리기까지 기다리는건 비효율적이다. </br>


Server Push는 **브라우저에서 필요한 리소스들을 서버가 알아서 찾아다가 내려주는걸 의미** 한다. </br>

그래서 HTML 태그에서 필요한 리소스가 뭔지 찾기 전에, HTML 태그를 받은 즉시, 리소스 (CSS,JS,IMAGE)를 페이지에 그릴 수 있게 되었다. </br>





