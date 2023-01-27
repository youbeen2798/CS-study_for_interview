서버와 클라이언트가 소통을 하기 위해서는 보통 Http를 이용한다. </br>

### REST (Representational State Transfer)
- 자원(Resource): URI
- 행위(Verb): HTTP Method
- 표현(Representations)


REST를 지키면서 행위를 전달하는 방법 -> HTTP Method</br>


# HTTP Method란?
- 클라이언트와 서버 사이에 이루어지는 요청(Request)과 응답(Response) 데이터를 전송하는 방식이다. </br>
즉, 서버가 수행해야 할 동작을 지정하는 요청을 보내는 방법이다. </br>

## 주요 메서드
HTTP 메서드의 종류는 총 9가지이며, 주로 5개의 메서드 "GET", "POST", "PUT", "PATCH", "DELETE" 가 사용된다.

### GET
- 리소스를 조회한다. (READ)
- 이미지나 정적 텍스트 문서 조회는 쿼리 파라미터 없이 리소스 경로로 단순하게 조회 가능
- 동적으로 서버에 전달하고 싶은 데이터는 쿼리스트링을 통해 전달한다. => GET /members/100? username=sumin
- 쿼리 스트링 이외도 메시지 바디를 사용해서 데이터 전달 가능하지만, 서버에서 따로 구성해야 되기 때문에 지원하지 않는 곳이 많아서 지양한다.
- 조회할 때 POST도 사용할 수 있지만, GET 메서드는 캐싱이 가능하기에 GET을 사용하는 것이 유리하다.


### POST
- 전달한 데이터 처리/생성 요청 메서드이다. (CREATE)
- 메시지 바디(body)를 통해 서버로 요청 데이터 전달하면 서버는 요청 데이터를 처리하여 업데이트를 한다.
- 전달된 데이터로 주로  신규 리소스 등록, 프로세스 처리에 사용된다.
- 데이터를 GET하는데 JSON으로 조회 데이터를 넘겨야할 경우 POST를 사용한다.

 
### PUT
- 리소스를 수정하는 메서드이다. (UPDATE)
- 요청 메시지에 리소스가 있으면 덮어쓰고, 없으면 새로 생성한다.</br>
ex) /member/100 데이터가 존재하면 기존에 것을 완전 대체 한다. </br>
ex) /member/100 데이터가 없으면 대체 할것이 없어 새로 생성한다.
- 데이터를 대체해야하니, 클라이언트가 리소스의 구체적인 전체 경로를 지정해 보내주어야한다. </br>
ex) POST / members : 맴버 새로 추가 </br>
ex) PUT / members/100: 100번째 멤버 수정 </br>
![image](https://user-images.githubusercontent.com/58407737/215031329-127de2e6-d4e6-42f5-bb3b-db59bb351146.png)
![image](https://user-images.githubusercontent.com/58407737/215031387-c3416ffc-4cdc-4199-8299-5a835e040683.png)




### PATCH
- 리소스 일부 부분을 변경하는 메소드(UPDATE)
- 만일 PATCH를 지원핮지 않는 서버에서는 PATCH 대신에 POST를 사용할 수 있다.


### DELETE
- 리소스 제거하는 메소드(DELETE)
- 상태코드는 대부분 200을 사용하고 상황에 따라 204를 사용한다.

## 그 외 메서드
### HEAD
- GET과 동일하지만 메시지 부분인 Body부분을 제외하고, 상태 줄과 헤더만 반환한다. (바디 return XX)

### OPTIONS
- 예비 요청(본 요청을 하기 전에 안전한지 미리 검사)에 사용된다.
- 서버의 지원 가능한 HTTP 메서드와 출처를 응답 받아 CORS정책을 검사하기 위한 요청이다. (주로 CORS에서 사용)

### CONNECT
- 대상 자원으로 식별되는 서버에 대한 터널을 설정한다.


### TRACE
- 대상 리소스에 대한 경로를 따라 메시지 루프백 테스를 수행한다. 

</br>
</br>
</br>
</br>

https://inpa.tistory.com/entry/WEB-%F0%9F%8C%90-HTTP-%EB%A9%94%EC%84%9C%EB%93%9C-%EC%A2%85%EB%A5%98-%ED%86%B5%EC%8B%A0-%EA%B3%BC%EC%A0%95-%F0%9F%92%AF-%EC%B4%9D%EC%A0%95%EB%A6%AC


