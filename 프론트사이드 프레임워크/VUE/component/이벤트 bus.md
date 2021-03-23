### 비 부모-자식간 통신
- 때로는 두 컴포넌트가 서로 통신 할 필요가 있지만 서로 부모/자식이 아닐 수도 있습니다. 간단한 시나리오에서는 비어있는 Vue 인스턴스를 중앙 이벤트 버스로 사용할 수 있습니다.

``` js
var bus = new Vue()
// 컴포넌트 A의 메소드
bus.$emit('id-selected', 1)
// 컴포넌트 B의 created 훅
bus.$on('id-selected', function (id) {
  // ...
})
// 보다 복잡한 경우에는 전용 상태 관리 패턴을 고려해야합니다
```

eventBus.js
- event를 중앙에서 통제하는 시스템
~~~js
import Vue form 'vue';
export default new Vue();
~~~