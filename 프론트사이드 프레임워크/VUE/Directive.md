### Directive란
- 디렉티브란, HTML 태그 안에 들어가는 속성의 역할을 하며, v-라는 접두사가 붙는 것이 특징입니다.

### html 속성에 접근하는 v-bind
- html 속성에 Vue내의 값을 사용할 수 있도록 도와주는 v-bind
~~~ javascript
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
    <div id="app">
    <a v-bind:href="link">링크</a>
    </div>
~~~
- v-bind 디렉티브를 사용하여 Vue 인스턴스 내에 선언된 값을 HTML 코드의 속성 값에 사용할 수 있다.
- v-bind 약어 :
    - v-bind:href=“url”을 줄여서 :href=”url” 이라고 표기해줄 수 있습니다.

### v-on
- v-on 디렉티브를 사용하여 DOM 이벤트를 듣고 트리거 될 때 JavaScript를 실행할 수 있다.
~~~ javascript
    <div id="example-1">
    <button v-on:click="counter += 1">Add 1</button>
    <p>위 버튼을 클릭한 횟수는 {{ counter }} 번 입니다.</p>
    </div>

    var example1 = new Vue({
    el: '#example-1',
    data: {
        counter: 0
    }
    })
~~~

- 이벤트 수식어
    - event.preventDefault() 또는 event.stopPropagation()를 호출하는 것은 매우 보편적인 일입니다. 메소드 내에서 쉽게 이 작업을 할 수 있지만, DOM 이벤트 세부 사항을 처리하는 대신 데이터 로직에 대한 메소드만 사용할 수 있으면 더 좋다.
    - .stop
    - .prevent
    - .capture
    - .self
    - .once
    - .passive
~~~ html
    <!-- 클릭 이벤트 전파가 중단됩니다 -->
    <a v-on:click.stop="doThis"></a>

    <!-- 제출 이벤트가 페이지를 다시 로드 하지 않습니다 -->
    <form v-on:submit.prevent="onSubmit"></form>

    <!-- 수식어는 체이닝 가능합니다 -->
    <a v-on:click.stop.prevent="doThat"></a>

    <!-- 단순히 수식어만 사용할 수 있습니다 -->
    <form v-on:submit.prevent></form>

    <!-- 이벤트 리스너를 추가할 때 캡처모드를 사용합니다 -->
    <!-- 즉, 내부 엘리먼트를 대상으로 하는 이벤트가 해당 엘리먼트에서 처리되기 전에 여기서 처리합니다. -->
    <div v-on:click.capture="doThis">...</div>


    <!-- event.target이 엘리먼트 자체인 경우에만 트리거를 처리합니다 -->
    <!-- 자식 엘리먼트에서는 안됩니다 -->
    <div v-on:click.self="doThat">...</div>
~~~