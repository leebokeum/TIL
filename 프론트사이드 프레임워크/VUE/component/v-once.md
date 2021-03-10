### v-once 를 이용한 비용이 적게드는 정적 컴포넌트
- 일반 HTML 엘리먼트를 렌더링하는 것은 Vue에서 매우 빠르지만 가끔 정적 콘텐츠가 많이 포함 된 컴포넌트가 있을 수 있습니다. 이런 경우,v-once 디렉티브를 루트 엘리먼트에 추가함으로써 캐시가 한번만 실행되도록 할 수 있습니다.

``` js
Vue.component('terms-of-service', {
  template: '\
    <div v-once>\
      <h1>Terms of Service</h1>\
      ... a lot of static content ...\
    </div>\
  '
})
```