### 내장 플러그인 Route
- 사용하기 전에
~~~ s
    npm install --save vue-router
~~~


### 사용하기
- routes/index.js
~~~ javascript
import Vue from 'vue';
import Router from 'vue-router'; // vue 내장 플러그인
import HelloWorld from '../components/HelloWorld.vue';
import HelloWorld2 from '../components/HelloWorld2.vue';

//플러그인을 사용하기 위한 메소드 use
Vue.use(Router);

export default new Router({
    mode: 'history',
    routes: [
      {
        path: '/',
        redirect: '/HelloWorld'
      },
      {
        path: '/HelloWorld',
        component: HelloWorld,
      },
      {
        path: '/HelloWorld2',
        component: HelloWorld2,
      },
    ]
  })
~~~

- main.js
~~~ javascript
import router from './routes/index.js';

Vue.config.productionTip = false

new Vue({
  router,
  render: h => h(App),
}).$mount('#app')

~~~

- HTML
~~~ html
<div id="app">
  <h1>Hello App!</h1>
  <p>
    <!-- 네비게이션을 위해 router-link 컴포넌트를 사용합니다. -->
    <!-- 구체적인 속성은 `to` prop을 이용합니다. -->
    <!-- 기본적으로 `<router-link>`는 `<a>` 태그로 렌더링됩니다.-->
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>
  </p>
  <!-- 라우트 아울렛 -->
  <!-- 현재 라우트에 맞는 컴포넌트가 렌더링됩니다. -->
  <router-view></router-view>
</div>
~~~