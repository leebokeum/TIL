### 함수는 객체다.
- 함수는 함수객체라고 불린다. 객체는 (변수)프로퍼티와 함수형태인 프로퍼티를 갖는데 여기서 함수인 프로퍼티를 메서드라고 부른다. 객체는 .(점 연산자)를 통해 자신의 프로퍼티인 메서드를 사용할 수 있다.

### call,apply,bind는 함수의 메서드(프로퍼티)다.
- call,apply,bind는 함수의 프로퍼티(메서드)다
- 이런 이유로 다음과 같이 call,apply,bind를 사용 할 수 있다.
    - 함수이름.call() , 함수이름.apply() , 함수이름.bind()
- 그 이유는 부모인 Function.Prototype으로 부터 call,apply,bind을 물려받았기 때문이다. 

### call,apply,bind로 함수의 실행영역을 지정한다.
- 함수가 호출형태에 따라 this가 달라진다 반면에,call,apply,bind메서드는 외부에서 할당하는 첫번째 인자가 그 함수의 this가 된다. 함수 자신의 실행"환경"을 외부 this로 설정할 수 있는 것이 주요한 특징이다.


### Call, apply
-  첫 번째 인자로 this를 넣고, call은 보통 함수와 똑같이 인자를 넣고, apply는 인자를 하나로 묶어 배열로 만들어 넣는다.
~~~ javascript
var example = function (a, b, c) {
  return a + b + c;
};
example(1, 2, 3);
example.call(this, 1, 2, 3);
example.apply(this, [1, 2, 3]);'
~~~


### bind
- bind 함수는 함수가 가리키는 this만 바꾸고 호출하지는 않는 겁니다. 
~~~ javascript
var obj = {
  string: 'zero',
  yell: function() {
    alert(this.string);
  }
};
var obj2 = {
  string: 'what?'
};
var yell2 = obj.yell.bind(obj2);
yell2(); // 'what?'
~~~