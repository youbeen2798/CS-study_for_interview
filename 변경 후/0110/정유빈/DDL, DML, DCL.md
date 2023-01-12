<h1> 데이터 정의어(DDL) </h1>

- 테이블이나 관계의 구조를 생성하는데 사용하며 CREATE, ALTER, DROP문 등이 있음

<h3> CREATE문 </h3>

- 테이블을 구성하고, 속성과 속성에 관한 제약을 정의하며 기본키 및 외래키를 정의하는 명령
- PRIMARY KEY는 기본키를 정할 때 사용하고 FOREIGN KEY는 외래키를 지정할 때 사용하며, ON UPDATE와 ON DELETE는 외래키의 수정과 튜플 삭제 시 동작을 나타냄

<h3> ALTER문 </h3>

- ALTER문은 생성된 테이블의 속성과 속성에 관한 제약을 변겨앟며, 기본키 및 외래키를 변경함
- ADD, DROP은 속성을 추가하거나 제거할 때 사용함
- MODIFY는 속성의 기본 값을 설정하거나 삭제할 때 이용함

<h3> DROP문 </h3>

- DROP문은 테이블을 삭제하는 명령
- 테이블의 구조와 데이터를 모두 삭제하므로 사용에 주의해야 함(데이터만 삭제하려면 DELETE)

<h1> 데이터 조작어(DML) </h1>

- 데이터를 검색, 삽입, 수정, 삭제하는데 사용하며 SELECT, INSERT, DELETE, UPDATE 문 등이 있음
- 여기서 SELECT문은 특별히 Query문(질의어)라고 함

<h3> INSERT문 </h3>

- 테이블에 새로운 튜플을 삽입하는 명령
- 대량 삽입(Bulk Insert)란 한 번에 여러 개의 튜플을 삽입하는 방법

<h3> UPDATE문 </h3>
- 특정 속성 값을 수정하는 명령

<h3> DELETE문 </h3>
- 테이블에 있는 기존 튜플을 삭제하는 명령

<h3> SELECT문 </h3>

SELECT bookname, publisher [속성 이름]
FROM book [테이블 이름]
WHERE price >= 10000; [검색 조건]

<h3> 부속질의(Subquery) </h3>

- 상관 부속질의(Correlated subquery)는 상위 부속질의의 튜플을 이용하여 하위 부속질의를 계산함
- 상위 부속질의와 하위 부속질의가 독립적이지 않고 서로 관련을 맺고 있음

<h3> EXISTS </h3>

- EXISTS는 원래 단어에서 의미하는 것과 같이 조건에 맞는 튜플이 존재하면 결과에 포함시킴
- 즉 부속질의문의 어떤 행이 조건에 만족하면 참임
- 반면 NOT EXISTS는 부속질의문의 모든 행이 조건에 만족하지 않을 때만 참임

<h1> 데이터 제어어(DCL) </h1>

- 데이터의 사용 권한을 관리하는데 사용하며 GRANT, REVOKE문 등이 있음
