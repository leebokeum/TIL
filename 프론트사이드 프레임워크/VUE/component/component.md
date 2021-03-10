### component
- template, script, style 한 세트

### 전역 컴포넌트
- 전역 컴포넌트를 등록하려면, Vue.component(tagName, options)를 사용합니다.
``` js
Vue.component('my-component', {
  // 옵션
})
```

``` js
// todo-item 이름을 가진 컴포넌트를 정의합니다
Vue.component('todo-item', {
  template: '<li>할일 항목 하나입니다.</li>'
})

var app = new Vue(...)

<ol>
  <!-- todo-item 컴포넌트의 인스턴스 만들기 -->
  <todo-item></todo-item>
</ol>

// 최종 
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```


#### 지역 등록
모든 컴포넌트를 전역으로 등록 할 필요는 없습니다. 컴포넌트를 components 인스턴스 옵션으로 등록함으로써 다른 인스턴스/컴포넌트의 범위에서만 사용할 수있는 컴포넌트를 만들 수 있습니다
```js
var Child = {
  template: '<div>사용자 정의 컴포넌트 입니다!</div>'
}

new Vue({
  // ...
  components: {
    // <my-component> 는 상위 템플릿에서만 사용할 수 있습니다.
    'my-component': Child
  }
})
```

#### DOM 템플릿 구문 분석 경고 : is
- `<ul>`,`<ol>`,`<table>`과`<select>`와 같은 일부 엘리먼트는 그 안에 어떤 엘리먼트가 나타날 수 있는지에 대한 제한을 가지고 있으며,<option>과 같이 특정 다른 엘리먼트 안에만 나타날 수 있습니다.

```js
<table>
  <my-row>...</my-row>
</table>
// 사용자 지정 컴포넌트 <my-row> 는 잘못 된 컨텐츠가 되어, 결과적으로 렌더링시 에러를 발생시킵니다. 해결 방법은 is 특수 속성을 사용하는 것입니다 :
<table>
  <tr is="my-row"></tr>
</table>
```

#### 부모-자식 데이터 교환

![alt text](/image/vue/props-events.png)

#### 동적 Props
```html
<div>
  <input v-model="parentMsg">
  <br>
  <child v-bind:my-message="parentMsg"></child>
</div>
```

#### 단방향 데이터 흐름
- 모든 props는 하위 속성과 상위 속성 사이의 단방향 바인딩을 형성합니다. 상위 속성이 업데이트되면 하위로 흐르게 되지만 그 반대는 안됩니다. 이렇게하면 하위 컴포넌트가 실수로 부모의 상태를 변경하여 앱의 데이터 흐름을 추론하기 더 어렵게 만드는 것을 방지할 수 있습니다.
1. 이 prop는 초기 값을 전달 하는데만 사용되며 하위 컴포넌트는 이후에 이를 로컬 데이터 속성으로 사용하기만 합니다.
2. prop는 변경되어야 할 원시 값으로 전달됩니다.

1. prop의 초기 값을 초기 값으로 사용하는 로컬 데이터 속성을 정의 하십시오.

``` js
props: ['initialCounter'],
data: function () {
  return { counter: this.initialCounter }
}
```

2. prop 값으로 부터 계산된 속성을 정의 합니다.

``` js
props: ['size'],
computed: {
  normalizedSize: function () {
    return this.size.trim().toLowerCase()
  }
}
```
**자바 스크립트의 객체와 배열은 참조로 전달되므로 prop가 배열이나 객체인 경우 하위 객체 또는 배열 자체를 부모 상태로 변경하면 부모 상태에 영향을 줍니다.**

#### 검증
``` js
Vue.component('example', {
  props: {
    // 기본 타입 확인 (`null` 은 어떤 타입이든 가능하다는 뜻입니다)
    propA: Number,
    // 여러개의 가능한 타입
    propB: [String, Number],
    // 문자열이며 꼭 필요합니다
    propC: {
      type: String,
      required: true
    },
    // 숫자이며 기본 값을 가집니다
    propD: {
      type: Number,
      default: 100
    },
    // 객체/배열의 기본값은 팩토리 함수에서 반환 되어야 합니다.
    propE: {
      type: Object,
      default: function () {
        return { message: 'hello' }
      }
    },
    // 사용자 정의 유효성 검사 가능
    propF: {
      validator: function (value) {
        return value > 10
      }
    }
  }
})
```

#### 부모와의 교감
- $on(eventName)을 사용하여 이벤트를 감지 하십시오.
- $emit(eventName)을 사용하여 이벤트를 트리거 하십시오.

```html
<div id="counter-event-example">
  <p>{{ total }}</p>
  <button-counter v-on:increment="incrementTotal"></button-counter>
  <button-counter v-on:increment="incrementTotal"></button-counter>
</div>
```
```js
Vue.component('button-counter', {
  template: '<button v-on:click="incrementCounter">{{ counter }}</button>',
  data: function () {
    return {
      counter: 0
    }
  },
  methods: {
    incrementCounter: function () {
      this.counter += 1
      this.$emit('increment')
    }
  },
})

new Vue({
  el: '#counter-event-example',
  data: {
    total: 0
  },
  methods: {
    incrementTotal: function () {
      this.total += 1
    }
  }
})
```


.navtiv
- 컴포넌트의 루트 엘리먼트에서 네이티브 이벤트를 수신하려는 경우가 있을 수 있습니다. 이러한 경우 v-on 에 .native 수식자를 사용할 수 있습니다.
```html
<my-component v-on:click.native="doTheThing"></my-component>
```

.sync
일부 경우에 속성에 “양방향 바인딩”이 필요할 수 있습니다. Vue 1버전에 있던 .sync 수식어와 동일합니다. 자식 컴포넌트가 .sync를 가지는 속성을 변경하면 값의 변경이 부모에 반영됩니다. 편리하지만 단방향 데이터 흐름이 아니기 때문에 장기적으로 유지보수에 문제가 생깁니다. 자식 속성을 변경하는 코드는 부모의 상태에 영향을 미칩니다.

이 때문에 .sync는 2.0버전에서 삭제되었습니다. 그러나 재사용 가능한 컴포넌트를 만들 때 유용할 수 있다는 점을 알게 되었습니다. 부모 상태에 영향을 미치는 코드를 더욱 일관적이고 명백하게 만들어야합니다.

2.3 버전에서 속성을 위한 .sync 수식어를 다시 만들었습니다. 자동으로 v-on로 확장되는 신택스 슈가입니다.
```html
아래 코드는
<comp :foo.sync="bar"></comp>
아래와 같습니다.
<comp :foo="bar" @update:foo="val => bar = val"></comp>
```
- 하위 컴포넌트가 foo를 갱신하려면 속성을 변경하는 대신 명시적으로 이벤트를 보내야합니다.
```js
this.$emit('update:foo', newValue)
```


#### 컴포넌트의 v-model 사용자 정의
```html
<my-checkbox
  :checked="foo"
  @change="val => { foo = val }"
  value="some value">
</my-checkbox>
```