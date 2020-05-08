### IIFE(Immediately Invoked Function Expression)
- 정의와 동시에 즉시 실행되는 함수를 의미한다.

### 즉시실행함수
- 즉시 실행 함수는 함수 리터럴을 () 로 감싼 뒤 바로 실행하는 형태가 일반적이다.

``` javascript
(function () { console.log('Hello World') })(); // Hello World
```

### 작성법
- function() {} 과 같이 작성되면, 자바스크립트 코드를 해석하는 파서는 이것을 함수 선언문(statement) 으로 인지한다.
- () 와 같이 괄호로 묶어주어 이것은 "함수 선언문이 아닌 "함수 표현식" 이라는 것을 명시적으로 나타내야 한다.
- () 로 묶어주는 것 외에도, 연산자를 앞에 붙여줄 경우에는 모두 즉시 실행 된다.

``` javascript
!function(a, b) { return console.log(a + b) }(1, 2) // 3
void function(a, b) { return console.log(a + b) }(1, 2) // 3
+function(a, b) { return console.log(a + b) }(1, 2) // 3
-function(a, b) { return console.log(a + b) }(1, 2) // 3
~function(a, b) { return console.log(a + b) }(1, 2) // 3
*function(a, b) { return console.log(a + b) }(1, 2) // 3
^function(a, b) { return console.log(a + b) }(1, 2) // 3
&function(a, b) { return console.log(a + b) }(1, 2) // 3
/* ... 등등 연산자를 앞에 붙이면 됩니다 ... */

(function(a, b) { return a + b })(1, 2) // 3
;(function(a, b) { return a + b })(1, 2) // 3

```