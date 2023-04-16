![image](https://user-images.githubusercontent.com/58407737/232274625-d13cf4b7-2f19-49a2-b313-0cbd3ee7e358.png)

위에 Addresses 는 Naver의 기본 IP 주소이다. </br> </br>

최초의 주소는 IP 주소이다. </br>
- HTTP:// ~ (주소) 
- 처음에는 http://223.130.200.107 로 썼었다. 
- IP 주소를 다 외울 수 없기 때문에 도메인이라는 것을 신청한다. 그래서 IP 주소 대신 도메인을 사용함.

- 점점 보안이 중요해지고 있다. 
- 클라이언트와 서버(Naver)는 실시간 통신을 해야한다( 로그인, 검색 등) -> 데이터 주고 받음 
- 그 데이터를 암호화해서 통신한다는 것을 보증한다는 것이 HTTPS이다.

- Http는 통신을 주고 받을 때의 데이터들을 암호화 하는 것을 보증하지 않겠다 이고, HTTPS는 해커가 데이터를 가로채도 가로채도 가로챈 데이터는 암호화 되어있다.라고 인증한다. </br>

- 인증 기관이 있고, Naver에서는 인증을 받은 것이다.

![image](https://user-images.githubusercontent.com/58407737/232275218-049af16d-4876-4678-b04b-35b3e0c95060.png) </br>

하지만 https://223.130.200.107  이러면 안나오는 이유는?
- https는 도메인 네임에 대한 시큐어를 보장한다.
- 즉, HTTPS는 IP에 대한 암호화 보장이 아닌 도메인에 대한 암호화 보장을 하는 것이다. 
 
 
 # HTTP (Hypertext Transfer Protocol)
 - 서로 다른 시스템들 사이에서 통신을 주고받게 하는 가장 기본적인 프로토콜이다.
 - 서버에서 브라우저로 데이터를 전송하는 용도로 가장 많이 사용한다.
 - 데이터 통신할 때 암호화 되지 않는다는 문제점을 가지고 있다.
 - 데이터 도난 위험이 있다.

</br>

# HTTPS(Hypertext Transfer Protocol Secure)
- SSL(보안 소켓 계층) 사용
- SSL은 서버와 브라우저 사이에 안전하게 암호화된 연결을 만들 수 있게 도와주고, 서버와 브라우저가 민감한 정보를 주고받을 때 해당 정보가 도난당하는 것을 막하준.
- HTTP 자체를 암호화하는 것이 아니라 HTTP 메시지 Body를 암호화한다.

</br>

### HTTP Header은 암호화 하지 않는 이유?
- HTTP Header는 요청/응답에 대한 정보를 포함하고 있다. (요청/응답에 대한 메타 데이터이고, 민감 정보가 없기 떄문에 암호화 하지 않아도 된다.)
- 또한, HTTP header를 암호화 한다면 필요한 메타데이터를 해독하고 처리하는 데 추가적인 처리 과정이 필요하므로 성능 저하가 일어나기 때문이다.
- 이는 웹사이트의 성능에 영향을 미치기 때문에 HTTPS를 사용하지 않는 이유중 하나이다.  

</br>

### 사용해야하는 이유?
1. 암호화
2. SEO (검색엔진 최적화)
- 구글은 HTTPS 웹 사이트에 가산점을 부여 -> 우선적으로 HTTPS를 노출 시킴
- AMP(가속화된 모바일 페이지)를 만들 때에는 HTTPS를 사용해야함 -> AMP는 구글에서 만들었음

</br>

## SSL/TSL
- SSL의 Upgrade version이 TSL 이다.
- 일반적으로는 두 단어를 동일하게 사용한다.

- SSL 인증서 발급 기관: Let's Encrypt, AWS Certificate Manager (무료로 발급 해줌)

## SSL (Secure Sockets Layer)
- Netscape Communications Corporation에서 웹 서버와 웹 브라우저간의 보안을 위해 만든 프로토콜이다.
- 공개키/개인키 대칭키 기반으로 사용함 (두 방식을 혼합해서 사용함)

### 대칭키
![image](https://user-images.githubusercontent.com/58407737/232277993-b3fe1f8f-b7df-4d94-932b-1ec16ca1d6be.png) </br>

- 누구든지 암호화된 키를 가지고 있다면 복호화 시킬 수 있다.
- 암호화, 복호화가 쉽다.
- Key를 배송할 때 문제가 될 수 있다.


### 공개키 (= 비대칭키)
![image](https://user-images.githubusercontent.com/58407737/232278222-23a407ef-aac8-4018-a751-1ef01d5e8275.png) </br>

- 서로 다른 키로 암호화, 복호화 진행한다.
- 암호화시 -> 공개키
- 복호화시 -> 개인키 

- 공개키로 암호화된 데이터는 오직 개인키로만 복호화 할 수 있기 때문에 누구든지 공개키를 가져도 된다. (중간에 해커가 가로채도 문제 발생X)
- 키배송 문제는 없지만, 암호화 연산 시간이 더 소요되어 비용이 크다. 

</br>

이러한 이유로 공개키/ 대칭키 방식을 혼합해서 사용한다. 

### SSL 통신과정
- 공개키 방식으로 대칭키를 전달하고, 대칭키를 활용하여 암호화/복호화를 하고 서버와 브라우저 통신을 주고 받는다. 

</br>

(1) </br>
![image](https://user-images.githubusercontent.com/58407737/232278369-72f236b6-6820-4688-992b-3bce595326c4.png) </br>
A가 B에게 접속 요청을 한다. 

</br>

(2) </br>
![image](https://user-images.githubusercontent.com/58407737/232278499-2829242c-eccf-4814-bbf5-55c52bfb98ad.png) </br>
B는 A에게 자신의 공개키를 전달해준다. 

</br>

(2) </br>
![image](https://user-images.githubusercontent.com/58407737/232278526-73378286-9e09-41c9-9702-6ca317280938.png) </br>
A는 자신의 대칭키를 B에게 전달받은 B의 공개키로 암호화 한다. 

 </br>
 
 
(3) </br>
![image](https://user-images.githubusercontent.com/58407737/232278617-bc123e0a-c92c-4f51-a7d6-4d2e7e468be4.png) </br>
암호화된 대칭키를 B에게 전달을 한다.

</br>
 
 
(4) </br>
![image](https://user-images.githubusercontent.com/58407737/232278651-ae0c4160-b78e-4f67-9c85-530942899d12.png) </br>
B는 A의 대칭키를 자신의 개인키로 복호화 한다.  </br>

(5) 복호화 결과로 B는 A의 대칭키를 얻어낼 수 있다.

 </br>
 
(6)  </br>
![image](https://user-images.githubusercontent.com/58407737/232278721-28b1dbec-e92d-4551-b213-adf65446fe59.png)  </br>

이렇게 얻어낸 키로 안전하게 통신을 진행한다.   </br>


사이트는 사이트 정보와 사이트 공개키를 인증기관에 전달한다. 
인증기관에서는 전달받은 정보를 검증을 하고 검증이 성공적으로 되면 자신의 개인키로 서명한다. -> 사이트 인증서가 생성된다.
생성된 인증서를 다시 사이트에게 전달한다. 
그리고 인증기관은 사용자에게 인증기관 공개키를 전달해주고 그 공개키는 사용자 브라우저에 자동적으로 내장 된다.


