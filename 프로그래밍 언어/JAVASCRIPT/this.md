### this
- this 는 현재 실행 문맥이다
- 실행문맥이란 말은 호출자가 누구냐는 것과 같다.
- 객체(this)는 함수가 실행되는 "기반", "영역","맥락",을 의미하며 이것을 실행하는 "주체"를 의미한다.
~~~ javascript
this; // Window {}
~~~

### 함수 실행에서의 this
- 함수 실행에서의 this는 전역 객체다.
~~~ javascript
function a() { console.log(this); };
a(); // Window {}
~~~

### 엄격 모드 (use strict) 에서 함수 실행에서의 this
- 엄격 모드에서 함수 실행에서의 this는 undefined다.

###  메소드 실행에서의 this(객체 내부의 속성으로 있는 함수)
~~~ javascript
var calc = {
  num: 0,
  increment: function() {
    console.log(this === calc); // => true
    this.num += 1;
    return this.num;
  }
};
// 메소드 실행. 여기서의 this는 calc.
calc.increment(); // => 1
calc.increment(); // => 2
~~~


### 생성자 실행에서의 this
- 생성자 실행에서의 this는 새롭게 만들어진 객체이다
~~~ javascript
function Foo () {
  console.log(this instanceof Foo); // => true
  this.property = 'Default Value';
}
// 생성자 실행
var fooInstance = new Foo();
fooInstance.property; // => 'Default Value'
~~~
