### spring boot에서 로깅 설정
- 의존성 주입
~~~ xml
<dependency>
    <groupId>com.integralblue</groupId>
    <artifactId>log4jdbc-spring-boot-starter</artifactId>
    <version>2.0.0</version>
</dependency>
~~~

- properties에 설정
~~~ properties
logging.level.jdbc.sqlonly=debug
logging.level.jdbc.resultset=off
~~~

[설명]
- jdbc.sqlonly : SQL문만 로그, PreparedStatement일 경우 관련된 argument 값으로 대체된 SQL문
- jdbc.sqltiming : SQL문과 해당 SQL을 실행시키는데 수행된 시간 정보(milliseconds)
- jdbc.audit : ResultSet 제외한 모든 JDBC 호출 정보. 많은 양의 로그가 생성
- jdbc.resultset : ResultSet 포함 모든 JDBC 호출 정보 로그, 방대한 양의 로그 생성
- jdbc.resultsettable : SQL 결과 조회된 데이터의 table을 로그