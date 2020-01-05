### String
- char 타입의 배열이 Stirng이다.
- 원시 타입처럼 취급하기 때문에, 리터럴을 생성할 때 new 키워드를 이용할 필요가 없다.
- 실제 컴파일시 따옴표 사이이에 있는 문자들은 String 객체로 생성된다.


### String 객체의 값을 변경할 수 있는가?
- Stirng 클래스에서는 String 객체의 값을 변경하는 것처럼 보이는 메서드가 실제로는 String 인스턴스를 반환한다. 
- substirng 또는 replace, splict 같은 메서드를 호출하면 String 객체의 새 복사본을 반환한다.