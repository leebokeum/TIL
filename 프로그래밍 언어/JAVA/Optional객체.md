### Optional 객체
- Optional는 존재할 수도 있지만 안 할 수도 있는 객체, 즉, null이 될 수도 있는 객체”을 감싸고 있는 일종의 래퍼 클래스이다.
- 직접 다루기에 위험하고 까다로운 null을 담을 수 있는 특수한 그릇으로 생각하시면 이해가 쉽다.

### 효용
- NPE를 유발할 수 있는 null을 직접 다루지 않아도 된다.
- 수고롭게 null 체크를 직접 하지 않아도 된다.
- 명시적으로 해당 변수가 null일 수도 있다는 가능성을 표현할 수 있다. (따라서 불필요한 방어 로직을 줄일 수 있다.)

### Optional 변수 선언하기

``` java
Optional<Order> maybeOrder; // Order 타입의 객체를 감쌀 수 있는 Optional 타입의 변수
Optional<Member> optMember; // Member 타입의 객체를 감쌀 수 있는 Optional 타입의 변수
Optional<Address> address; // Address 타입의 객체를 감쌀 수 있는 Optional 타입의 변수
```

### Optional 객체 생성하기
- Optional.empty()
null을 담고 있는, 한 마디로 비어있는 Optional 객체를 얻어온다.
이 비어있는 객체는 Optional 내부적으로 미리 생성해놓은 싱글턴 인스턴스이다.
``` java
Optional<Member> maybeMember = Optional.empty();
```
- Optional.of(value)
null이 아닌 객체를 담고 있는 Optional 객체를 생성한다.
null이 넘어올 경우, NPE를 던지기 때문에 주의해서 사용해야 한다.
``` java
Optional<Member> maybeMember = Optional.of(aMember);
```
- Optional.ofNullable(value)
null인지 아닌지 확신할 수 없는 객체를 담고 있는 Optional 객체를 생성한다.
Optional.empty()와 Optional.of(value)를 합쳐놓은 메소드라고 생각하면 된다.
null이 넘어올 경우, NPE를 던지지 않고 Optional.empty()와 동일하게 비어 있는 Optional 객체를 얻어온다.
해당 객체가 null인지 아닌지 자신이 없는 상황에서는 이 메소드를 사용해야 한다.
``` java
Optional<Member> maybeMember = Optional.ofNullable(aMember);
Optional<Member> maybeNotMember = Optional.ofNullable(null);
```


### 참조
https://www.daleseo.com/java8-optional-after/