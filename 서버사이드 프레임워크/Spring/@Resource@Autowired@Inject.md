### @Resource @Autowired @Inject
- 공통점은 의존 주입 이다.

/ |@Resource |@Autowired | @Inject
--------- |--------- |--------- | ---------
설명 |Java 에서 지원하는 어노테이션 |Spring Framework 에서 지원하는 Dependency 정의 용도의 어노테이션 자동주입이며 종속적이다 | Java 에서 지원하는 어노테이션
사용하는 위치 |필드 , 한개의 파라미터인 빈 프로퍼티 setter 메소드 |필드 , 생성자 , 여러개인 파라미터 메소드  | 필드 , 생성자 , 메소드
연결 또는 검색 방식   |이름으로 연결 안되면 타입|타입으로 연결 안되면 이름  | 타입으로 연결 안되면 이름
특이사항 |/ |스프링프레임워크 종속적이다 | /
강제 연결 하기 |@Resource(name="title") |@Qualifier("title") | /


## 참조
https://itjava.tistory.com/54