### 몽고DB란
- NoSQL(Not Only SQL)
- BigData를 위한 솔루션으로 세상에 나옴
- ACID원칙을 사용하지 않고 userfull work를 온전히 사용하면서, 속도를 증가시켰다.
- 대신 BASE원칙을 지킨다.

### BASE
- BAsically available
- Soft state
- Eventually consistent


### 데이터 모델
- DB -Database는 Collection들의 물리적인 컨테이너. 각 Database는 파일시스템에 여러파일들로 저장됩니다.
- Collection (Table) - MongoDB Document의 그룹
- Document (Record)
- Key : Value (Field)

### 특징
- 스키마가 없다.
- 스케일 아웃이 가능하다.
- 조인과 트랜잭션 없음.
- 고성능


### 샤딩(Sharding)
- 데이터를 여러 서버에 분산해서 저장하고 처리할 수 있도록 하는 기술을 말한다.
