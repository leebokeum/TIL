### lang 패키지
- java.lang은 자바 프로그램에서 가장 많이 사용되는 패키지로서 자바 프로그램내에 'import' 문을 사용하지 않아도 자동으로 포함된다. 그만큼 자바 프로그램의 기본이 되는 클래스들과 인터페이스들이 포함되어 있다.

![alt text](https://t1.daumcdn.net/cfile/tistory/233BA837529F47710A)

### Object
- java.lang.Object 클래스는 자바 API의 모든 클래스와 사용자가 정의한 모든 클래스의 최상위 클래스이다. 즉, 모든 자바 클래스들은 Object 클래스로부터 상속받는다

- 주요 메소드

| 메소드 | 설 명  |
| :-------- | :--------: |
| boolean equals(Object obj)  | 두 개의 객체가 같은지 비교하여 같으면 true를, 같지 않으면 false를 반환한다. | 
| protected Object clone() | 객체를 복사한다.  | 
| protected void finalize()   | 가비지 컬렉션 직전에 객체의 리소스를 정리할 때 호출한다. | 
| int hashCode()   | 객체의 코드값을 반환한다.   | 
| void notify()   | wait된 스레드 실행을 재개할 때 호출한다.|
| void notifyAll()  | wait된 모든 스레드 실행을 재개할 때 호출한다. |
| void wait()   | 레드를 일시적으로 중지할 때 호출한다. |
| void wait(long timeout)   | 주어진 시간만큼 스레드를 일시적으로 중지할 때 호출한다.|
| void wait(long timeout, int nanos)   | 주어진 시간만큼 스레드를 일시적으로 중지할 때 호출한다.|

