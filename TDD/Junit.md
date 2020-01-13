### Junit
- Java의 대표적인 Testing Framework가 JUnit이다.

### JUnit assert관련 Method
Method | 내용
--------- | ---------
assertArrayEquals(a,b)	| 배열 a와b가 일치함을 확인한다.
assertEquals(a,b)|객체 a와b의 값이 같은지 확인한다.
assertSame(a,b)|객체 a와b가 같은 객체임을 확인한다.
assertTrue(a)|a가 참인지 확인한다.
assertFalse(a)|a가 거짓인기 확인한다.
assertNotNull(a)|a객체가 Null이 아님을 확인한다.

### JUnit Function Flow
- setUp() : 테스트 대상 클래스의 실행전에 가장 먼저 setUP()을 실행한다.
ex) 네트워크 연결, DB 연결에 활용한다.
- tearDown() : 가장 마지막에 수행되며 setUp()의 반대 개념으로 생각하면 된다.
ex) 네트워크 연결 종료, DB 연결을 종료하는데 활용한다.
- setUp()과 tearDown()은 Test Case를 진행할때마다 반복적으로 실행된다.
ex) setUp() -> TestA() -> tearDown() -> setUp() -> TestB() -> tearDown()
