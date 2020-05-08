### 리플렉션(Reflection)
- 객체를 통해 클래스의 정보를 분석해내는 프로그램 기법
- 클래스 파일의 위치나 이름만 있으면 해당 클래스의 정보를 얻어내고, 객체를 생성하는 것 또한 가능하게 해주는 유연한 프로그래밍을 위한 기법

### Class.class
- 자바 프로그래밍을 하다보면 .class 라는 문구가 코드 내에 빈번하게 등장
``` java
String.class
```
- Class 클래스는 자바에서 사용되는 클래스들에 대한 구조를 가지고 있는 Class
![alt text](https://t1.daumcdn.net/cfile/tistory/225DC23857A567E01A)
- Class 객체의 메소드들의 반환형인 반환형인 Field, Method, Package, Constructor 등은 모두 reflect 패키지에서 제공해주는 클래스이다.

