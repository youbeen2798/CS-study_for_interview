## Index 들어가기 전
index는 DB 데이터 조회 성능 향상을 위해 사용된다.  </br>

대욜량 데이터를 담고 있는 DB 테이블에서 우리에게 필요한 데이터를 빨리 찾으려면 'Index' 도움이 필요하다. </br>

## DB 성능과 관련된 사항들
### 1. 프로세서
컴파일(실행계획 생성) </br>
연산 (SORT, JOIN, DATA, CONVERSION)
LOCK 관리 등이 존재한다.

### 2. LOCK
Row, Table, Library Cache LOCK 등이 존재한다.

### 3. Network I/O
Application Server와 DB Server들 간의 요청 혹은 결과 데이터 전송을 뜻한다. </br></br>

이러한 데이터 전송 간의 네트워크 시간이 꽤 오래 걸리기 때문에 해단 시간을 최소한으로 해야한하는데 </br>
해결책은 원하는 데이터를 한방에 가져오는 '한방 쿼리' 를 짜는 것이다. 

### 4. 데이터 I/O
**데이터가 입력되고 나감 -> DB 인덱스 개념이 여기에 속한다.**

</br>
</br>

# Index 란?
![image](https://user-images.githubusercontent.com/58407737/213962398-0c359bb3-6cfa-4342-b629-ed7918ab89ec.png)

DB 내 저장된 데이터의 '주소'를 갖고 있는 것이다. </br>

테이블 내의 1개의 컬럼, 혹은 여러 개의 컬럼을 Key로 삼고, Key에 해당하는 OID(레코드의 물리적 주소 값)가 저장되어 있다. </br>

테이블의 다른 세부 항목들은 갖고 있지 않아 보통의 테이블을 저장하는 데 **필요한 디스크 공간보다 작은 디스크 공간을 필요**로 한다.

책에 비유하자면 일종의 "찾아보기" 페이지
-> 책 뒤에서 그 내용을 알고 싶으면 몇 페이지로 가라'라고 지름길을 안내해주는 것으로, 흔히 찾아보기라고 되어 있는 부분이 색인이다.  </br>

</br>
</br>

## 장점 
1. DB 데이터의 주소를 갖고 있어서 원하는 데이터를 빠르게 찾을 수 있다는 것이다. </br>
-> 전반적인 시스템의 부하를 줄일 수 있기도 하지만, 데이터 조회가 빠르다는 것이 핵심이다. </br>

</br>

## 단점
### 1. 타 성능 악영향
SELECT를 제외한 모든 동작 INSERT / UPDATE / DELETE 성능에 영향을 미친다. </br>

위 세 동작은 데이터를 삽입하고 수정하고 삭제하는 행위를 하는데, 이러한 행위들로 인해 인덱스를 걸어둔 컬럼의 데이터가 바뀌면 인덱스 테이블의 수정도 필요하여 삽입 / 수정 / 삭제 작업이 두 번 이루어지게 된다. </br>

</br>
</br>

### 2. 추가 저장 공간 필요
DB에 저장된 데이터의 주소를 인덱스의 Key값으로 가지려면 별도의 공간에 저장하므로 추가 저장 공간이 필요하다. </br>

인덱스를 사용하는 시스템을 설계할 때, 인덱스 영역을 전체 테이블 영역의 30 ~ 50%까지 잡아 놓을 만큼 저장 공간이 꽤나 많이 필요하다. </br>


### 3. 공수 필요
인덱스를 생성하고 주기적으로 관리할 인력과 시간이 필요하다. 

</br>
</br>

## RDBMS에서 인덱스는 필수이다.
- 일반적인 OLTP(Online Transaction Procession, 온라인 트랜잭션 처리) 시스템에서 데이터 조회 업무가 90% 이상이기 때문이다.
- 조회 업무의 검색 속도 향상은 시스템 부하를 감소시켜, 같은 시간 내에 더 많은 업무 처리가 가능해진다.

</br>

- 규모가 작지 않은 테이블에서
- INSERT / UPDATE / DELETE가 자주 발생하지 않은 컬럼에서
- JOIN / WHERE / ORDER BY 에 자주 사용되는 컬럼에서
- 데이터의 중복도가 낮은 컴럼 등에서 인덱스를 사용하면 좋다.

</br>

백엔드 성능을 높이려고 실행하는 SQL 튜닝은 SQL이 인덱스를 활용하도록 SQL을 수정하는 것이라고 할 수 있다.
