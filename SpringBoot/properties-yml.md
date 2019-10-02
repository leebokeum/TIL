### application properties란?
- Srping boot enviroment  외부 설정 속성 정의
- properties의 값은 @Value 어노테이션을 통해 읽어올 수 있다.

#### 간단한 사용법

~~~ properties
# application.properties
name=Michael
~~~

~~~ java
@Component
public class MyBean {

    @Value("${name}")
    private String name;

    // ...

}
~~~

- 위의 MyBean 클래스의 name 멤버변수는 @Value 어노테이션을 지정한 것만으로 application.properties에 있는 name속성 값 "Michael"로 초기화가 된다.

- 만약에 application.properties 파일에 name 속성이 정의되어있지 않았을 때 default값을 지정하는 방법도 있다. 아래와 같이 @Value 어노테이션에서 속성 이름 옆에 콜론(:)을 찍고 직접 지정해 주면 된다.

~~~ java
    @Value("${name:Michael}")
    private String name;

    @Value("${age:20}")
    private int age;
~~~

### 프로퍼티 우선 순위
- 스프링 부트에서는 프로퍼티값에 대해 우선 순위를 두고 있으며 우선 순위는 다음과 같다.
1. 유저 홈 디렉토리에 있는 spring-boot-dev-tools.properties
2. 테스트에 있는 @TestPropertySource
3. @SpringBootTest 애노테이션의 properties 애트리뷰트
4. 커맨드 라인 아규먼트
5. SPRING_APPLICATION_JSON (환경 변수 또는 시스템 프로티) 에 들어있는 프로퍼티
6. ServletConfig 파라미터
7. ServletContext 파라미터
8. java:comp/env JNDI 애트리뷰트
9. System.getProperties() 자바 시스템 프로퍼티
10. OS 환경 변수
11. RandomValuePropertySource
12. JAR 밖에 있는 특정 프로파일용 application properties
13. JAR 안에 있는 특정 프로파일용 application properties
14. JAR 밖에 있는 application properties
15. JAR 안에 있는 application properties
16. @PropertySource
17. 기본 프로퍼티 (SpringApplication.setDefaultProperties)


### application.properties 파일 위치에 따른 우선 순위
1. 현재 위치에서 /config 디렉토리
2. 현재 위치
3. classpath 내의 /config 패키지
4. classpath 내의 루트


### application.properties 내의 값은 이전의 정의된 값을 참조할 수 있다.
~~~ properties
app.name=MyApp
app.description=${app.name} is a Spring Boot application
~~~


#### 참조
https://supawer0728.github.io/2018/03/11/Spring-Property/