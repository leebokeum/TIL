### 열거형 타입 Enum
- 몇가지의 한정된 데이터들을 가지는 경우가 있다. 대표적으로는 "요일"이나 "계절" 같은것이지요 요일은 월,화,수,목,금,토,일 이렇게 7가지밖고 계절도 봄,여름,가을,겨울 4가지 계절로 한정되어 있다. 이렇게 이와 같이 한정된 데이터들을 갖는 데이터들은 열거형으로 묶어주면 편하다.

~~~ java
enum Season {
    봄, 여름, 가을, 겨울
}

public class People {
    public String name; //이름
    public Season favorite_session; //좋아하는계절

    public static void main(String[] args) {
    	People people = new People();
        
    	people.name = "홍길동";
    	people.favorite_session = Season.봄;
         
        System.out.println("이름 : " + people.name);
        System.out.println("좋아하는 계절 : " + people.favorite_session);
    }
}
~~~

- 객체 내장 메소드
~~~ java
ordinal(), valueOf(), name(), compareTo()
~~~