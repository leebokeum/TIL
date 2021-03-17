#### Plugin 만들기
``` js
Vue.use();
```
- Vue.use() 코드가 바로 플러그인을 설치하여 사용하는 코드
- 플러그인을 한번 설치하고 나면 뷰 인스턴스의 내부에 플러그인에 정의한 기능이 추가된다. 컴포넌트 내부에서 this로 해당 기능을 편하게 접근할 수 있다.
- 이런 이유로 자주 사용되는 라이브러리나 기능들은 플러그인으로 정의하여 사용하는 것이 좋다.


#### 만드는 방법
```js
// 만들기
export default {
  install(Vue, options) {
    Vue.prototype.ChartJS = Chart;
  }
}

// 적용
import ChartPlugin from './ChartPlugin.js';
Vue.use(ChartPlugin);

// 사용
this.ChartJS
```


### 사용 가능한 것들
``` js
// 1. 전역 메소드 또는 속성 추가
  Vue.myGlobalMethod = function () {
    // 필요한 로직 ...
  }
// 2. 전역 에셋 추가
  Vue.directive('my-directive', {
    bind (el, binding, vnode, oldVnode) {
      // 필요한 로직 ...
    }
    ...
  })
// 3. 컴포넌트 옵션 주입
  Vue.mixin({
    created: function () {
      // 필요한 로직 ...
    }
    ...
  })
// 4. 인스턴스 메소드 추가
Vue.prototype.$myMethod = function (options) {
  // 필요한 로직 ...
  }
```