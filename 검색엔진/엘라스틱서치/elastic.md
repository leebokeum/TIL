### 엘라스틱서치(Elasticsearch)란 무엇인가?
- 엘라스틱서치는 엘라스틱(Elastic) 社가 아파치 루씬(Apache Lucene)을 기반으로 개발·공급하는 오픈소스 검색엔진 솔루션
- 엘라스틱서치는 루씬의 기능을 대부분 지원하면서 대용량 데이터 처리가 가능하고 설치와 구성이 용이
-  방대한 양의 데이터를 신속하게, 거의 실시간( NRT, Near Real Time )으로 저장, 검색, 분석할 수 있다.

### ELK( Elasticsearch / Logstatsh / Kibana )스택
- Logstash
    - 다양한 소스( DB, csv파일 등 )의 로그 또는 트랜잭션 데이터를 수집, 집계, 파싱하여 Elasticsearch로 전달
- Elasticsearch
    - Logstash로부터 받은 데이터를 검색 및 집계를 하여 필요한 관심 있는 정보를 획득
- Kibana
    - Elasticsearch의 빠른 검색을 통해 데이터를 시각화 및 모니터링

### Search
- 엘라스틱서치에서는 단일 데이터 단위를 도큐먼트(Document)라고 하며 이 도큐먼트를 모아놓은 집합을 인덱스(Index)로 칭한다.
- 엘라스틱서치는 데이터가 유입될 때 인덱싱(indexing)이라는 프로세스를 진행하여 검색 및 통계를 위한 도큐먼트를 확보한다.


### 키바나
- 축적된 데이터를 기반으로 인사이트와 스토리텔링을 할 수 있게 도와주는 시각화를 담당
- 바나는 엘라스틱서치의 데이터 시각화를 위한 사용자 인터페이스(User Interface, UI) 도구로 출발하여 시스템 관리자 기능까지 확대 적용되면서 엘라스틱 스택의 중요한 축이 되고 있다.


### Elasticsearch와 관계형 DB 비교
![alt text](/image/검색엔진/엘라스틱서치1.jpg)
![alt text](/image/검색엔진/엘라스틱서치2.jpg)