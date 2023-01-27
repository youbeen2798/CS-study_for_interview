<h1> Http Method </h1>

- 클라이언트와 서버 사이에 이루어지는 요청(Request)과 응답(Response) 데이터를 전송하는 방식을 일컫는다.
- 쉽게 말해, 서버에 주어진 리소스에 수행하길 원하는 행동, 서버가 수행해야 할 동작을 지정하는 요청을 보내는 방식이다.

<h1> 주요 메소드 </h1>

<h2> 1. GET </h2>

  - 리소스 조회
  - 서버에 전달하고 싶은 데이터는 "QueryString"을 통해 전달
    - GET/members/100?username=inpa&height=200
  - "QueryString" 외에 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 서버에서 따로 구성해야 하기 때문에, 지원하지 않는 곳이 많아서 권장하지 않음
  - 조회할 때, POST를 사용할 수 있지만, GET 메소드는 캐싱이 가능하기에 GET을 사용하는 것이 유리하다.
 
 <h3> GET - 정적 데이터 조회 과정 </h3>
 
 1. 이미지, 정적 텍스트 문서 GET </br>
 2. 쿼리 파라미터 없이 리소스 경로로 단순 조회 가능 </br>
    
 <h4> 1. 클라이언트에서 /members/100으로 100번 멤버를 조회해서 정보를 달라고 GET 요청 </h4>
    
 ![image](https://user-images.githubusercontent.com/62228401/214473281-43c5ff24-5698-46c9-b724-01171060c5c4.png)
    
 <h4> 2. 서버에서는 요청 메시지를 분석해 내부의 유저 정보를 조회한 뒤 결과 Response를 만든다. </h4>

![image](https://user-images.githubusercontent.com/62228401/214473395-9c369483-cf35-4fb1-a1d5-3d083b7dc695.png)
 
 <h4> 3. 서버에서 클라이언트로 응답을 해준다. 그러면 클라이언트에서 정상적으로 받으면 200 OK status를 가지며, 회원정보를 얻게 된다. </h4>
 
 ![image](https://user-images.githubusercontent.com/62228401/214495834-4a184db9-f6ad-4a72-8b83-f60484157fd3.png)

  <h3> GET - 동적 데이터 조회 과정 </h3>
  
  1. 주로 검색, 게시판 목록에서 검색어로 이용
  2. 쿼리 파라미터 사용해서 데이터를 전달
  3. 쿼리 파라미터는 key1 = value1 & key2 = value2 구조로 되어 있음

  <h4> 요청 url 뒤에 ?q=hello&h2=ko 쿼리 파라미터를 주서 상세한 조회 데이터를 얻는다. </h4>
  
  ![image](https://user-images.githubusercontent.com/62228401/214496671-a72beaa2-7936-499d-be34-038f24be9b1c.png)

  <h3> HTML Form 데이터 조회 과정 </h3>
  
  1. HTML Form 태그 문서로 사용자와 UI로 상호작용하여 서버와 통신
  2. HTML Form 전송은 GET, POST만 지원

  <h4> 웹문서에서 폼 입력칸에 데이터를 적고 전송 버튼을 누른다. </h4>

  ![image](https://user-images.githubusercontent.com/62228401/214496987-cf1b9353-5551-4632-ae91-0340f780b57c.png)

  <h4> 지정한 GET 메소드 동작에 따라 input 태그 안에 들어간 값들이 쿼리스트링으로 서버로 전송된다. </h4>
  
  ![image](https://user-images.githubusercontent.com/62228401/214497099-bf6a8390-02f1-4138-8269-a8b1d1cb6cdd.png)


  <h2> 2.   POST </h2>
  
  - 전달한 데이터 처리 / 생성 요청 메소드 (Create)
  - 요청 데이터 처리, 주로 등록에 사용
  - 메시지 바디(body)를 통해 서버로 요청 데이터 전달하면 서버는 요청 데이터를 처리하여 업데이트
  - 전달된 데이터로 주로 신규 리소스 등록, 프로세스 처리에 사용
  - 만약 데이터를 GET하는데 있어, JSON으로 조회 데이터를 넘겨야 하는 애매한 경우 POST 상ㅇ

  <h3> JSON 데이터 전송 과정 </h3>
  
  <h4> 1. 클라이언트는 body에 등록할 회원 정보를 JSON 형태로 만들어 담고 서버로 전송한다. </h4>
  
  ![image](https://user-images.githubusercontent.com/62228401/214726820-994f9678-0740-40a3-b2bc-30a63c1cd888.png)
  
  <h4> 2. 서버에서는 받은 메시지를 분석해 로직대로 처리한다. 예를 들어, 데이터베이스에 등록하고 신규 아이디를 생성한다. </h4>

 ![image](https://user-images.githubusercontent.com/62228401/214726941-e6f6a365-c782-4ef3-af09-476df528d763.png)

  <h4> 3. 신규회원에 대한 데이터를 바디에 담아서 클라이언트로 응답한다. </h4>
  
    <h5> 1. 신규 자원 생성은 200이나 201로 응답을 보낸다. </h5>
    <h5> 2. Location은 자원이 신규로 생성된 URI 경로를 의미한다. </h5>
  
  ![image](https://user-images.githubusercontent.com/62228401/214727379-2e4df7cd-4746-4a80-8465-9bbbe699933b.png)

  <h3> HTML Form 데이터 전송 과정 </h3>
  
  1. HTML Form 태그 문서로 사용자와 UI로 상호작용하여 서버와 통신
  2. 회원 가입, 상품 주문, 데이터 변경에 이용
  3. HTML Form 전송은 GET, POST만 지원

<h4> 웹문서에서 폼 입력칸에 데이터를 적고 전송 버튼을 누른다 </h4>

![image](https://user-images.githubusercontent.com/62228401/214734548-7f2b0d09-4b1d-49fc-9286-f54538e756cf.png)

<h4> 2. 지정한 POST 메소드 동작에 따라 input 태그 안에 들어가 값들이 쿼리스트링으로 서버로 전송된다. </h4>

![image](https://user-images.githubusercontent.com/62228401/214734248-9ccc44ab-c62c-4f3c-adfa-0c7d2996b065.png)


** info **
<h5> Content-Type 헤더 종류 </h5>

1. Content-Type: application/x-www-form-urlendcoded

  - Form의 내용을 HTTP 메시지 바디를 통해서 전송(key=value, 쿼리 파라미터 형식)
  - 전송 데이터를 url encoding 처리
  - ex) abc김 -> abc%EA%B9%80

2. Content-Type : multipart/form-data

  - 파일 업로드 같은 바이너리 데이터 전송 시 사용
  - 다른 종류의 여러 파일과 Form의 내용 함께 전송 가능. 그래서 이름이 multipart

3. Content-Type : application/json

  - TEXT, XML, JSON 데이터 전송 시 사용

<h3> 파일 데이터 전송 과정 </h3>

1. enctype을 multiparat/form-data로 작성해 해당 폼에 파일이 있다는 것을 표시한다.
2. 바이너리 데이터 전송 시 사용한다.
3. multipart/form-data 형식이라면 HTTP 메시지에 임의의 구분자(------XXX)가 Form 데이터간 구분을 지어준다.
4. 여러 개의 Content-Type에 대한 데이터를 보낼 수 있다.

![image](https://user-images.githubusercontent.com/62228401/214735587-83cc3167-c236-4186-a962-a931a4b2ffdc.png)

<h2> 3. PUT </h3>

- 리소스를 대체(수정)하는 메소드(Update)
- 만일 요청 메시지에 리소스가 잇으면 덮어쓰고, 없으면 생성한다.
  - /members/100 데이터가 존재하면 기본의 것을 완전 대체한다.
  - /members/100 데이터가 없으면 대체할게 없으니까 새로 생성한다.

- 데이터를 대체해야 하니, 클라이언트가 리소스의 구체적인 전체 경로를 지정해 보내주어야 한다.
  - POST/members : 멤버 새로 추가
  - POST/members/100 : 100번째 멤버 수정

<h3> PUT 요청에 리소스가 있는 경우 </h3> 

<h4> 1. 100번 유저의 리소스를 교체하겠다는 요청을 보낸다. </h4>

![image](https://user-images.githubusercontent.com/62228401/214736023-67abbbd2-58a3-494f-b40b-6c9bf680713d.png)

<h4> 2. 기존에 데이터가 있었다면 완전히 대체된다. </h4>

![image](https://user-images.githubusercontent.com/62228401/214736129-e48c81ae-fc8f-4c52-8a75-845446ea534a.png)

<h3> PUT 요청에 리소스가 없는 경우 </h3>

<h4> 1. 100번 유저의 리소스를 교체하겠다는 요청을 보낸다. </h4>

![image](https://user-images.githubusercontent.com/62228401/214736259-179ff94b-d16a-48b4-8d30-dbc519bbe235.png)

<h4> 2. 기존에 데이터가 없다면 POST와 같이 신규로 생성한다. </h4>

![image](https://user-images.githubusercontent.com/62228401/214736370-f9359e7a-740a-4db8-8c65-bf293f7d749d.png)

<h3> PUT 요청에 일부 리소스만 변경하길 원할 경우 </h3>

<h4> 1. age만 50으로 변경하려고 해당 데이터를 PUT을 전달한다. </h4>

  ![image](https://user-images.githubusercontent.com/62228401/214737525-7e3f6531-ea11-43ba-8ff3-f3057a59b8a6.png)

<h4> 2. 하지만 기존 데이터가 완전히 대체되어 이름 데이터가 삭제된다. (이 때는 PATCH 메소드를 사용해야 한다.) </h4>

![image](https://user-images.githubusercontent.com/62228401/214737622-884b0f53-e0d3-47f7-ac14-a67136e9d21d.png)

<h2> 3. PATCH </h2>

- 리소스 일부 부분을 변경하는 메소드(Update)
- 만일 PATCH를 지원하지 않는 서버에서는 대신에 POST를 사용할 수 있다.

<h4> 1. age만 50으로 변경하려고 해당 데이터를 PATCH로 전달한다. </h4>

![image](https://user-images.githubusercontent.com/62228401/214737820-a0aad876-e375-404c-aee2-419308d9b373.png)

<h4> 2. PUT과 다르게 회원 정보에서 age만 변경된다. </h4>

![image](https://user-images.githubusercontent.com/62228401/214737909-bdc0e3cb-bdaa-4408-b9a3-7cbdf1ac2286.png)


<h2> 4. DELETE </h2>

- 리소스를 제거하는 메소드
- 상태코드는 대부분 200을 사용하고 상황에 따라 204 사용

<h4> 100번째 멤버를 제거하기 위해 DELETE로 전달한다. </h4>

![image](https://user-images.githubusercontent.com/62228401/214739852-b236efeb-3d9b-4ff2-936f-8e2431d207d8.png)

<h4> 서버에서 요청을 받고 데이터베이스의 해당 리소스를 제거한다. </h4> 

![image](https://user-images.githubusercontent.com/62228401/214739924-4468733b-e16a-4f0a-9f1b-adc42c76bc22.png)

<h2> HTTP 메소드 - HEAD </h2>

- GET과 동일하지만 서버에서 Body를 Return하지 않음
- Resource를 받지 않고 오직 찾기만 원할 때 사용(응답의 상태코드만 확인할 때)
- 서버의 응답 헤더를 봄으로써 Resource가 수정 되었는지 확인

![image](https://user-images.githubusercontent.com/62228401/214740181-7164ec78-d7e4-4d76-b9ab-8a44c9daa206.png)

<h2> HTTP 메소드 - TRACE </h2>

- 이 메소드도 일종의 검사용
- 클라이언트의 요청 패킷이 방화벽, Proxy 서버, Gateway 등을 거치면서 패킷의 변조가 일어날 수 있는데, 이 때 서버에 도달했을 때의 최종 패킷의 요청 패킷 내용을 응답 받을 수 있다.
- 즉, 요청했던 패킷 내용과 응답 받은 요청 패킷 내용을 비교하여 변조 유무를 확인할 수 있다.
- 요청의 최종 수신자는 반드시 송신자에게 200(OK) 응답 내용(Body)로 수신한 메시지를 반송해야 한다.
- 최초 Client 요청에는 Body가 포함될 수 없다.
  - 리소스 부분 변경(PUT이 전체 변경, PATCH는 일부 변경)

![image](https://user-images.githubusercontent.com/62228401/214741395-8a98a3c6-c986-4019-94c2-10cc24344423.png)

<h2> HTTP 메소드 - OPTION </h2>

- 예비 요청에 사용되는 HTTP  APTHEM
- 예비 요청이란, 본 요청을 하기 전에 안전한지 먼저 검사하는 것이라고 보면 된다.
- 서버의 지원 가능한 HTTP 메소드와 출처를 응답받아 CORS 정책을 검사하기 위한 요청이다.

![image](https://user-images.githubusercontent.com/62228401/214741612-646d488d-42a3-4685-9942-cd7be2519072.png)

<h3> 기타 메소드 간단 내용</h3>

- HEAD
  - GET과 동일하지만, 메시지 부분(body 부분)을 제외하고, 상태 줄과 헤더만 반환
- OPTIONS
  - 대상 리소스에 대한 통신 가능 옵션(메소드)을 설명(주로 CORS에서 사용)
- CONNECT
  - 대상 자원으로 식별되는 서버에 대한 터널을 설정
- TRACE
  - 대상 리소스에 대한 경로를 따라 메소드 
