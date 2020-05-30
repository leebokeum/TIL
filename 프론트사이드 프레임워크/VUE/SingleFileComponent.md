### Single File Component
- 특정 화면 영역의 HTML, CSS, JS 코드를 한 파일에서 관리할 수 있는 방법. 파일 확장자는 vue이며 HTML 파일에서 뷰 개발을 진행했을 때의 한계점을 극복할 수 있는 방법이기도 하다. 한계점은 아래와 같다.

1. 모든 컴포넌트에 고유의 이름을 붙여야 함
2. js 파일에서 template 안의 html 의 문법 강조가 되지 않음
3. js 파일상에서 css 스타일링 작업이 거의 불가
4. ES5 를 이용하여 계속 앱을 작성할 경우 Babel 빌드가 지원되지 않음

~~~ javascript
<template>
  <!-- HTML -->
</template>

<script>
  // Javascript
</script>

<style>
  /* CSS */
</style>
~~~

### 참조
https://joshua1988.github.io/web-development/vuejs/vuejs-tutorial-for-beginner/#vue-cli