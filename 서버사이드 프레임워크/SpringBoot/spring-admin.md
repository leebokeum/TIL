### spring admin
- Spring Boot Admin은 Spring Boot에서 제공하는 Actuator endpoints를 이용해서 모니터링 할 수 있게 UI를 제공해주는 프로젝트이다. Spring Boot Admin을 사용 하기 위해서는 서버를 설정 해야된다.
- Spring Boot Admin / Spring Boot Client

- 의존성
``` gradle
    implementation 'de.codecentric:spring-boot-admin-starter-client'
    implementation 'de.codecentric:spring-boot-admin-starter-server'
```

- @EnableAdminServer 추가
``` java
@SpringBootApplication
@EnableAdminServer
public class AdminmonitorApplication {

    public static void main(String[] args) {
        SpringApplication.run(AdminmonitorApplication.class, args);
    }

}
```

### Logfile Viewer
- Spring Boot Admin로그 파일은 End Point 에서 자동으로 접근 할 수 없다. 그래서 Spring Boot에 있는 로그 파일을 Actuator endpoints에 설정을 해줘야된다.
- log 파일을 생성 하기 위해서 /src/main/resource/logback-spring.xml을 생성

## 참조
https://jaehyun8719.github.io/2019/06/20/springboot/admin/