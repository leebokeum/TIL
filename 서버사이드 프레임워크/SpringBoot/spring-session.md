### spring-session-core
- Spring Session provides an API and implementations for managing a user’s session information.

### spring-session-jdbc
- 서버가 실행되면 자동으로 세션을 관리하는 database 테이블이 생성된다.
- default로 SPRING_SESSION, SPRING_SESSION_ATTRIBUTES 두개의 테이블이 생성된다.
- jdbc는 Redis나 MongoDB와는 달리 세션이 만료될 경우 데이터베이스에서 자체적으로 삭제되지 않고 Spring 서버에서 로직을 통해 삭제되게 되어있다.

### spring-session-redis

## 참조
https://gofnrk.tistory.com/42
https://gofnrk.tistory.com/45