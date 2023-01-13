# SQL문법 종류

## DDL (Data Definition Language): 데이터 정의 언어
-> 테이블과 컬럼을 정의하는 명령어로 생성, 수정, 삭제 등의 데이터 전체 골격을 결정하는 역할을 담당한다.
</br>
### 특징 
명령어를 입력하는 순간 작업이 **즉시 반영(Auto Commit)** 된다.

### 종류
![image](https://user-images.githubusercontent.com/58407737/212258511-459c1ef2-39ba-4f02-81e5-673fdba863d9.png)
</br>
</br>

## DML (Data Manipulation Language): 데이터 조작 언어
-> 데이터베이스의 내부 데이터를 관리하기 위한 언어이다. 데이터를 조회, 추가, 변경, 삭제 등의 작업을 수행하기 위해 사용된다.

### 특징 
DDL과 달리 DML은 **즉시 반영**이 되지 않는다. 즉, DML에 의한 데이터 변동은 영구적인 변경이 아니기 때문에 ROLLBACK으로 다시 되돌릴 수 있다. </br>
또한, DML은 Target 테이블을 메모리 버퍼 위에 올려두고 변경을 수행하기 때문에, 실시간으로 테이블에 반영되지 않는다. </br>
commit을 통해 Transaction을 종료해야 해당 변경 사항이 테이블에 반영된다. </br>

### 종류
![image](https://user-images.githubusercontent.com/58407737/212259166-0126c38d-4766-4d3d-8032-5c7e07b8538d.png)
</br>
</br>

## DCL (Data Control Language): 데이터 제어 언어
-> 데이터를 관리 목적으로 보안, 무결성, 회복, 병행 제어 등을 정의하는데 사용한다. </br>
DCL을 사용하면 데이터베이스에 접근하여 읽거나 쓰는 것을 제한할 수 있는 권한을 부여하거나 박탈할 수 있고 트랜잭션을 명시하거나 조작할 수 있다. </br>

### 특징
불법적인 사용자로부터 데이터를 보호하기 위한 데이터 보안의 역할을 수행하며, 데이터의 정확성을 위한 무결성을 유지하기도 한다.</br> 
마지막으로 시스템 장애에 대비한 회복과 병행수행을 제어한다. </br>

### 종류
![image](https://user-images.githubusercontent.com/58407737/212259638-aeb640bb-fa01-4b6c-8ac2-4fa9372570bb.png)
