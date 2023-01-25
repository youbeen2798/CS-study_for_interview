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

  <h2> POST </h2>
  
  - 전달한 데이터 처리 / 생성 요청 메소드 (Create)
  - 요청 데이터 처리, 주로 등록에 사용
- PUT
  - 리소스를 대체(덮어쓰기), 해당 리소스가 없으면 생서 
- PATCH
  - 리소스 부분 변경(PUT이 전체 변경, PATCH는 일부 변경)
- DELETE
  - 리소스 삭제

<h3> 기타 메소드 </h3>

- HEAD
  - GET과 동일하지만, 메시지 부분(body 부분)을 제외하고, 상태 줄과 헤더만 반환
- OPTIONS
  - 대상 리소스에 대한 통신 가능 옵션(메소드)을 설명(주로 CORS에서 사용)
- CONNECT
  - 대상 자원으로 식별되는 서버에 대한 터널을 설정
- TRACE
  - 대상 리소스에 대한 경로를 따라 메소드 
