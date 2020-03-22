### DBCP(Data Base Connection Poo)
- DBCP는 JDBC(Java Data Base Connectivity) 의 약점을 보완한 방식으로 DastaSource & JNDI를 이용한다.
- DB와 연결하여 작동하는 app는 매번 구동시 연결하여 시간 및 부하가 걸린다. 이를 극복하기 위해 매번 접속하지 않고 하는 방법이  DBCP이다. 

### 설정할 수 있는 옵션
- maxActive : 동시에 사용할 수 있는 최대 커넥션 개수
- maxIdle : Connection Pool에 반납할 때 최대로 유지될 수 있는 커넥션 개수
- minIdle : 최소한으로 유지할 커넥션 개수
- initialSize : 최소로 getConnection() Method를 통해 커넥션 풀에 채워 넣을 커넥션 개수 