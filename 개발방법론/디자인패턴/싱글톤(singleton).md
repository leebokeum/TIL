### 싱글톤 패턴
- 인스턴스가 오직 하나여야 하고 인스턴스 접근, 생성 방식이 오직 하나여야한다.
- 애플리케이션이 시작될 때 어떤 클래스가 최초 한번만 메모리를 할당하고(Static) 그 메모리에 인스턴스를 만들어 사용하는 디자인패턴.

### 장점
- 고정된 메모리 영역을 얻으면서 한번의 new로 인스턴스를 사용하기 때문에 메모리 낭비를 방지할 수 있음
- 싱글톤으로 만들어진 클래스의 인스턴스는 전역 인스턴스이기 때문에 다른 클래스의 인스턴스들이 데이터를 공유하기 쉽다.

### 활용
- DBCP(DataBase Connection Pool)처럼 공통된 객체를 여러개 생성해서 사용해야하는 상황에서 많이 사용.
- 쓰레드풀, 캐시, 대화상자, 사용자 설정, 레지스트리 설정, 로그 기록 객체등

### 만드는 방법
- private 생성자(외부에서 접근 금지)
- private static 인스턴스 변수
- public static getInstance() method

### 예제
~~~ java

public class Singleton {

    public static Singleton st;

    private static Singleton getInstance(){
        if(st == null){
            st = new Singleton();
        }
    }

    private Singleton(){

    }
}

~~~
