### IE에서 오류 transpileDependencies
- transpileDependencies 옵션을 활용해 node_modules에 속해있는 라이브러리도 babel을 적용할 수 있다.
- vue.config.js에 transpileDependencies: ["모듈명"] 추가

```js
module.exports = {
... (생략)
transpileDependencies: ["모듈명"]
};
```

### 참조
https://sjquant.tistory.com/38?category=829604