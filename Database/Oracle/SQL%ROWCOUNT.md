### PL/SQL에는 묵시적 커서(Implicit Cursor)
- PL/SQL에는 묵시적 커서(Implicit Cursor)가 있다.
그것에는 SQL%FOUND, SQL%ISOPEN, SQL%NOTFOUND 그리고, SQL%ROWCOUNT 가 있다.
 
### SQL%ROWCOUNT
- SQL%ROWCOUNT 는 INSERT, UPDATE, DELETE 문장에 대해서 영향을 받은 행의 갯수를 보여준다.

### 그외
- SQL%ROWCOUNT : 가장 최근에 수행된 SQL문에 의해 영향을 받은 행의 갯수(정수 값)
- SQL%FOUND : 가장 최근에 수행된 SQL문에 의해 영향을 받은 행의 갯수가 한 개 이상이면 TRUE가 되는 BOOLEAN 속성
- SQL%NOTFOUND : 가장 최근에 수행된 SQL 문에 의해 영향을 받은 행이 없으면 TRUE가 되는 BOOLEAN 속성
- SQL%ISOPEN : PL/SQL은 실행 후 바로 묵시적 커서(IMPLICIT CURSOR)를 닫기 때문에 항상 FALSE로 평가