### Collections 클래스
- Collections는 Collection과 다르다.
- Collections는 클래스이다. 이 클래스 안에 있는 메서드는 static이기 때문에 인스턴스를 생성하지 않고 바로 사용할 수 있다.
- Collection 인터페이스를 구현한 클래스에 대한 객체생성, 정렬(sort), 병합(merge), 검색(search) 등의 기능을 안정적으로 수행하도록 도와주는 역할을 하는 유틸리티 클래스

#### 주요 method()
- max: 지정된 컬렉션에서 최대 요소를 반환한다. (인덱스 X)
- min: 지정된 컬렉션에서 최소 요소를 반환한다. (인덱스 X)
- sort: 지정된 컬렉션을 정렬시킨다. 오버로드 메소드들이 존재하며 가장 기본적인 메소드는 자연순서에 따라 내림차순으로 정렬된다.
```java
//원소가 String 타입이므로 알파벳 순서대로 정렬.

List<String> list = new LinkedList<String>();
list.add(“철수”);
list.add(“영희”);
Collections.sort(list);
```
- shuffle: 지정된 컬렉션의 요소들의 순서를 무작위로 섞는다.
```java
// 철수와 영희의 순서가 섞이게 된다.
List<String> list = new LinkedList<String>();
list.add(“철수”);
list.add(“영희”);
Collections.shuffle(list);
```
- synchronizedCollection: 지정된 컬렉션에 의해 지원되는 동기화 된 컬렉션을 재생성해 반환한다.
- binarySearch: 지정된 컬렉션에서 이진 탐색 알고리즘을 사용해 지정된 객체를 검색해 인덱스를 반환한다.
```java
// list는 리스트, element는 탐색할 원소이다.
int index = Collections.binarySearch(list, element);
```
- disjoint	2개의 지정된 컬렉션들에서 공통된 요소가 하나도 없는 경우 true 를 반환한다.
- copy: 지정된 켈렉션의 모든 요소를 새로운 컬렉션으로 복사해 반환한다.
- reverse	지정된 컬렉션에 있는 순서를 역으로 변경한다.