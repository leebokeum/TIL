### computed
- computed 속성은 기본적으로 getter 함수만 가지고 있지만, 필요한 경우 setter 함수를 만들어 쓸 수 있습니다.
- computed는 캐싱된다.

``` js
// ...
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
// ...
```

### computed에 파라미터 넘기는 방법
```js
computed: {
  foo() {
    return (bar) => {
    	return bar + 1;
    };
  }
}
```