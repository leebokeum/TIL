### Stream이란
- JDK 8에서 추가된 API
- 파일 I/O에서 사용되는 스트림과는 다르다.
- 데이터소스를 추상화하고, 데이터를 다루는데 자주 사용되는 메서들을 정의해 놓았다.

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


### 특징
- 스트림은 데이터 소스를 변경하지 않는다.
- 