<h1> 데이터 정의어(DDL) </h1>

- 테이블이나 관계의 구조를 생성하는데 사용하며 CREATE, ALTER, DROP문 등이 있음

<h3> CREATE문 </h3>

- 테이블을 구성하고, 속성과 속성에 관한 제약을 정의하며 기본키 및 외래키를 정의하는 명령
- PRIMARY KEY는 기본키를 정할 때 사용하고 FOREIGN KEY는 외래키를 지정할 때 사용하며, ON UPDATE와 ON DELETE는 외래키의 수정과 튜플 삭제 시 동작을 나타냄

![image](https://user-images.githubusercontent.com/62228401/212206014-30424754-096e-4b94-9889-6dc824ab5147.png)

<h3> ALTER문 </h3>

- ALTER문은 생성된 테이블의 속성과 속성에 관한 제약을 변겨앟며, 기본키 및 외래키를 변경함
- ADD, DROP은 속성을 추가하거나 제거할 때 사용함
- MODIFY는 속성의 기본 값을 설정하거나 삭제할 때 이용함

![image](https://user-images.githubusercontent.com/62228401/212206047-e1fe25b2-5d02-487b-8d0b-8f29da813418.png)


<h3> DROP문 </h3>

- DROP문은 테이블을 삭제하는 명령
- 테이블의 구조와 데이터를 모두 삭제하므로 사용에 주의해야 함(데이터만 삭제하려면 DELETE)

![image](https://user-images.githubusercontent.com/62228401/212206086-c537c321-5814-4504-8191-2706f8274275.png)

<h1> 데이터 조작어(DML) </h1>

- 데이터를 검색, 삽입, 수정, 삭제하는데 사용하며 SELECT, INSERT, DELETE, UPDATE 문 등이 있음
- 여기서 SELECT문은 특별히 Query문(질의어)라고 함


<h3> INSERT문 </h3>

- 테이블에 새로운 튜플을 삽입하는 명령
- 대량 삽입(Bulk Insert)란 한 번에 여러 개의 튜플을 삽입하는 방법

![image](https://user-images.githubusercontent.com/62228401/212206340-92d9ff26-19c4-45ba-8bf3-8e6016b9de35.png)

<h3> UPDATE문 </h3>
- 특정 속성 값을 수정하는 명령

![image](https://user-images.githubusercontent.com/62228401/212206309-43e75896-6e1f-4b3f-8ceb-abe8fc370203.png)

<h3> DELETE문 </h3>
- 테이블에 있는 기존 튜플을 삭제하는 명령

![image](https://user-images.githubusercontent.com/62228401/212206365-9bbdcf74-0960-4ec0-8523-f1fb5846461f.png)

<h3> SELECT문 </h3>

SELECT bookname, publisher [속성 이름]
FROM book [테이블 이름]
WHERE price >= 10000; [검색 조건]

- WHERE절에 조건으로 사용할 수 있는 술어는 다양하며 아래의 표에서 필요에 따라 참고하면 된다.

![image](https://user-images.githubusercontent.com/62228401/212206646-11d9a8ca-116c-4410-804e-5aef23288f6a.png)

- 집계 함수 종류

![image](https://user-images.githubusercontent.com/62228401/212206718-85602417-48c3-4464-81de-6eaf93eaca89.png)

- Join 연산

![image](https://user-images.githubusercontent.com/62228401/212206775-eff4aeb6-4c16-4a5c-a2ac-67c9691ad09b.png)

<h3> 부속질의(Subquery) </h3>

- 상관 부속질의(Correlated subquery)는 상위 부속질의의 튜플을 이용하여 하위 부속질의를 계산함
- 상위 부속질의와 하위 부속질의가 독립적이지 않고 서로 관련을 맺고 있음

![image](https://user-images.githubusercontent.com/62228401/212206811-fb7be195-f3f2-467c-98c9-1f90499bebf8.png)

<h3> EXISTS </h3>

- EXISTS는 원래 단어에서 의미하는 것과 같이 조건에 맞는 튜플이 존재하면 결과에 포함시킴
- 즉 부속질의문의 어떤 행이 조건에 만족하면 참임
- 반면 NOT EXISTS는 부속질의문의 모든 행이 조건에 만족하지 않을 때만 참임

![image](https://user-images.githubusercontent.com/62228401/212206837-bf5f8cb8-c317-4bd1-9cc6-da1539c8e819.png)

<h1> 데이터 제어어(DCL) </h1>

- 데이터의 사용 권한을 관리하는데 사용하며 GRANT, REVOKE문 등이 있음
