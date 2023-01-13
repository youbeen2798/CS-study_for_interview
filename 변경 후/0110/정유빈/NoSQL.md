<h1> NoSQL </h1>

- Not Only SQL의 약자


<h3> RDBMS </h3>

- RDBMS의 저장 방식은 SQL에 의해 저장되며 정해진 스키마에 따라 데이터를 저장하여야 한다.
- RDBMS의 R은 Relational의 약자로 RDBMS는 관계형 데이터베이스 관리 시스템을 의미합니다.
- RDBMS는 RDB를 관리하는 시스템이며, RDB는 관계형 데이터 모델을 기초로 두고 모든 데이터를 2차원 테이블 형태로 표현하는 데이터베이스이다.
- RDBMS는 아래와 같이 구성된 테이블이 다른 테이블들과 관계를 맺고 모여있는 집합체로 이해할 수 있다. 

<h1> NoSQL </h1>

- RDB 형태의 관계형 데이터베이스가 아닌 다른 형태의 데이터 저장 기술을 의미함
- RDBMS와 달리 테이블 간 관계를 정의하지 않음
- 데이터 테이블은 그냥 하나의 테이블이며 테이블 간의 관계를 정의하지 않아 일반적으로 테이블 간 Join도 불가능함
- NoSQL은 점점 빅데이터의 등장으로 인해 데이터와 트래픽이 기하급수적으로 증가함에 따라 등장하였음
- RDBMS의 단점이 성능을 향상시키기 위해서는 장비가 좋아야 하는 Scale-Up의 특징이 비용을 기하급수적으로 증가시키기 때문에 데이터 일관성은 포기하되 비용을 고려하여 여러 대의 데이터에 분산하여 저장하는 Scale-Out을 목표로 등장하였음
- NoSQL을 하면 가장 유명한 Document 기반의 MongoDB를 많이 떠올리지만, MongoDB는 NoSQL의 한 종류로 NoSQL은 다양한 형태의 저장 기술을 지원하고 있음
- 다양한 형태의 저장 기술은 RDBS 스키마에 맞추어 데이터를 관리해야 된다는 한계를 극복하고 수평적 확장성(Scale-Out)을 쉽게 할 수 있다는 장점을 가지고 있음
- 크게 4가지 유형이 존재함

<h3> 1. Key-Value Database </h3>

- 아래와 같이 데이터가 Key와 Value의 쌍으로 저장됨

![image](https://user-images.githubusercontent.com/62228401/212219788-6263a99f-987a-4805-850d-a60fcf47d59d.png)
- kEY-VALUE 하나의 묶음(Unique) 로 저장되는 기술로 단순한 구조이기에 속도가 빠르며 분산 저장 시 용이하다.
- Key는 VALUE에 접근하기 위한 용도로 사용되며, 값은 어떤 형태의 데이터라도 담을 수 있음(심지어 오디오와 비디오도 가능함)
- 간단한 API를 제공하는 만큼 질의의 속도가 굉장히 빠른 편임
- 예시로, Redis, Riak, Amazon Dynamo DB 등이 있음

<h3> 2. Document Database </h3>

- Key와 Document 형태로 저장됨
- Key-Value 모델과 다른 점은 Value가 계층적인 형태의 도큐먼트로 저장된다는 것임
- 객체 지향에서의 객체와 유사하며, 이들은 하나의 단위로 취급되어 저장된다. (즉, 하나의 객체를 여러 개의 테이블에 나누어 저장할 필요가 없음)
- 주요한 특징으로 객체와 관계 매핑이 필요하지 않다. 객체를 Document 형태로 바로 저장이 가능하기 때문이다.
- 또한 검색에 최적화되어 있는데, 이는 Key-Value 모델의 특징과 동일함
- 단점은 사용이 번거롭고, 쿼리가 SQL과는 다르다는 점이다.
- 도큐먼트 모델에서는 질의의 결과가 JSON이나 xml 형태로 출력되기 때문에 그 사용 방법이 RDBMS의 질의 결과를 사용하는 방법과 다르다.
- 트리형 구조로 레코드를 저장하거나 검색하는데 효과적이다. ( 그러나 Scan에는 용이하지 않음)
![image](https://user-images.githubusercontent.com/62228401/212220138-d3448417-5fc3-4923-bee0-d7c3bbc6c3a0.png)
- 대표적인 NoSQL Document Model로는 MongoDB, CouthDB가 있음

<h3> 3. Wide Column Database </h3>

- 아래 그림은 Column Familes를 포함하는 Key Space
![image](https://user-images.githubusercontent.com/62228401/212222655-17d63698-258f-4f91-85fe-85589659fa9d.png)

- 아래는 3행을 포함하는 COLUMN FAMILES. 행마다 각각의 컬럼을 가진다.
![image](https://user-images.githubusercontent.com/62228401/212219526-5cf0fdcb-1045-40df-abeb-9e63f7418cd1.png)
- 행마다 키와 해당 값을 저장할 때마다 각각 다른 값의 다른 수의 스키마를 가질 수 있다.
- 대량의 데이터의 압축, 분산처리, 집계 쿼리(SUM, COUNT, AVG) 등 쿼리 동작 속도와 확장성이 뛰어난 것이 대표적 특징이다.

<h3> 4. GRAPH DATABASE </h3>
![image](https://user-images.githubusercontent.com/62228401/212220262-df2cf812-5c31-40b1-ab26-b3586b59db59.png)
- 데이터를 노드로 표현하며, 노드 사이의 관계를 엣지로 표현
- RDBMS보다 Performance가 좋고 유연하며 유지보수에 용이한 것이 특징
