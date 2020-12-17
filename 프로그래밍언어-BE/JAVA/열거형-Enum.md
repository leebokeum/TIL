### Enum
- 클래스처럼 보이게 하는 상수
- 서로 관련 있는 상수들을 모아 심볼릭한 명칭의 집합으로 정의한 것
- Enum 클래스형을 기반으로 한 클래스형 선언
- 새로운 열거형을 선언하면, 내부적으로 Enum 클래스형 기반의 새로우누 클래스형이 만들어짐.
-  어떤 클래스가 상수만으로 작성되어 있으면 반드시 class로 선언할 필요는 없다. 이럴 때 class로 선언된 부분에 enum이라고 선언하면 이 객체는 상수의 집합이다. 라는 것을 명시적으로 나타낸다.
-  기존에는 인터페이스나 클래스 내에서 상수를 선언함으로써 상수를 관리 하였는데 클래스 내에서 선언하는 부분은 네이밍이 겹칠 수 있고 불 필요하게 상수가 많아지는 단점이 있다.
- 인터페이스로 관리하는 경우 이런 부분은 줄어들지만 여전히 IDE의 지원을 적극적으로 받을 수 없고 타입 안정성이 떨어지는 단점을 가지고 있었다. 이를 보완하며 나온 것이 Enum이다.

~~~ java
// 사용법
<Shoes.java>
enum Type {
    WALKING, RUNNING, TRACKING, HIKING
}
public class Shoes {
    public String name;
    public int size;
    public Type type;
     
    public static void main(String[] qrgs) {
        Shoes shoes = new Shoes();
         
        shoes.name = "나이키";
        shoes.size = 230;
        shoes.type = Type.RUNNING;
         
        System.out.plintln("신발 이름 = " + shoes.name);
        System.out.plintln("신발 사이즈 = " + shoes.size);
        System.out.plintln("신발 종류 = " + shoes.type);
    }
}

# 결과
신발 이름 = 나이키
신발 사이즈 = 230
신발 종류 = RUNNING
~~~

### Enum 내장 메소드
- values() : Enum 클래스가 가지고 있는 모든 상수 값을 배열의 형태로 리턴 한다. 참고로 단순히 String 의 형태로 단순 반환하는 것이 아니라 인스턴스를 반환하는 것이다. 즉 Enum 클래스가 가지고 있는 모든 인스턴스를 배열에 담아 반환하는 것이다.
- ordinal() : 원소에 열거된 순서를 정수 값으로 반환
- valueOf() : 매개변수로 주어진 String과 열거형에서 일치하는 이름을 갖는 원소를 반환
  - 주어진 String과 일치하는 원소가 없는 경우 IllegalArgumentException 예외 발생
- name() : 열거 객체가 가지고 있는 문자열을 리턴, 이때 리턴되는 문자열은 열거 타입을 정의할때 사용한 상수 이름과 동일
- compareTo() : compareTo()메소드는 매개값으로 주어진 열거 객체를 기준으로 전후로 몇번째 위치하는지 비교
  - 만약 열거 객체가 매개값의 열거 객체보다 순번이 빠르다면 음수가, 순번이 늦다면 양수가 리턴

### 열거형 상수를 다른 값과 연결하기
~~~ java
enum Type {
    // 상수("연결할 문자")
    WALKING("워킹화"), RUNNING("러닝화")
    , TRACKING("트래킹화"), HIKING("등산화")
     
    final private String name;
     
    private Type(Stirng name) { //enum에서 생성자 같은 역할
        this.name = name;
    }
    public String getName() { // 문자를 받아오는 함수
        return name;
    }
}
public class Shoes {
    public static void main(String[] args) {
        for(Type type : Type.values()){
            System.out.println(type.getName());
        }
    }
}

# 결과
워킹화
러닝화
트래킹화
등산화
~~~


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