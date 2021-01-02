### Array
- pop : 배열 뒷부분의 값을 삭제
- push : 배열 뒷부분에 값을 삽입
- unshift : 배열 앞부분에 값을 삽입
- shift : 배열 앞부분의 값을 삭제
- splice : 배열의 특정위치에 요소를 추가하거나 삭제
- slice( startIndex, endIndex) : 배열의 startIndex부터 endIndex까지(endIndex는 불포함)에 대한 shallow copy를 새로운 배열 객체로 반환
- concat : 다수의 배열을 합치고 병합된 배열의 사본을 반환


### 유용한 api
- every : 배열의 **모든** 요소가 제공한 함수로 구현된 테스트를 통과하는지를 테스트
~~~ js
var arr =[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
var isEven = function( value ) {

  // value가 2의 배수이면 true를 반환한다.
  return value % 2 === 0;
};
console.log( arr.every( isEven ) ); // false  모든 요소가 true이면 true를 return 하고 그렇지 않으면 false
~~~
- some L 지정된 함수의 결과가 true일 때까지 배열의 각 원소를 반복
~~~ js
var arr =[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
var isEven = function( value ) {

  // value가 2의 배수이면 true를 반환한다.
  return value % 2 === 0;
};
console.log( arr.some( isEven ) ); // true  하나라도 true이면 true를 return
~~~


- forEach : 배열의 각 원소별로 지정된 함수를 실행한다.
- map : 배열의 각 원소별로 지정된 함수를 실행한 결과로 구성된 새로운 배열을 반환한다.
~~~ js
var arr =[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
var isEven = function( value ) {
  return value % 2 === 0;
};
var newArr = arr.map( isEven );
console.log( newArr ); // [ false, true, false, true, false, true, false, true, false, true ]
~~~
- filter : 지정된 함수의 결과 값을 true로 만드는 원소들로만 구성된 별도의 배열을 반환한다.
-  reduce : 누산기(accumulator) 및 배열의 각 값(좌에서 우로)에 대해 (누산된) 한 값으로 줄도록 함수를 적용
~~~ js
var arr =[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
var value = arr.reduce( function( previousValue, currentValue, index ) {
  return previousValue + currentValue;
});
console.log( value ); // 55
~~~

- reverse : 배열의 원소 순서를 거꾸로 바꾼다.
- sort : 배열의 원소를 알파벳순으로, 또는 지정된 함수에 따른 순서로 정렬한다. 모든 원소를 문자열로 취급해 사전적으로 정렬
- toString : 배열을 문자열로 바꾸어 반환한다
- valueOf : toString과 비슷, 그러나 배열을 반환
- join : 배열 원소 전부를 하나의 문자열로 합친다.

