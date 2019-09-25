## MySQL 쿼리최적화 by toast.NHN

### 조인
- a, b 조인시 a쪽 데이터만 출력해야 하는데 distict 또는 group by가 있다면 `비효율` 발생
- 통계함수가 없는데 group by가 있다면 `비효율` 발생

#### semiJoin
- 서브 쿼리와 메인 쿼리와의 연결 처리를 위한 유사 조인 방식

#### Anti Join
- Semi Join의 부정형

#### Nested Loop Join
- MySQL에서 지원하는 유일한 조인 방식
- 순차적인 처리를 하며, 먼저 처리되는 테이블의 처리 범위에 따라 전체 쿼리의 비용이 결정됨
- 조인에 참여하는 레코드 건 수가 많아질수록 전체적인 응답 속도 저하가 발생
- 조인 연결고리 칼럼에 인덱스 구성이 되어 있지 않은 경우 Lookup 회수만큼 Full Table Scan을 해야 함
- 다량의 Random I/O가 발생
- 주로 좁은 범위 처리에 유리