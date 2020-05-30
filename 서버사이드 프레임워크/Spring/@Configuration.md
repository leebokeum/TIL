### @Configuration
-  @Configuration 어노테이션을 사용함으로써 이 Java 클래스는 Spring의 환경 설정과 관련된 파일이다라고 알려준다.
- org.springframework.context.annoatation 패키지의 @Configuration 어노테이션과 @Bean 어노테이션을 이용해서 스프링 컨테이너에 새로운 Bean 객체를 제공할 수 있다. 

~~~ java
@Configuration
public class BoardConfig {
     
    @Bean(destroyMethod="close")
    public DataSource dataSource(){
        BasicDataSource dataSource = new BasicDataSource();
        dataSource.setDriverClassName("oracle.jdbc.driver.OracleDriver");
        dataSource.setUrl("jdbc:oracle:thin:@localhost:1521:orcl");
        dataSource.setUsername("study");
        dataSource.setPassword("study");
        dataSource.setDefaultAutoCommit(false);
   
        return dataSource;
    }
~~~
- @Bean 어노테이션을 함수 위에 언급함으로써 이 함수는 Spring에서 사용하는 Bean을 리턴해준다는 것을 언급해준다.
- Spring에서는 @Configuration 어노테이션을 사용한 클래스에서  @Bean 어노테이션을 사용한 함수가 리턴하는 객체는 자체적으로 Singleton으로 관리해준다. 