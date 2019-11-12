### JNDI란
- 웹 어플리케이션에서 ConnectionPool 객체를 구현할 때는 Java SE에서 제공하는 javax.sql.DataSource 클래스를 이용한다.
- 웹 어플리케이션실행시 톰캣이 만들어 놓은 ConnectionPool 객체에 접근 할때는 JNDI를 이용한다.

- 톰캣 컨테이너가 ConnetionPool 객체를 생성하면 이 객체에 대한 JNDI 이름(key)을 미리 설정해 놓는다.
- 그러면 웹 애플리케이션에서 데이터베이스와 연동 작업을 할때 이 JNDI 이름(key)로 접근해서 작업한다.

### 이클립스에서 톰캣 DataSource 설정
- 톰캣 Servers -> context.xml 파일을 보면 <Resource> 태크를 이용해 톰캣 실행 시 연결할 데이터베이스를 설정한다.
- 자바 클래스에서는 name속성의 jdbc/oracle로 DataSource에 접근한다.

### 톰캣의 DataSource  설정 및 사용 방법
![alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FkBloH%2FbtqwVEzjgpy%2FoOMbSrWVB8lBca65tLBXsK%2Fimg.png)