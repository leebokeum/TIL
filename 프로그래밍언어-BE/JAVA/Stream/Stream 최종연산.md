### Stream 최종 연산
1. Max/Min/Sum/Average/Count 
2. 데이터 수집 - collect()
- Stream의 요소들을 List나 Set, Map, 등 다른 종류의 결과로 수집하고 싶은 경우에는 collect 함수를 이용할 수 있다. collect 함수는 어떻게 Stream의 요소들을 수집할 것인가를 정의한 Collector 타입을 인자로 받아서 처리한다.
```java
collect() : 스트림의 최종연산, 매개변수로 Collector를 필요로 한다.
Collector : 인터페이스, collect의 파라미터는 이 인터페이스를 구현해야한다.
Collectors : 클래스, static메소드로 미리 작성된 컬렉터를 제공한다.

// collect의 파라미터로 Collector의 구현체가 와야 한다.
Object collect(Collector collector)
```

3. 조건 검사 - Match 
- Stream의 요소들이 특정한 조건을 충족하는지 검사하고 싶은 경우에는 match 함수를 이용할 수 있다. match 함수는 함수형 인터페이스 Predicate를 받아서 해당 조건을 만족하는지 검사를 하게 되고, 검사 결과를 boolean으로 반환한다. match 함수에는 크게 다음의 3가지가 있다.

anyMatch: 1개의 요소라도 해당 조건을 만족하는가
allMatch: 모든 요소가 해당 조건을 만족하는가
nonMatch: 모든 요소가 해당 조건을 만족하지 않는가

4. 특정 연산 수행 - forEach 
- Stream의 요소들을 대상으로 어떤 특정한 연산을 수행하고 싶은 경우에는 forEach 함수를 이용할 수 있다. 앞에서 살펴본 비슷한 함수로 peek()가 있다. peek()는 중간 연산으로써 실제 요소들에 영향을 주지 않은 채로 작업을 진행하고, Stream을 반환하는 함수였다. 하지만 forEach()는 최종 연산으로써 실제 요소들에 영향을 줄 수 있으며, 반환값이 존재하지 않는다. 예를 들어 요소들을 출력하기를 원할 때 다음과 같이 forEach를 사용할 수 있다.