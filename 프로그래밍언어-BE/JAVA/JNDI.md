### JNDI란(Java Naming and Directory Interface)
- 필요한 자원을 키/값(key/value)쌍으로 저장한 후 필요할때 키를 이용해 값을  얻는 방법이다.

### JNDI 예
- 웹 브라우저에서 name/value 쌍으로 전송한 후 서블릿에서 getParameter(name)로 값을 가져올때
- 해시맵(HashMap) 이나 해시테이블(HashTable)에 키/값으로 저장한 후 키를 이용해 값을 가져올때
- 웹 브라우저에서 도메인네임으로 DNS서버에 요청할 경우 도메인 네임에 대한 IP주소를 가져올때

### JNDI 대표적인 예, 톰캣을 이용한 database 설정
- 웹 어플리케이션에서 ConnectionPool 객체를 구현할 때는 Java SE에서 제공하는 javax.sql.DataSource 클래스를 이용한다.
- 웹 어플리케이션실행시 톰캣이 만들어 놓은 ConnectionPool 객체에 접근 할때는 JNDI를 이용한다.

- 톰캣 컨테이너가 ConnetionPool 객체를 생성하면 이 객체에 대한 JNDI 이름(key)을 미리 설정해 놓는다.
- 그러면 웹 애플리케이션에서 데이터베이스와 연동 작업을 할때 이 JNDI 이름(key)로 접근해서 작업한다.

즉, DB의 정보는 Java code에 직접 하드코딩하면 불편한 점이 많다.(유지보수 어려움) 계정정보와 같은 DB 정보가 바뀐다면 수정하고 재 컴파일하여 서버에 업로드해야 하기 떄문이다
DB 정보를 외부(was)에서 관리하고 Source에서는 외부정보를 가져다쓸 수 있는 이름 값을 사용하면 된다. 이를 위한 방법이 JNDI이다.
 

### 이클립스에서 톰캣 DataSource 설정
- 톰캣 Servers -> context.xml 파일을 보면 <Resource> 태크를 이용해 톰캣 실행 시 연결할 데이터베이스를 설정한다.
- 자바 클래스에서는 name속성의 jdbc/oracle로 DataSource에 접근한다.

### 톰캣의 DataSource  설정 및 사용 방법
![alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FkBloH%2FbtqwVEzjgpy%2FoOMbSrWVB8lBca65tLBXsK%2Fimg.png)