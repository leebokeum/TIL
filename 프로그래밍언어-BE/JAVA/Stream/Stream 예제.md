### stream 예제

1. List 형태를 Map 형태로 바꿔봅시다. List<V> 형태와 같이 특정 오브젝트 타입의 리스트를 오브젝트의 한 필드를 키로 하는 Map<K, V> 형태로 변경합니다.
```java
List<Person> personList = new ArrayList<>();
personList.add(new Person("짱구", 23, "010-1234-1234"));
personList.add(new Person("유리", 24, "010-2341-2341"));
personList.add(new Person("철수", 29, "010-3412-3412"));
personList.add(new Person("맹구", 25, null));

// Function.identity는 t -> t, 항상 입력된 인자(자신)를 반환합니다.
Map<String, Person> personMap = personList.stream()
        .collect(Collectors.toMap(Person::getName, Function.identity()));

// 추가적으로 filter 메서드를 사용하면 특정 조건에 일치한 형태만 골라낼 수 있습니다.
Map<String, Person> personMap = personList.stream()
        .filter(person -> person.getAge() > 24) // 25살 이상만 골라낸다.
        .collect(Collectors.toMap(Person::getName, Function.identity()));
```

2. 스트림 내에서 null 제외하기
```java
Stream<String> stream = Stream.of("철수", "훈이", null, "유리", null);
List<String> filteredList = stream.filter(Objects::nonNull)
        .collect(Collectors.toList())
```

3. 조건에 일치한 요소 찾기
```java
List<Person> personList = new ArrayList<>();
personList.add(new Person("짱구", 23, "010-1234-1234"));
personList.add(new Person("유리", 24, "010-2341-2341"));
personList.add(new Person("맹구", 23, "010-3412-3412"));

// 짱구
Person person = personList.stream()
        .filter(p -> p.getAge() == 23)
        .findFirst().get();
// findFirst 메서드 대신에 findAny 메서드도 가능합니다. 단, 일반 스트림에서는 동일한 요소(짱구)가 결과로 나오지만 병렬 스트림에서는 매 실해마다 다를 수 있습니다. 순서에 상관없이 조건에 충족한 요소를 찾고 싶을 때 findAny 메서드가 효과적일 수 있습니다.
```

4. 스트림 정렬하기
```java
List<Person> personList = new ArrayList<>();
personList.add(new Person("짱구", 25, "010-1234-1234"));
personList.add(new Person("유리", 24, "010-2341-2341"));
personList.add(new Person("맹구", 23, "010-3412-3412"));
personList.add(new Person("훈이", 26, "010-4123-4123"));

// 맹구, 유리, 짱구, 훈이
personList.stream()
        .sorted(Comparator.comparing(Person::getAge))
        .forEach(p -> System.out.println(p.getName()));
```

5. reduce로 결과 구하기
- reduce 메서드로 스트림을 하나의 결과로 연산할 수 있습니다. 예를 들어 아래와 같이 숫자로 구성된 리스트 내의 요소를 모두 더해 합계(sum)를 구할 수 있습니다.
```java
List<Integer> list = List.of(5, 4, 2, 1, 6, 7, 8, 3);
        
// 36
Integer result = list.stream()
        .reduce(0, (value1, value2) -> value1 + value2);
```

6. 단일 컬렉션 만들기
- 2차원 배열과 같은 요소를 flatmap 메서드를 사용하여 중첩 구조를 제거하고 단일 컬렉션으로 만들 수 있습니다.
```java
String[][] names = new String[][]{
        {"짱구", "철수"}, {"훈이", "맹구"}
};

// 리스트로
List<String> list = Arrays.stream(names)
        .flatMap(Stream::of)
        .collect(Collectors.toList());
        
// 1차원 배열로
String[] flattedNames = Arrays.stream(names)
        .flatMap(Stream::of).toArray(String[]::new);
```

7. String배열을 int배열로 변환하기
8. Integer배열을 String배열로 변환하기
9. String배열을 String리스트로 변환하기
10. String리스트를 String배열로 변환하기
```java
int[] intArray = Stream.of(stringArray).mapToInt(Integer::parseInt).toArray();

String[] stringArray = Stream.of(arr).map(String::valueOf).toArray(String[]::new);

String[] stringArray = new String[]{"!", "@", "#"};
List<String> stringList = Stream.of(stringArray).collect(Collectors.toList());

List<String> stringList = new ArrayList<>(Arrays.asList("!","@","#"));
String[] stringArray = stringList.toArray(new String[0]);

```

11. stream().map()을 이용한 객체(object) 변환하기
```java
// 변환 전 클래스
@Getter
class Soldier {
  String name;
  int age;

  public Soldier(String name, int age) {
    this.name = name;
    this.age = age;
  }
}

// 변환 대상 클래스
@Getter
class King {
  String name;
  int age;
  public King(String name, int age) {
    this.name = name;
    this.age = age;
  }
}

// 샘플 Soldier stream 생성
Stream<Soldier> s = Stream.of(new Soldier("A", 18), new Soldier("B", 22), new Soldier("C", 19));

// map()을 이용하여 변환하기
List<King> k = s.map(soldier -> new King(soldier.getName(), soldier.getAge()))
		.collect(Collectors.toList());
```

12. 배열, 리스트를 정렬 후 출력하는 코드
~~~ java
// 배열, 리스트를 정렬 후 출력하는 코드
//Stream 사용 전
String[] strArr = { "mash-up", "backend", "codingsquid" }
List<String> strList = Arrays.asList(strArr);

Arrays.sort(strArr);
Collections.sort(strList);

for(String str: strArr) {
  System.out.println(str);
}

for(String str : strList) {
  System.out.println(str);
}

//Stream 사용 후
Stream<String> listStream = strList.stream();
Stream<String> arrayStream = Arrays.stream(strArr);

listStream.sorted().forEach(System.out::println);
arrayStream.sorted().forEach(System.out::println);
~~~