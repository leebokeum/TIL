#### 재사용 가능한 components
- Vue 컴포넌트의 API는 prop, 이벤트 및 슬롯의 세 부분으로 나뉩니다.
    - Props 는 외부 환경이 데이터를 컴포넌트로 전달하도록 허용합니다.
    - 이벤트를 통해 컴포넌트가 외부 환경에서 사이드이펙트를 발생할 수 있도록 합니다.
    - 슬롯 을 사용하면 외부 환경에서 추가 컨텐츠가 포함 된 컴포넌트를 작성할 수 있습니다.

``` html
<my-component
  :foo="baz"
  :bar="qux"
  @event-a="doThis"
  @event-b="doThat"
>
  <img slot="icon" src="...">
  <p slot="main-text">Hello!</p>
</my-component>
```