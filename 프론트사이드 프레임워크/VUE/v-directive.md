### directive
``` js
// 전역 사용자 정의 디렉티브 v-focus 등록
Vue.directive('focus', {
  // 바인딩 된 엘리먼트가 DOM에 삽입되었을 때...
  inserted: function (el) {
    // 엘리먼트에 포커스를 줍니다
    el.focus()
  }
})

directives: {
  focus: {
    // 디렉티브 정의
    inserted: function (el) {
      el.focus()
    }
  }
}
```

```html
<input v-focus>크
```