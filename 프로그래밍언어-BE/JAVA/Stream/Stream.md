### Stream이란
- JDK 8에서 추가된 API
- 파일 I/O에서 사용되는 스트림과는 다르다.
- 데이터소스를 추상화하고, 데이터를 다루는데 자주 사용되는 메서들을 정의해 놓았다.

- 생성하기
  - 배열 / 컬렉션 / 빈 스트림
  - Stream.builder() / Stream.generate() / Stream.iterate()
  - 기본 타입형 / String / 파일 스트림
  - 병렬 스트림 / 스트림 연결하기
- 가공하기
  - Filtering
  - Mapping
  - Sorting
  - Iterating
- 결과 만들기
  - Calculating
  - Reduction
  - Collecting
  - Matching
  - Iterating

### 전체 -> 맵핑 -> 필터링 1 -> 필터링 2 -> 결과 만들기 -> 결과물


### 특징
- 스트림은 데이터 소스를 변경하지 않는다.
- 