### VUE 인스턴스
- https://kr.vuejs.org/v2/api/index.html

~~~ js
var vm = new Vue({
  // 옵션
})
~~~

#### Vue.config
- Vue의 전역 설정을 가지고 있는 객체입니다. 앱이 실행하기 전에 아래의 속성들을 변경할 수 있다.
- silent : 모든 Vue의 로그와 경고를 출력하지 않습니다.
- optionMergeStrategies : 사용자 정의 병합 전략을 설정할 수 있다.
  - 부모 및 자식 인스턴스에 정의된 해당 옵션의 값을 첫번째와 두번째 인자로 전달 받는다.
- devtools : vue-devtools를 사용할 수 있게 한다.
- errorHandler : 컴포넌트 렌더 함수 및 감시자 중에 잡히지 않은 오류에 대한 핸들러를 할당한다.
- keyCodes : v-on에 사용자 정의 키를 할당한다.


### 전역 API
- Vue.extend( options ) : Vue 생성자의 “하위 클래스”를 만든다.
- Vue.nextTick( [callback, context] ) : 다음 DOM 업데이트 사이클 이후 실행하는 콜백을 연기한다.
- Vue.set( target, propertyName/index, value ) : 객체에 대한 속성을 설정한다.
- Vue.delete( target, propertyName/index ) : 객체의 속성을 삭제한다.
- Vue.directive( id, [definition] ) : 전역 디렉티브를 등록하거나 검색 한다.
- Vue.filter( id, [definition] ) : 전역 필터를 등록하거나 검색
- Vue.component( id, [definition] ) : 전역 컴포넌트를 등록하거나 검색한다.
- Vue.use( plugin ) : Vue.js 플러그인을 설치한다. 플러그인이 Object인 경우 install 메소드를 가져야 한다.
  - 이 메소드는 new Vue()를 호출하기 전에 사용되어야 한다.
- Vue.mixin( mixin ) : 전역으로 mixin을 적용한다.. 생성된 모든 Vue 인스턴스에 영향한다.
- Vue.compile( template ) : 템플릿 문자열을 렌더링 함수로 컴파일
  

### 옵션
- data
- props : 부모 컴포넌트의 데이터를 받을 수 있게 노출된 속성의 리스트/해시한다.
    ~~~ js
        // 단순한 구문
        Vue.component('props-demo-simple', {
        props: ['size', 'myMessage']
        })
    ~~~
- computed : Vue 인스턴스에 추가되는 계산된 속성이다. 모든 getter와 setter는 자동으로 this 컨텍스트를 Vue 인스턴스에 바인딩 한다.
- methods
- watch : Vue 인스턴스는 인스턴스 생성시 객체의 각 항목에 대해 $watch()를 호출한다.
    ~~~ js
    var vm = new Vue({
        data: {
            a: 1,
            b: 2,
            c: 3,
            d: 4,
            e: {
            f: {
                g: 5
            }
            }
        },
        watch: {
            a: function (val, oldVal) {
            console.log('new: %s, old: %s', val, oldVal)
            },
            // 문자열 메소드 이름
            b: 'someMethod',
            // 깊은 감시자
            c: {
            handler: function (val, oldVal) { /* ... */ },
            deep: true
            },
            // 콜백은 관찰이 시작된 직후 호출됩니다.
            d: {
            handler: 'someMethod',
            immediate: true
            },
            e: [
            'handle1',
            function handle2 (val, oldVal) { /* ... */ },
            {
                handler: function handle3 (val, oldVal) { /* ... */ },
                /* ... */
            }
            ],
            // watch vm.e.f's value: {g: 5}
            'e.f': function (val, oldVal) { /* ... */ }
        }
        })
        vm.a = 2 // => new: 2, old: 1
    ~~~
- el
- template
- render
- beforeCreate
- created
- beforeMount
- mounted
- beforeUpdate
- updated
- activated : keep-alive 인 컴포넌트가 활성화 될 때 호출
- deactivated
- beforeDestroy
- destroyed
- directives
- filters
- components
- parent : 부모는 자식에 대해 this.$parent로 접근할 수 있고 자식은 부모의 $children배열로 추가 된다.
- mixins
- name
- model


### $ 인스턴스
- vm.$data
- vm.$props
- vm.$el
- vm.$options
- vm.$parent
- vm.$root
- vm.$children
- vm.$slots
- vm.$scopedSlots
- vm.$refs : ref 속성이 등록된 자식 컴포넌트와 DOM 엘리먼트 객체이다.
- vm.$isServer
- vm.$attrs : props로 인식(및 추출)되지 않는 부모 범위 속성 바인딩이다.
- vm.$listeners : v-on="$listeners"를 통해 내부 컴포넌트로 전달할 수 있다.
- vm.$watch
- vm.$set : 전역 Vue.set의 별칭 
- vm.$delete : 전역 Vue.delete의 별칭 
- vm.$on : 현재 VM에서 사용자 정의 이벤트를 듣느다. 이벤트는 vm.$emit에 의해 호출될 수 있다.
    ~~~ js
        vm.$on('test', function (msg) {
            console.log(msg)
        })
        vm.$emit('test', 'hi')
        // => "hi"
    ~~~
- vm.$once
- vm.$off
- vm.$emit : 현재 인스턴스에서 이벤트를 트리거
  ~~~ js
    Vue.component('magic-eight-ball', {
    data: function () {
        return {
        possibleAdvice: ['Yes', 'No', 'Maybe']
        }
    },
    methods: {
        giveAdvice: function () {
        var randomAdviceIndex = Math.floor(Math.random() * this.possibleAdvice.length)
        this.$emit('give-advice', this.possibleAdvice[randomAdviceIndex])
        }
    },
    template: `
        <button v-on:click="giveAdvice">
        Click me for advice
        </button>
    `
    })
  ~~~
- vm.$mount
- vm.$forceUpdate()
- vm.$nextTick( [callback] )
- vm.$destroy()
  

### 디렉티브
- v-text
- v-html
- v-show
- v-if
- v-else
- v-else-if
- v-for
- v-on
- v-bind
- v-model
- v-pre
- v-cloak
- v-once : 엘리먼트 및 컴포넌트를 한번만 렌더링한다.
- 



## 출처
https://kr.vuejs.org/v2/api