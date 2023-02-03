## CORS란? (Cross-Origin Resource Sharing)
- HTTP 헤더를 사용하여, 한 출처에서 실행중인 웹 애플리케이션이 다른(프로토콜, 도메인, 포트번호)의 리소스에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제이다.
- 웹 어플리케이션은 리소스가 자신의 출처와 다를 때 Cross-Origin HTTP 요청을 실행한다.

</br>

- 도메인, 프로토콜, 포트 번호가 하나라도 다를 경우에 교차 출처(Cross-Origin)라고 판단되며 브라우저에서는 보안 때문에 Cross-Origin HTTP 요청을 제한한다.
- 권한을 부여 받기 위한 Cross-Origin 요청은 서버에서 허가를 받아야하는데, HTTP-Header를 통해 받을 수있다.

</br>

출처를 비교하는 방법은 URL 구성요소중 프로토콜, 호스트, 포트 세가지만 동일한지 확인하면 된다. </br>

같은 프로토콜, 호스트, 포트를 사용한다면 같은 출처로 인정되며, 리소스가 자신의 출처와 다를 경우 브라우저는 교차출처 요청을 실행한다. </br>

즉, 프로토콜, 포트, 호스트가 모드 일치하면 Same Origin이며, 하나라도 일치하지 않으면 Cross-Origin이다. </br>


![image](https://user-images.githubusercontent.com/58407737/216612775-704e06c8-5330-47e6-b8c1-223a71d8a082.png)

</br>

![image](https://user-images.githubusercontent.com/58407737/216612859-95dbb84c-8e33-4bc7-82dc-d4be5431cabb.png)


</br>
</br>

참고  </br>
https://hymndev.tistory.com/78 </br>
https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-CORS-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-%F0%9F%91%8F

