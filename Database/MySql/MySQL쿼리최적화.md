## MySQL 쿼리최적화 by toast.NHN

### 조인
- a, b 조인시 a쪽 데이터만 출력해야 하는데 distict 또는 group by가 있다면 `비효율` 발생
- 통계함수가 없는데 group by가 있다면 `비효율` 발생

#### semiJoin
- 서브 쿼리와 메인 쿼리와의 연결 처리를 위한 유사 조인 방식

~~~ sql
SELECT a.prod_cd, a.prod_nm
FROM prod a INNER JOIN ordr_prod b ON a.prod_cd = b.prod_cd
WHERE a.prod_rgst_ymdt < ‘2016-07-01 00:00:00’
GROUP BY a.prod_cd, a.prod_nm ;
~~~
위 쿼리는 세미조인으로 바꿨을때 더 효율적

#### Anti Join
- Semi Join의 부정형

#### Nested Loop Join
- MySQL에서 지원하는 유일한 조인 방식
- 순차적인 처리를 하며, 먼저 처리되는 테이블의 처리 범위에 따라 전체 쿼리의 비용이 결정됨
- 조인에 참여하는 레코드 건 수가 많아질수록 전체적인 응답 속도 저하가 발생
- 조인 연결고리 칼럼에 인덱스 구성이 되어 있지 않은 경우 Lookup 회수만큼 Full Table Scan을 해야 함
- 다량의 Random I/O가 발생
- 주로 좁은 범위 처리에 유리

~~~ sql
select 부서코드, 부서명, 사원번호, 사원명
from 부서 A, 사원 B
where a.부서코드 = b.부서코드
~~~

각각 pk만 존재할때

Q. 위 쿼리에서 드라이빙 테이블은?
A. 사원
- N쪽에서 1쪽으로 드라이빙 순서가 생성된다.

### 조인 순서의 결정
- 기본적으로 MySQL 옵티마이저는 모든 테이블 조인 순서에 대해서 Cost를 계산
- 최소 Cost가 계산된 조인 순서를 기반으로 실행 계획 생성

### 1:N 관계에서의 쿼리패턴 솔루션
- ex) 게시글 목록(댓글 수)
- 반정규화 해서 댓글수를 게시글 테이블에 포함, 반정규화 시켜 게시글만 가지고 온다.



## 인덱스
#### 복합인덱스
- 복합 인덱스 순서도 성능에 영향을 미친다.


### Scalar subquery VS Join
- Join이 가장 빠른 응답속도를 기대할 수 있다
- scalar subquery는 조회건수가 적은 경우 join과 비슷한 성능을 보이나 결과셋이 큰 경우 응답속도 측면에서는 join으로 변
경하는 것이 좋다
- scalar subquery의 경우 outer의 건수만큼 쿼리를 실행시키므로 pasing비용 등의 추가비용이 발생한다
- function은 간단하고 쿼리를 짧게 만들어주어 가독성 측면에서 좋지만 응답속도는 현저히 느리다
- OLTP성 업무에서는 JOIN이나 scalar subquery를 써도 무방하지만 배치작업 등 대용량의 데이터를 처리하는 경우 join으
로 변경하는 것이 필요하다


### GROUP BY ~ ORDER BY NULL
- group by 는 정렬을 수반하므로 정렬이 필요치 않은 경우 order by null 구문을 활용

### GROUP BY를 이용하여 UNIQUE 결과를 찾는 경우 DISTINCT를 사용
- 모두 결과셋은 동일하지만 정렬이 되느냐 안되느냐의 차이를 보임