#### spring 컨테이너 역할
1. 스프링은 객체를 관리한다.
    - 객체 생성 : @Component 어노테이션을 포함한 클래스들의 인스턴스를 자동으로 생성한다.
    - @Component의 종류
        1. @Contoller - @RestController
        2. @Service
        3. @Repository
2. 스프링은 의존성을 관리
    - setter 주입
    - 생성자 주입
    - @Autowired
