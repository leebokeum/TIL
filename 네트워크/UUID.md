### UUID란
- 트워크 상에서 고유성이 보장되는 id를 만들기 위한 표준 규약.
- 주로 분산 컴퓨팅 환경에서 사용되는 식별자이다. 중앙관리시스템이 있는 환경이라면 각 세션에 일련번호를 부여해줌으로써 유일성을 보장할 수 있겠지만 중앙에서 관리되지 않는 분산 환경이라면 개별 시스템이 id를 발급하더라도 유일성이 보장되어야만 할 것이다. 이를 위해 탄생한 것이 범용고유식별자 UUID (Universally Unique IDentifier) 이다.

### 정의
- UUID는 128비트의 숫자이며, 32자리의 16진수로 표현된다. 여기에 8-4-4-4-12 글자마다 하이픈을 집어넣어 5개의 그룹으로 구분한다.
~~~ txt
예: 550e8400-e29b-41d4-a716-446655440000
~~~
- UUID 버전은 1, 3, 4 및 5가 있다. 이 중 많이 쓰이는 것은 버전 1과 4이다. 버전 1은 타임스탬프를 기준으로 생성되며, 버전 4는 랜덤 생성이다. 버전 3, 5는 각각 MD5, SHA-1 해쉬를 이용해 생성하는 방식이다.


### 자바에서 UUID 생성
~~~ java
import java.util.UUID;

public class UUIDTest {

    public static void main(String[] args) {
        UUID one = UUID.randomUUID();
        UUID two = UUID.randomUUID();

        System.out.println("UUID One: " + one.toString());
        System.out.println("UUID Two: " + two.toString());
    }
}
~~~