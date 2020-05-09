### 플러그인 사용하기 - use() 메소드
~~~ javascript
// `MyPlugin.install(Vue)` 호출
Vue.use(MyPlugin)

new Vue({
  //... options
})
~~~

- Vue.use는 자동으로 같은 플러그인을 두 번 이상 사용하지 못하기 때문에 같은 플러그인에서 여러 번 호출하면 플러그인이 한 번만 설치된다.

