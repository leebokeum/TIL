### String
- char 타입의 배열이 Stirng이다.
- 원시 타입처럼 취급하기 때문에, 리터럴을 생성할 때 new 키워드를 이용할 필요가 없다.
- 실제 컴파일시 따옴표 사이이에 있는 문자들은 String 객체로 생성된다.


### String 객체의 값을 변경할 수 있는가?
- Stirng 클래스에서는 String 객체의 값을 변경하는 것처럼 보이는 메서드가 실제로는 String 인스턴스를 반환한다. 
- substirng 또는 replace, splict 같은 메서드를 호출하면 String 객체의 새 복사본을 반환한다.

### String / StringBuffer / StringBuilder 차이점 & 장단점
- String은 immutable, StirngBuffer 와 StringBuilder는 mutable 객체이다.
- String 객체는 문자열 연산이 많은 경우 그 성능이 좋지 않다.

### StringBuffer vs StringBuilder
- 문자열 연산 등으로 기존 객체의 공간이 부족하게 되는 경우,기존의 버퍼 크기를 늘리며 유연하게 동작합니다. StringBuffer와 StringBuilder 클래스가 제공하는 메서드는 서로 동일합니다.

- StringBuffer는 각 메서드별로 Synchronized Keyword가 존재하여, 멀티스레드 환경에서도 동기화를 지원. 반면 StringBuilder는 동기화를 보장하지 않음. 그래서 멀티스레드 환경이라면 값 동기화 보장을 위해 StringBuffer를 사용하고 단일 스레드 환경이라면 StringBuilder를 사용한다.