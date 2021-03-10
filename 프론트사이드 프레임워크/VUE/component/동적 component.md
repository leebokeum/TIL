### 동적 컴포넌트 is
``` html
<component v-bind:is="currentView">
  <!-- vm.currentView가 변경되면 컴포넌트가 변경됩니다! -->
</component>
```