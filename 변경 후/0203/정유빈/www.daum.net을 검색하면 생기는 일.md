<h1> URL 입력 www.daum.net </h1>

검색 창에 www.daum.net을 입력하고 검색을 누르면 1초안에 벌어지는 일들을 설명드리겠습니다.

1. 검색을 하게 되면 우선 daum.net 도메인에 속해있는 www 컴퓨터 인터넷망에 통신하기 위해 daum Ip 주소를 알아야 한다.
2. IP 주소를 찾기 위해 캐시에서 DNS 기록을 확인한다. 인터넷 전화번호부와 같은 DNS는 웹사이트의 IP 주소와 도메인 주소를 연결해주는 시스템이다. DNS는 사람들이 쉽게 사이트 주소를 찾을 수 있도록 도와준다. DNS 기록을 찾기 위해서는 브라우저는 총 4개의 캐시를 확인한다.

    (2-1) DNS 쿼리는 이전에 방문한 웹 사이트의 DNS 기록을 일정 기간 동안 저장하고 있는 브라우저 캐시를 확인한다. </br>
    (2-2) 브라우저 캐시에 원하는 DNS 레코드가 없으면, 브라우저가 내 컴퓨터 OS에 시스템 호출을 통해 DNS 기록을 가져옵니다. (OS도 DNS 캐시를 저장하고 있다 - OS캐시) </br>
    (2-3) 컴퓨터에도 원하는 DNS 레코드가 없드면, 브라우저는 라우터에서 DNS 기록을 저장한 캐시를 확인한다. - 라우터 캐시 </br>
    (2-4) 위 단계 DNS 기록을 찾지 못한다면, 브라우저는 ISP에서 DNS 기록을 찾는다. ISP는 DNS 서버를 가지고 있는데, 해당 서버에서 DNS 기록 캐시를 검색할 수 있다 - ISP 캐시

번외)
왜 이렇게 많은 캐시가 유지되고 있을지 의문을 가질 수 있다.
캐싱된 정보가 개인 정보 보호에는 위험할 수 있지만, 캐시는 네트워크 트래픽을 규제하고 데이터 전송 시간을 개선하는데 필수적이다.

3. 요청한 URL이 캐시에 없다면, ISP의 DNS 서버가 DNS 쿼리로 www.을 호스팅하는 IP 주소를 찾습니다. </br>
    DNS 쿼리는 현재 DNS 서버에 원하는 IP 주소가 존재하지 않는다면 다른 DNS 서버를 방문하는 과정으로 IP 주소를 찾을 때까지 반복한다. </br>
    여러 DNS 서버에 검색을 한다.
    이러한 유형의 검색을 재귀적 질의라고 한다.
    
4.  전달받은 IP 주소를 이용해 브라우저는 해당 서버와 TCP 연결을 시작한다. </br>
    인터넷 통신을 해야하는데 HTTP 통신은 일반적으로 TXP 연결 기반이기 때문에 TCP 전송 프로토콜을 사용한다. TCP 3way handshake 과정을 통해 연결 및 데이터를 수신받아 TCP 연결을 설정한다.


5. TCP 연결 설정 후 브라우저는 웹 서버에 www.daum.com 웹 페이지를 요청하는 GET 요청(HTTP 요청)을 보낸다.</br>
    Browser Identification, 수신할 Request 종류, TCP Connection을 유지하는 Connection Header, browser에서 얻은 Cookie 정보 등 이러한 부가정보 들도 함께 전달된다.
    
6. 서버가 요청을 처리하고 response를 보낸다.

7. 서버가 HTTP Response를 다시 Browser에게 데이터를 전송한다.

8. 브라우저는 Response를 받아 파싱하여 화면에 랜더링 한다. </br>
    브라우저는 Http Content를 단계적으로 보여준다. </br>
    HTML 스켈레톤을 랜더링하고, HTML 태그들을 체크한 후 추가적으로 필요한 Image, CSS, JS 파일 등과 같은 웹 페이지 요소들을 GET으로 요청한다.
    
정적 콘텐츠들은 Browser에 의해 캐싱되어 나중에 재방문시, 다시 서버로부터 불러오는 등의 과정이 생략되어 빠른 속도로 웹 페이지가 띄어진다.

이러한 과정을 단 1초도 되지 않는 식나에 끝낸다.
