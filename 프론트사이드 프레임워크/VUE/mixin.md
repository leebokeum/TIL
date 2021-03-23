#### mixin 사용법
```js
const toggle = {
  data() {
    return {
      isShowing: false
    }
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing;
    }
  }
}
​
const Modal = {
  template: '#modal',
  mixins: [toggle],
  components: {
    appChild: Child
  }
};
​
const Tooltip = {
  template: '#tooltip',
  mixins: [toggle],
  components: {
    appChild: Child
  }
};

```

### 출처
출처: https://itmining.tistory.com/123 [IT 마이닝]