## Memcached의 특징에 대해 알아보자

- 여러 코어 또는 멀티 스레드까지 처리 가능함


- 상대적으로 작고 정적인 데이터를 캐싱하는 경우 사용

- 메모리 관리가 Redis만큼 정교하지는 않지만, 메타 데이터에 대한 메모리 리소스를 적게 소비하여 간단한 사용에 적합

- 데이터 타입으로 String만 저장

- 데이터 저장을 메모리에만 함

- 확장성을 Scale-out을 통해 얻을 수 있음

- LRU 알고리즘만으로 메모리 자원을 관리


| 항목 | Memcached | Redis |
|데이터분할|O|O|
|Multi Thread / Single Thread|Multi Thread|Single Thread|
|데이터 저장(persistence / snapshot) | X | O |
|데이터 복제(replication)|X|O|
|트랜잭션 지원|X|O|
|Publisher|X|O|

- Memcached와 Redis는 모두 Key-Value 모델에 기반을 둔 NoSQL 솔루션으로, 두 솔루션 모두 캐시 레이어로서 동작

- Memcached의 대부분의 기능은 Redis로 커버 가능

- 단순한 동작 방식으로 인해, Memcached는 In-Memory Key-Value 저장소라 한다면, Redis는 단순한 Key-Value 저장소를 넘어<br />
  일종의 데이터 구조 스토어라 할 수 있음
