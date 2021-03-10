### $root 속성
- new Vue 의 모든 하위 컴포넌트에서는 $root 속성을 이용해 루트 인스턴스에 접근할 수 있습니다

```js
// 루트 Vue 인스턴스
new Vue({
  data: {
    foo: 1
  },
  computed: {
    bar: function () { /* ... */ }
  },
  methods: {
    baz: function () { /* ... */ }
  }
})

모든 하위 컴포넌트에서 아래와 같이 접근할 수 있으며, 전역 저장소처럼 활용할 수 있습니다.

// root의 데이터 가져오기
this.$root.foo

// root의 데이터 수정하기
this.$root.foo = 2

// root의 computed 속성 접근하기
this.$root.bar

// root의 method 사용하기
this.$root.baz()

// 이러한 패턴은 아주 작은 크기의 어플리케이션이나 적은 수의 컴포넌트에 대해서 유용하게 사용될수는 있습니다. 하지만 어플리케이션의 크기가 커지게 될 때 해당 패턴을 확장하기란 쉬운 일이 아닙니다. 대부분의 경우, 상태 관리를 위해 Vuex 를 사용하는 것을 강력히 권장합니다..
```