### ref
``` html
<div id="parent">
  <user-profile ref="profile"></user-profile>
</div>
```
```js
var parent = new Vue({ el: '#parent' })
// 자식 컴포넌트 인스턴스에 접근합니다.
var child = parent.$refs.profile
```